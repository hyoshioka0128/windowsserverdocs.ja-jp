---
title: SMB セキュリティ拡張機能
description: Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB 暗号化機能について説明します。
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: e81b5ca5d28c33187b90fbabebc3d3f36073124c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954699"
---
# <a name="smb-security-enhancements"></a>SMB セキュリティ拡張機能

>適用先:Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

このトピックでは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB セキュリティ拡張機能について説明します。

## <a name="smb-encryption"></a>SMB 暗号化

SMB 暗号化は、SMB データをエンド ツー エンドで暗号化し、信頼できないネットワークで発生する傍受からデータを保護できます。 SMB 暗号化は最小限の労力で展開できますが、特殊なハードウェアまたはソフトウェアの場合は、追加コストがいくらか必要になることもあります。 インターネット プロトコル セキュリティ (IPsec) または WAN アクセラレータの要件はありません。 SMB 暗号化は共有ごとでもファイル サーバー全体でも構成できます。また、信頼できないネットワークをデータが通過するさまざまなシナリオにおいて有効にできます。

>[!NOTE]
>SMB 暗号化は保存時のセキュリティには対応しておらず、これは通常、BitLocker ドライブ暗号化によって処理されます。

man-in-the-middle 攻撃から機密データを保護する必要があるすべてのシナリオで、SMB 暗号化を検討する必要があります。 次のようなシナリオが想定されます。

- インフォメーション ワーカーの機密データは、SMB プロトコルを使用して移動されます。 SMB 暗号化は、Microsoft 以外のプロバイダーによって管理されているワイド エリア ネットワーク (WAN) 接続など、通過するネットワークに関係なく、ファイル サーバーとクライアントの間でのエンドツーエンドのプライバシーと整合性の保証を提供します。
- SMB 3.0 を使用すると、ファイル サーバーは SQL Server や Hyper-V などのサーバー アプリケーションに対して、継続的に使用可能な記憶域を提供できます。 SMB 暗号化を有効にすると、その情報をスヌーピング攻撃から保護する機会が得られます。 SMB 暗号化は、ほとんどの記憶域ネットワーク (SAN) に必要な専用ハードウェア ソリューションよりも簡単に使用できます。

>[!IMPORTANT]
>非暗号化による保護と比較した場合、エンドツーエンドの暗号化保護ではパフォーマンス上かなりのコストが発生することに注意してください。

## <a name="enable-smb-encryption"></a>SMB 暗号化を有効にする

SMB 暗号化は、ファイル サーバー全体に対して、または特定のファイル共有に対してのみ有効にすることができます。 SMB 暗号化を有効にするには、次のいずれかの手順を使用します。

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell を使用して SMB 暗号化を有効にする

1. 個々のファイル共有の SMB 暗号化を有効にするには、サーバーで次のスクリプトを入力します。

    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. ファイル サーバー全体で SMB 暗号化を有効にするには、サーバーで次のスクリプトを入力します。

    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. SMB 暗号化を有効にして新しい SMB ファイル共有を作成するには、次のスクリプトを入力します。

    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>サーバー マネージャーで SMB 暗号化を有効にする

1. サーバー マネージャーで、 **[ファイル サービスおよびストレージ サービス]** を開きます。
2. **[共有]** を選択して、共有管理ページを開きます。
3. SMB 暗号化を有効にする共有を右クリックし、 **[プロパティ]** を選択します。
4. 共有の **[設定]** ページで、 **[データ アクセスの暗号化]** を選択します。 この共有へのリモート ファイル アクセスが暗号化されます。

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 暗号化を展開する際の注意事項

既定では、ファイル共有またはサーバーに対して SMB 暗号化を有効にすると、SMB 3.0 クライアントのみが、指定されたファイル共有にアクセスできます。 これにより、共有にアクセスするすべてのクライアントのデータを保護するという管理者の意図が実現されます。 ただし、状況によっては、管理者は SMB 3.0 をサポートしていないクライアントに対して、暗号化されていないアクセスを許可することが必要な場合もあります (たとえば、クライアント オペレーティング システムのバージョンが混在して使用されている場合の移行期間中など)。 SMB 3.0 をサポートしていないクライアントに対して暗号化されていないアクセスを許可するには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

次のセクションで説明されている、セキュリティで保護された言語ネゴシエーション機能では、man-in-the-middle によって接続が SMB 3.0 から SMB 2.0 (暗号化されていないアクセスを使用する) にダウングレードされることを防ぎます。 ただし、SMB 1.0 へのダウングレードを防ぐことはできず、これによって暗号化されていないアクセスが発生します。 SMB 3.0 クライアントが常に SMB 暗号化を使用して、暗号化された共有にアクセスすることを保証するには、SMB 1.0 サーバーを無効にする必要があります。 (手順については、「[SMB 1.0 の無効化](#disabling-smb-10)」セクションを参照してください。) **–RejectUnencryptedAccess** 設定が既定の設定の **$true** のままになっている場合は、暗号化対応の SMB 3.0 クライアントのみがファイル共有にアクセスできます (SMB 1.0 クライアントも拒否されます)。

>[!NOTE]
>* SMB 暗号化は Advanced Encryption Standard (AES) CCM アルゴリズムを使用して、データを暗号化および復号化します。 さらに AES-CCM は SMB 署名の設定に関係なく、暗号化されたファイル共有に対してデータ整合性の検証 (署名) を行います。 暗号化せずに SMB 署名を有効にする場合は、この操作を引き続き行うことができます。 詳細については、[SMB 署名の基本](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2)に関する記事をご覧ください。
>* 組織でワイド エリア ネットワーク (WAN) アクセラレーション アプライアンスを使用している場合は、ファイル共有またはサーバーにアクセスしようとすると問題が発生することがあります。
>* 既定の構成 (暗号化されたファイル共有に対して暗号化されていないアクセスは許可されない) では、SMB 3.0 をサポートしていないクライアントが暗号化されたファイル共有にアクセスしようとすると、イベント ID 1003 が Microsoft-Windows-SmbServer/Operational イベント ログに記録され、クライアントは "**アクセスが拒否されました**" というエラー メッセージを受け取ります。
>* SMB 暗号化と NTFS ファイル システム内の暗号化ファイル システム (EFS) には関連がなく、SMB 暗号化は EFS を必要とせず、その使用に依存していません。
>* SMB 暗号化と BitLocker ドライブ暗号化は関連がなく、SMB 暗号化は BitLocker ドライブ暗号化を必要とせず、その使用に依存していません。

## <a name="secure-dialect-negotiation"></a>セキュリティで保護された言語ネゴシエーション

SMB 3.0 は、SMB 2.0 または SMB 3.0 プロトコルや、クライアントとサーバーがネゴシエートする機能のダウングレードを試みる man-in-the-middle 攻撃を検出することができます。 このような攻撃がクライアントまたはサーバーによって検出されると、接続が切断され、Microsoft-Windows-SmbServer/Operational イベント ログにイベント ID 1005 が記録されます。 セキュリティで保護された言語ネゴシエーションでは、SMB 2.0 または3.0 から SMB 1.0 へのダウングレードを検出することも防止することもできません。 このため、SMB 暗号化のすべての機能を利用するには、SMB 1.0 サーバーを無効にすることを強くお勧めします。 詳しくは、「[SMB 1.0 の無効化](#disabling-smb-10)」を参照してください。

次のセクションで説明されている、セキュリティで保護された言語ネゴシエーション機能では、man-in-the-middle によって接続が SMB 3 から SMB 2 (暗号化されていないアクセスを使用する) にダウングレードされることを防ぎます。ただし、SMB 1 へのダウングレードを防ぐことはできず、これにより暗号化されていないアクセスが発生します。 Windows 以外の以前の SMB 実装で発生する可能性のある問題の詳細については、[Microsoft サポート技術情報](https://support.microsoft.com/kb/2686098)を参照してください。

## <a name="new-signing-algorithm"></a>新しい署名アルゴリズム

SMB 3.0 では、署名のための新しい暗号化アルゴリズムである、Advanced Encryption Standard (AES) 暗号ベースのメッセージ認証コード (CMAC) を使用します。 SMB 2.0 では、古い HMAC-SHA256 暗号化アルゴリズムが使用されていました。 AES-CMAC と AES-CCM を使用すると、AES 命令をサポートするほとんどすべての最新の CPU のデータ暗号化を大幅に高速化できます。 詳細については、[SMB 署名の基本](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2)に関する記事をご覧ください。

## <a name="disabling-smb-10"></a>SMB 1.0 の無効化

SMB 1.0 の従来のコンピューター ブラウザー サービスやリモート管理プロトコルの機能は個別の機能となったため、削除することができます。 既定ではこれらの機能は引き続き有効になっていますが、以前の SMB クライアント (Windows Server 2003 や Windows XP を実行するコンピューターなど) を使用していない場合は、SMB 1.0 の機能を削除して、セキュリティを向上させ、修正プログラムの適用を減らすことができます。

>[!NOTE]
>SMB 2.0 は、Windows Server 2008 と Windows Vista で導入されました。 Windows Server 2003 または Windows XP を実行しているコンピューターなどの以前のクライアントは SMB 2.0 をサポートしていないため、SMB 1.0 サーバーが無効化されるとファイル共有や印刷共有にアクセスできなくなります。 また、Microsoft 以外の一部の SMB クライアントは、SMB 2.0 ファイル共有または印刷共有 (たとえば、"スキャンして共有する" 機能を持つプリンター) にアクセスできない場合があります。

SMB 1.0 の無効化を開始する前に、SMB 1.0 を実行しているサーバーに SMB クライアントが現在接続されているかどうかを確認する必要があります。 これを行うには、Windows PowerShell で次のコマンドレットを入力します。

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>監査証跡を構築するには、1週間にわたってこのスクリプトを (1 日に複数回) 繰り返し実行する必要があります。 これは、スケジュールされたタスクとして実行することもできます。

SMB 1.0 を無効にするには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0 を実行しているサーバーが無効になっているために SMB クライアント接続が拒否された場合は、Microsoft-Windows-SmbServer/Operational イベント ログにイベント ID 1001 が記録されます。

## <a name="more-information"></a>説明を見る

Windows Server 2012 での SMB テクノロジと関連テクノロジに関するその他の資料を以下に示します。

- [サーバー メッセージ ブロック](file-server-smb-overview.md)
- [Windows Server の記憶域](../storage.yml)
- [アプリケーション データ用のスケールアウト ファイル サーバー](../../failover-clustering/sofs-overview.md)
