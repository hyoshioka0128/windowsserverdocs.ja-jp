---
title: SMB セキュリティ拡張機能
description: Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 での SMB 暗号化機能の説明です。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b1586c8c63e46452075b4106c944670395734142
ms.sourcegitcommit: 21165734a0f37c4cd702c275e85c9e7c42d6b3cb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2019
ms.locfileid: "65034401"
---
# <a name="smb-security-enhancements"></a>SMB セキュリティ拡張機能

>適用対象:Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

このトピックでは、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB セキュリティ強化について説明します。

## <a name="smb-encryption"></a>SMB 暗号化

SMB 暗号化は、SMB データのエンド ツー エンドの暗号化を提供し、信頼されていないネットワークで発生する傍受からデータを保護します。 最小限の労力で SMB 暗号化を展開することができますが、特殊なハードウェアまたはソフトウェアの追加のコストが小さい必要があります。 インターネット プロトコル セキュリティ (IPsec) または WAN アクセラレータの要件はありません。 共有ごとに、または、全体のファイル サーバー用に SMB 暗号化を構成でき、さまざまなデータが信頼されていないネットワークを通過するシナリオを有効にすることができます。

>[!NOTE]
>SMB 暗号化では、通常、BitLocker ドライブ暗号化によって処理が rest でのセキュリティは含まれません。

SMB 暗号化は、中間の攻撃から保護する機密データが必要なすべてのシナリオを検討してください。 次のようなシナリオが想定されます。

- SMB プロトコルを使用して、インフォメーション ワーカーの機密データが移動されます。 SMB 暗号化は、ファイル サーバーとは、マイクロソフト以外のプロバイダーによって管理されるワイド エリア ネットワーク (WAN) 接続などの走査、ネットワークに関係なく、クライアントの間のエンド ツー エンドのプライバシーと整合性保証を提供します。
- SMB 3.0 は、SQL Server や HYPER-V などのサーバー アプリケーションの継続的に使用可能記憶域を提供するファイル サーバーを使用します。 SMB 暗号化を有効にすると、スヌーピング攻撃からその情報を保護する機会を提供します。 SMB 暗号化が使用して、ほとんどのストレージ エリア ネットワーク (San) を必要とされる専用のハードウェア ソリューションよりも簡単です。

>[!IMPORTANT]
>運用コストと比較すると、暗号化されていないと、エンド ツー エンドの暗号化保護で注目すべきパフォーマンスがあることに注意してください。

## <a name="enable-smb-encryption"></a>SMB 暗号化を有効にします。

全体のファイル サーバーや専用の特定のファイル共有に SMB 暗号化を有効にできます。 SMB 暗号化を有効にするのにには、次の手順のいずれかを使用します。

### <a name="enable-smb-encryption-with-windows-powershell"></a>Windows PowerShell を使用した SMB 暗号化を有効にします。

1. 個々 のファイル共有の SMB 暗号化を有効にするには、サーバーで、次のスクリプトを入力します。
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. ファイル サーバー全体で SMB 暗号化を有効にするには、サーバーで、次のスクリプトを入力します。
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. SMB 暗号化を有効には、新しい SMB ファイル共有を作成するには、次のスクリプトを入力します。
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>サーバー マネージャーでの SMB 暗号化を有効にします。

1. サーバー マネージャーで開きます**File and Storage Services**します。
2. 選択**共有**共有の管理ページを開きます。
3. SMB 暗号化を有効にして、選択する共有を右クリックして**プロパティ**します。
4. **設定**ページ、共有の**データ アクセスの暗号化**します。 この共有にリモート ファイル アクセスは暗号化されます。

### <a name="considerations-for-deploying-smb-encryption"></a>SMB 暗号化を展開するための考慮事項

既定でファイル共有またはサーバーの SMB 暗号化が有効になっているときに SMB 3.0 クライアントのみが指定されたファイル共有へのアクセス許可されます。 これは、共有にアクセスするすべてのクライアント、データの保護の管理者の意図を強制します。 ただし、状況によっては、管理者が (たとえば中、移行期間が混在するクライアント オペレーティング システムのバージョンが使用されている場合)、SMB 3.0 をサポートしていないクライアントに暗号化されていないアクセスを許可することがあります。 SMB 3.0 をサポートしていないクライアントの暗号化されていないアクセスを許可するには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

次のセクションで説明されているセキュリティで保護された言語のネゴシエーションの機能で中間者攻撃が SMB 3.0 から SMB 2.0 (これは暗号化されていないアクセスを使用して) への接続のダウン グレードできなくなります。 ただし、これも、ダウン グレード SMB 1.0 は、暗号化されていないアクセスにもなります。 SMB 3.0 クライアントが、暗号化された共有にアクセスする、SMB 暗号化を常に使用することを保証するには、SMB 1.0 サーバーを無効にする必要があります。 (手順については、セクションをご覧ください[SMB 1.0 の無効化](#disabling-smb-10)。)。場合、 **– RejectUnencryptedAccess**設定は既定の設定のまま **$true**、のみの暗号化に対応の SMB 3.0 クライアントがファイル共有 (SMB 1.0 クライアントは拒否も) へのアクセス許可されます。

>[!NOTE]
>* SMB 暗号化は、Advanced Encryption Standard (AES) を使用して、CCM アルゴリズムを暗号化し、データを復号化します。 AES CCM は、暗号化されたファイル共有では、SMB 署名の設定に関係なく (署名) データの整合性の検証も提供します。 SMB 暗号化を使用せずに署名を有効にする場合は、これを行うこともできます。 詳細については、次を参照してください。 [、基本の SMB 署名](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)します。
>* 組織は、ワイド エリア ネットワーク (WAN) の高速化のアプライアンスを使用している場合、ファイル共有またはサーバーにアクセスしようとしたときに問題が発生する可能性があります。
>* 既定の構成 (暗号化されたファイル共有を許可する暗号化されていないアクセスはありません)、Microsoft Windows-SmbServer/操作のイベント ログにイベント ID が 1003、暗号化されたファイル共有にアクセスしようと SMB 3.0 をサポートしていないクライアントがログインしている場合は、、クライアントは、および、**アクセスが拒否されました**エラー メッセージ。
>* SMB 暗号化と、NTFS ファイル システムで、暗号化ファイル システム (EFS) は、関連であり、SMB 暗号化が必要または EFS の使用に依存していません。
>* SMB 暗号化と BitLocker ドライブ暗号化は、関連であり、SMB 暗号化が必要または BitLocker ドライブ暗号化を使用してに依存していません。

## <a name="secure-dialect-negotiation"></a>セキュリティで保護された言語のネゴシエーション

SMB 3.0 は、SMB 2.0 または SMB 3.0 プロトコルまたはクライアントとサーバーをネゴシエートする機能をダウン グレードしようとする中間の攻撃を検出することができます。 クライアントまたはサーバーによってこのような攻撃が検出されると、接続が切断されているし、イベント ID 1005 は Microsoft Windows-SmbServer/操作イベント ログに記録されます。 言語をセキュリティで保護のネゴシエーションが検出または SMB 1.0 に SMB 2.0 または 3.0 からダウン グレードを防止することはできません。 このため、および SMB 暗号化の機能をフル活用するためには、SMB 1.0 サーバーを無効にすることを強くお勧めします。 詳細については、次を参照してください。 [SMB 1.0 を無効にすると](#disabling-smb-10)します。

次のセクションで説明されているセキュリティで保護された言語ネゴシエーションの機能は、SMB 3 から (は暗号化されていないアクセスを使用) する SMB 2; への接続のダウン グレードからで中間者攻撃を防ぐことただし、これもダウン グレードを SMB 1 は、暗号化されていないアクセスにもなります。 SMB の Windows 以外の実装前と潜在的な問題の詳細については、次を参照してください。、[マイクロソフト サポート技術情報](http://support.microsoft.com/kb/2686098)します。

## <a name="new-signing-algorithm"></a>新しい署名アルゴリズム

SMB 3.0 は、署名するためより新しい暗号化アルゴリズムを使用します。高度暗号化標準 (AES) - 暗号 - ベースのメッセージ認証コード (CMAC)。 SMB 2.0 では、古い hmac-sha256 暗号化アルゴリズムを使用します。 AES CMAC および AES CCM では、AES の命令をサポートしているほとんどの最新の Cpu でデータの暗号化を推し進めることができますが大幅にします。 詳細については、次を参照してください。 [、基本の SMB 署名](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/)します。

## <a name="disabling-smb-10"></a>SMB 1.0 を無効にします。

従来のコンピューター ブラウザー サービスと SMB 1.0 でのリモート管理プロトコルの機能は、独立したようになりましたし、取り除くことができます。 これらの機能が既定では、まだ有効になっているが、Windows Server 2003 または Windows XP を実行しているコンピューターなど、以前の SMB クライアントがあるない場合は、SMB 1.0 機能のセキュリティを強化し、修正プログラムの適用を削減する可能性がありますを削除することができます。

>[!NOTE]
>SMB 2.0 は、Windows Server 2008 および Windows Vista で導入されました。 Windows Server 2003 または Windows XP を実行しているコンピューターなど、以前のクライアントは SMB 2.0 をサポートしていませんそのため、これらはできませんをファイル共有にアクセスまたは SMB 1.0 サーバーが無効になっている場合は、共有を印刷します。 さらに、一部の Microsoft 以外の SMB クライアントが SMB 2.0 ファイルの共有にアクセスまたは共有 (たとえば、「スキャン-共有」機能を備えたプリンターなど) を印刷することできません。

SMB 1.0 を無効化を開始する前に、SMB クライアントが SMB 1.0 を実行するサーバーに現在接続されているかどうかを確認する必要があります。 これを行うには、Windows PowerShell で次のコマンドレットを入力します。

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>このスクリプトは、監査証跡を作成する曜日 (複数回毎日) の過程で繰り返し実行する必要があります。 これは、スケジュールされたタスクとしても実行できます。

SMB 1.0 を無効にするには、Windows PowerShell で次のスクリプトを入力します。

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>SMB 1.0 を実行しているサーバーが無効になっているため、SMB クライアント接続が拒否された場合、イベント ID 1001 は Microsoft Windows-SmbServer/操作イベント ログにログに記録されます。

## <a name="more-information"></a>詳細情報

SMB テクノロジと Windows Server 2012 での関連テクノロジに関する追加リソースを次に示します。

- [サーバー メッセージ ブロック](file-server-smb-overview.md)
- [Windows Server でのストレージ](../storage.md)
- [アプリケーション データ用のスケール アウト ファイル サーバー](../../failover-clustering/sofs-overview.md)