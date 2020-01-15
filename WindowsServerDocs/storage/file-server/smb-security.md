---
title: SMB セキュリティ拡張機能
description: Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB 暗号化機能について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7b96574dcfc2a4417aa36780d7bd87c2556f61f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950259"
---
# <a name="smb-security-enhancements"></a>SMB セキュリティ拡張機能

>適用対象: Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

このトピックでは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB セキュリティ強化について説明します。

## <a name="smb-encryption"></a>SMB 暗号化

SMB 暗号化は、SMB データのエンドツーエンドの暗号化を提供し、信頼されていないネットワークでの盗聴からデータを保護します。 SMB 暗号化は最小限の労力で展開できますが、特殊なハードウェアまたはソフトウェアの場合は、追加コストがわずかに増えることがあります。 インターネットプロトコルセキュリティ (IPsec) または WAN アクセラレータの要件はありません。 SMB 暗号化は、共有ごとに、またはファイルサーバー全体に対して構成できます。また、データが信頼されていないネットワークを通過するさまざまなシナリオで有効にすることができます。

>[!NOTE]
>SMB 暗号化は、保存時のセキュリティには対応していません。通常は、BitLocker ドライブ暗号化によって処理されます。

機密データを man-in-the-middle 攻撃から保護する必要がある場合は、SMB 暗号化を考慮する必要があります。 次のようなシナリオが想定されます。

- インフォメーションワーカーの機密データは、SMB プロトコルを使用して移動されます。 SMB 暗号化は、Microsoft 以外のプロバイダーによって管理されているワイドエリアネットワーク (WAN) 接続など、スキャンされたネットワークに関係なく、ファイルサーバーとクライアントの間でエンドツーエンドのプライバシーと整合性の保証を提供します。
- SMB 3.0 を使用すると、ファイルサーバーは、SQL Server や Hyper-v などのサーバーアプリケーション用に、継続的に使用可能な記憶域を提供できます。 SMB 暗号化を有効にすると、その情報を覗き見攻撃から保護する機会が得られます。 SMB 暗号化は、ほとんどの記憶域ネットワーク (San) に必要な専用ハードウェアソリューションよりも簡単に使用できます。

>[!IMPORTANT]
>暗号化されていない場合と比較した場合、エンドツーエンドの暗号化保護では、パフォーマンスの重要なコストが発生することに注意してください。

## <a name="enable-smb-encryption"></a>SMB 暗号化を有効にする

SMB 暗号化は、ファイルサーバー全体に対して、または特定のファイル共有に対してのみ有効にすることができます。 SMB 暗号化を有効にするには、次のいずれかの手順に従います。

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell を使用して SMB 暗号化を有効にする

1. 個々のファイル共有の SMB 暗号化を有効にするには、サーバーで次のスクリプトを入力します。
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. ファイルサーバー全体で SMB 暗号化を有効にするには、サーバーで次のスクリプトを入力します。
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. SMB 暗号化が有効になっている新しい SMB ファイル共有を作成するには、次のスクリプトを入力します。
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>サーバーマネージャーで SMB 暗号化を有効にする

1. サーバーマネージャーで、 **[ファイルサービスおよび記憶域サービス]** を開きます。
2. **共有** を選択して、共有 管理ページを開きます。
3. SMB 暗号化を有効にする共有を右クリックし、 **[プロパティ]** を選択します。
4. 共有の **[設定]** ページで、 **[データアクセスの暗号化]** を選択します。 この共有へのリモートファイルアクセスは暗号化されています。

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 暗号化の展開に関する考慮事項

既定では、ファイル共有またはサーバーに対して SMB 暗号化を有効にすると、SMB 3.0 クライアントのみが指定されたファイル共有へのアクセスを許可されます。 これにより、共有にアクセスするすべてのクライアントのデータを保護するという管理者の意図が適用されます。 ただし、状況によっては、管理者が SMB 3.0 をサポートしていないクライアントに対して、暗号化されていないアクセスを許可する場合があります (たとえば、混合クライアントオペレーティングシステムのバージョンが使用されている場合の移行期間中など)。 SMB 3.0 をサポートしていないクライアントに対して暗号化されていないアクセスを許可するには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

次のセクションで説明されている安全な言語ネゴシエーション機能では、中間者攻撃によって SMB 3.0 から SMB 2.0 (暗号化されていないアクセスを使用する) への接続がダウングレードされないようにします。 ただし、SMB 1.0 にダウングレードすることはできません。これにより、暗号化されていないアクセスが発生します。 Smb 3.0 クライアントが常に SMB 暗号化を使用して暗号化された共有にアクセスすることを保証するには、SMB 1.0 サーバーを無効にする必要があります。 (手順については、「 [SMB 1.0 を無効](#disabling-smb-10)にする」を参照してください)。 **– RejectUnencryptedAccess**設定が **$true**の既定の設定のままになっている場合は、暗号化対応の SMB 3.0 クライアントのみがファイル共有へのアクセスを許可されます (smb 1.0 クライアントも拒否されます)。

>[!NOTE]
>* SMB 暗号化では、Advanced Encryption Standard (AES) CCM アルゴリズムを使用してデータを暗号化および復号化します。 また、AES-CCM は、SMB 署名の設定に関係なく、暗号化されたファイル共有に対してデータ整合性検証 (署名) を提供します。 暗号化せずに SMB 署名を有効にする場合は、この操作を続行できます。 詳細については、「 [SMB 署名の基本](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)」を参照してください。
>* 組織でワイドエリアネットワーク (WAN) アクセラレーションアプライアンスを使用している場合は、ファイル共有またはサーバーにアクセスしようとすると問題が発生することがあります。
>* 既定の構成 (暗号化されたファイル共有への暗号化されていないアクセスが許可されていない場合) では、SMB 3.0 をサポートしていないクライアントが暗号化されたファイル共有にアクセスしようとすると、イベント ID 1003 が SmbServer/Operational イベントログに記録され、クライアントは**アクセス拒否**エラーメッセージを受け取ります。
>* NTFS ファイルシステムの SMB 暗号化と暗号化ファイルシステム (EFS) には関連がありません。また、SMB 暗号化は、EFS の使用には必要ありません。
>* SMB 暗号化と BitLocker ドライブ暗号化は関係ありません。 SMB 暗号化は、BitLocker ドライブ暗号化の使用には必要ありません。

## <a name="secure-dialect-negotiation"></a>セキュリティで保護された言語ネゴシエーション

SMB 3.0 は、SMB 2.0 または SMB 3.0 プロトコルのダウングレードを試みる man-in-the-middle 攻撃や、クライアントとサーバーがネゴシエートする機能を検出することができます。 このような攻撃がクライアントまたはサーバーによって検出されると、接続が切断され、SmbServer/Operational イベントログにイベント ID 1005 が記録されます。 セキュリティで保護された言語ネゴシエーションは、SMB 2.0 または3.0 から SMB 1.0 へのダウングレードを検出または防止できません。 このため、SMB 暗号化のすべての機能を利用するには、SMB 1.0 サーバーを無効にすることを強くお勧めします。 詳細については、「 [SMB 1.0 の無効化](#disabling-smb-10)」を参照してください。

次のセクションで説明されている安全な言語ネゴシエーション機能では、中間者攻撃によって SMB 3 から SMB 2 (暗号化されていないアクセスを使用する) への接続がダウングレードされないようにします。ただし、SMB 1 へのダウングレードを防ぐことはできません。これにより、暗号化されていないアクセスが発生します。 以前の Windows 以外の SMB 実装で発生する可能性のある問題の詳細については、 [Microsoft サポート技術](https://support.microsoft.com/kb/2686098)情報を参照してください。

## <a name="new-signing-algorithm"></a>新しい署名アルゴリズム

SMB 3.0 は、署名のためにより新しい暗号化アルゴリズムを使用します: Advanced Encryption Standard (AES)-暗号ベースのメッセージ認証コード (CMAC)。 SMB 2.0 では、古い HMAC SHA256 暗号化アルゴリズムが使用されていました。 Aes-CMAC と AES-CCM を使用すると、AES 命令をサポートする最新の Cpu のデータ暗号化を大幅に高速化できます。 詳細については、「 [SMB 署名の基本](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)」を参照してください。

## <a name="disabling-smb-10"></a>SMB 1.0 を無効にする

従来のコンピューターブラウザーサービスと SMB 1.0 のリモート管理プロトコルの機能は別になったため、削除することができます。 これらの機能は既定で有効になっていますが、Windows Server 2003 または Windows XP を実行しているコンピューターなどの古い SMB クライアントがない場合は、SMB 1.0 の機能を削除してセキュリティを強化し、修正プログラムの適用を減らすことができます。

>[!NOTE]
>SMB 2.0 は、Windows Server 2008 と Windows Vista で導入されました。 Windows Server 2003 または Windows XP を実行しているコンピューターなどの古いクライアントは、SMB 2.0 をサポートしていません。SMB 1.0 サーバーが無効になっていると、ファイル共有や印刷共有にアクセスできなくなります。 また、Microsoft 以外の一部の SMB クライアントは、SMB 2.0 ファイル共有または印刷共有 (たとえば、"共有のスキャン" 機能を持つプリンター) にアクセスできない場合があります。

Smb 1.0 の無効化を開始する前に、smb クライアントが SMB 1.0 を実行しているサーバーに現在接続されているかどうかを確認する必要があります。 これを行うには、Windows PowerShell で次のコマンドレットを入力します。

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>監査証跡を構築するには、1週間 (1 日に複数回) にわたってこのスクリプトを繰り返し実行する必要があります。 これは、スケジュールされたタスクとして実行することもできます。

SMB 1.0 を無効にするには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>Smb 1.0 を実行しているサーバーが無効になっているために SMB クライアント接続が拒否された場合は、SmbServer/Operational イベントログにイベント ID 1001 が記録されます。

## <a name="more-information"></a>説明を見る

ここでは、Windows Server 2012 の SMB および関連テクノロジに関するその他のリソースについて説明します。

- [サーバーメッセージブロック](file-server-smb-overview.md)
- [Windows Server の記憶域](../storage.md)
- [アプリケーションデータのスケールアウトファイルサーバー](../../failover-clustering/sofs-overview.md)