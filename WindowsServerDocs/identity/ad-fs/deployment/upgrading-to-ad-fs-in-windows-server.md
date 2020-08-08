---
ms.assetid: 7671e0c9-faf0-40de-808a-62f54645f891
title: Windows Server 2016 での AD FS へのアップグレード
author: billmath
manager: femila
ms.date: 04/09/2018
ms.topic: article
ms.author: billmath
ms.openlocfilehash: cf8a12957621ce86492cc4216c56d9a159f1ee5c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940568"
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-using-a-wid-database"></a>WID データベースを使用した、Windows Server 2016 での AD FS へのアップグレード


> [!NOTE]
> 完了のために計画された明確な時間枠でアップグレードを開始するだけです。 混合モードで AD FS を維持すると、ファームで問題が発生する可能性があるため、長時間にわたって混在モードの状態で AD FS を維持することはお勧めしません。

## <a name="upgrading-a-windows-server-2012-r2-or-2016-ad-fs-farm-to-windows-server-2019"></a>Windows Server 2012 R2 または 2016 AD FS ファームから Windows Server 2019 へのアップグレード
次のドキュメントでは、WID データベースを使用している場合に、Windows Server 2019 の AD FS に AD FS ファームをアップグレードする方法について説明します。

### <a name="ad-fs-farm-behavior-levels-fbl"></a>AD FS ファームの動作レベル (FBL)
Windows Server 2016 の AD FS では、ファームの動作レベル (FBL) が導入されました。 これはファーム全体の設定であり、AD FS ファームで使用できる機能を決定します。

次の表に、Windows Server バージョン別の FBL 値の一覧を示します。

| Windows Server のバージョン  | FBL | AD FS 構成データベース名 |
| ------------- | ------------- | ------------- |
| 2012 R2  | 1  | AdfsConfiguration |
| 2016  | 3  | AdfsConfigurationV3 |
| 2019  | 4  | AdfsConfigurationV4 |

> [!NOTE]
> FBL をアップグレードすると、新しい AD FS 構成データベースが作成されます。  各 Windows Server AD FS バージョンおよび FBL 値の構成データベースの名前については、上記の表を参照してください。

### <a name="new-vs-upgraded-farms"></a>新しい vs のアップグレードされたファーム
既定では、新しい AD FS ファームの FBL は、インストールされている最初のファームノードの Windows Server バージョンの値と一致します。

新しいバージョンの AD FS サーバーを AD FS 2012 R2 または2016ファームに参加させることができ、ファームは既存のノードと同じ FBL で動作します。 同じファーム内で、最低バージョンの FBL 値で複数の Windows Server バージョンが動作している場合、ファームは "mixed" と呼ばれます。 ただし、FBL が発生するまで、以降のバージョンの機能を利用することはできません。 ファームが混在している場合:

- 管理者は、新しい Windows Server 2019 フェデレーションサーバーを既存の Windows Server 2012 R2 または2016ファームに追加できます。 その結果、ファームは "混在モード" になり、元のファームと同じファーム動作レベルで動作します。 ファーム全体での動作の一貫性を確保するために、新しいバージョンの Windows Server AD FS の機能を構成または使用することはできません。

- FBL を発生させる前に、管理者はファームから以前のバージョンの Windows Server の AD FS ノードを削除する必要があります。  WID ファームの場合は、ファーム内のプライマリノードの役割に昇格させる新しい Windows Server 2019 フェデレーションサーバーの1つが必要であることに注意してください。

- ファーム内のすべてのフェデレーションサーバーが同じ Windows Server バージョンになると、FBL が発生する可能性があります。  その結果、新しい AD FS Windows Server 2019 の機能を構成して使用できるようになります。

ファームモードが混在している場合、AD FS ファームは、Windows Server 2019 の AD FS で導入された新しい機能には対応していないことに注意してください。 これは、新しい機能を試す必要がある組織は、FBL が発生するまでこれを行うことができないことを意味します。 そのため、お客様の組織が FBL を導入する前に新しい機能をテストすることを検討している場合は、別のファームをデプロイしてこれを行う必要があります。

このドキュメントの残りの部分では、windows server 2019 フェデレーションサーバーを windows server 2016 または 2012 R2 環境に追加し、Windows Server 2019 に FBL を発生させる手順について説明します。 これらの手順は、以下のアーキテクチャ図に示されているテスト環境で実行されました。

> [!NOTE]
> Windows Server 2019 FBL の AD FS に移行する前に、Windows Server 2016 または 2012 R2 のすべてのノードを削除する必要があります。 Windows Server 2016 または 2012 R2 OS を Windows Server 2019 にアップグレードするだけで、それが2019ノードになるようにすることはできません。 これを削除し、新しい2019ノードに置き換える必要があります。

> [!NOTE]
> AlwaysOnAvailability グループまたはマージレプリケーションが AD FS で構成されている場合は、アップグレードの前にすべての ADFS データベースのすべてのレプリケーションを削除し、すべてのノードがプライマリ SQL データベースをポイントするようにします。 これを実行した後、ドキュメントに従ってファームのアップグレードを実行します。 アップグレード後、AlwaysOnAvailability グループまたはマージレプリケーションを新しいデータベースに追加します。

##### <a name="to-upgrade-your-ad-fs-farm-to-windows-server-2019-farm-behavior-level"></a>AD FS ファームを Windows Server 2019 ファームの動作レベルにアップグレードするには

1. サーバーマネージャーを使用して、Windows Server 2019 に Active Directory フェデレーションサービス (AD FS) の役割をインストールします。

2. AD FS 構成ウィザードを使用して、新しい Windows Server 2019 サーバーを既存の AD FS ファームに参加させます。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_1.png)

3. Windows Server 2019 フェデレーションサーバーで、AD FS 管理を開きます。 このフェデレーションサーバーはプライマリサーバーではないため、管理機能を使用できないことに注意してください。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_3.png)

4. Windows Server 2019 サーバーで、管理者特権の PowerShell コマンドウィンドウを開き、次のコマンドレットを実行します。

```PowerShell
Set-AdfsSyncProperties -Role PrimaryComputer
```

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_4.png)

5. 以前にプライマリとして構成されていた AD FS サーバーで、管理者特権の PowerShell コマンドウィンドウを開き、次のコマンドレットを実行します。

```PowerShell
Set-AdfsSyncProperties -Role SecondaryComputer -PrimaryComputerName {FQDN}
```

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_5.png)

6. 次に、Windows Server 2016 フェデレーションサーバーで AD FS 管理を開きます。 プライマリロールがこのサーバーに転送されているため、すべての管理機能が表示されるようになりました。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_6.png)

7. AD FS 2012 R2 ファームを2016または2019にアップグレードする場合、ファームのアップグレードでは、AD スキーマが少なくともレベル85である必要があります。  スキーマをアップグレードするには、Windows Server 2016 のインストールメディアを使用してコマンドプロンプトを開き、support\adprep ディレクトリに移動します。 次のコマンドを実行します: `adprep /forestprep`

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_7.png)

実行が完了したら`adprep/domainprep`

> [!NOTE]
> 次の手順を実行する前に、[設定] から Windows Update を実行して、Windows Server が最新であることを確認します。 更新の必要がなくなるまで、このプロセスを続けます。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_8.png)

8. Windows Server 2016 サーバーで PowerShell を開き、次のコマンドレットを実行します。


> [!NOTE]
> 次の手順を実行する前に、すべての 2012 R2 サーバーをファームから削除する必要があります。

```PowerShell
Invoke-AdfsFarmBehaviorLevelRaise
```

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_9.png)

9. プロンプトが表示されたら、「Y」と入力します。これにより、レベルの引き上げが開始されます。 これが完了すると、FBL が正常に発生しました。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_10.png)

10. ここで、[AD FS の管理] にアクセスすると、新しい機能が追加された AD FS バージョンが表示されます。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_12.png)

11. 同様に、PowerShell コマンドレットを使用して、 `Get-AdfsFarmInformation` 現在の FBL を表示できます。

![upgrade](media/Upgrading-to-AD-FS-in-Windows-Server-2016/ADFS_Mixed_13.png)

12. WAP サーバーを最新レベルにアップグレードするには、各 Web アプリケーションプロキシで、管理者特権のウィンドウで次の PowerShell コマンドレットを実行して、WAP を再構成します。

```PowerShell
$trustcred = Get-Credential -Message "Enter Domain Administrator credentials"
Install-WebApplicationProxy -CertificateThumbprint {SSLCert} -fsname fsname -FederationServiceTrustCredential $trustcred
```

クラスターから古いサーバーを削除し、次の Powershell コマンドレットを実行して、上記で再構成された最新のサーバーバージョンを実行している WAP サーバーのみを保持します。

```PowerShell
Set-WebApplicationProxyConfiguration -ConnectedServersName WAPServerName1, WAPServerName2
```

Get WebApplicationProxyConfiguration コマンドレットを実行して、WAP の構成を確認します。 ConnectedServersName には、前のコマンドからのサーバー実行が反映されます。

```PowerShell
Get-WebApplicationProxyConfiguration
```
> [!NOTE]
> ConfigurationVersion が Windows Server 2016 の場合は、次の手順をスキップします。 これは、Windows Server 2016/2019 の Web アプリケーションプロキシの正しい値です。

WAP サーバーの ConfigurationVersion をアップグレードするには、次の Powershell コマンドを実行します。

```PowerShell
Set-WebApplicationProxyConfiguration -UpgradeConfigurationVersion
```

これにより、WAP サーバーのアップグレードが完了します。


> [!NOTE]
> ハイブリッド証明書信頼を使用する Windows Hello for Business が実行されている場合、AD FS 2019 には既知の PRT の問題が存在します。 ADFS 管理者イベント ログで、次のエラーが発生することがあります。Received invalid Oauth request. \(無効な Oauth 要求を受信しました。\) The client 'NAME' is forbidden to access the resource with scope 'ugs'. \(クライアント 'NAME' はスコープ 'ugs' のリソースにアクセスすることが許可されていません。\)
> このエラーを修復するには、次のようにします。
> 1. AD FS 管理コンソールを起動します。 [Services]\(サービス\) > [Scope Descriptions]\(スコープ記述\) を参照します
> 2. [Scope Descriptions]\(スコープ記述\) を右クリックし、[Add Scope Description]\(スコープ記述の追加\) を選択します
> 3. 名前に「ugs」と入力し、[適用] > [OK] をクリックします
> 4. 管理者として PowerShell を起動します
> 5. コマンド "Get-AdfsApplicationPermission" を実行します。 ClientRoleIdentifier を含む ScopeNames :{openid, aza} を探します。 ObjectIdentifier をメモしておきます。
> 6. コマンド "Set-AdfsApplicationPermission -TargetIdentifier <手順 5 の ObjectIdentifier> -AddScope 'ugs' を実行します
> 7. ADFS サービスを再起動します。
> 8. クライアント側:クライアントを再起動します。 ユーザーは WHFB をプロビジョニングするように求められます。
> 9. プロビジョニング ウィンドウがポップアップ表示されない場合は、NGC トレース ログを収集し、さらにトラブルシューティングを行う必要があります。
