---
title: Server Core の管理
description: Windows Server の Server Core インストールを管理する方法について説明します
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 761bfc681d7e39059884977cd99997ea9996268b
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811357"
---
# <a name="manage-a-server-core-server"></a>Server Core サーバーを管理します。
 
> 適用対象:Windows Server (半期チャネル) および Windows Server 2016

次の方法では、Server Core サーバーを管理できます。
- 使用して[Windows Admin Center](../../manage/windows-admin-center/overview.md)
- 使用して[リモート サーバー管理ツール](../../remote/remote-server-administration-tools.md)Windows 10 で実行されています。
- Windows PowerShell を使用してローカルおよびリモートで管理する
- 使用してリモート[サーバー マネージャー](../server-manager/server-manager.md)
- 使用してリモート、 [MMC スナップイン](#managing-with-microsoft-management-console)
- 使用してリモートで[リモート デスクトップ サービス](#managing-with-remote-desktop-services)

ハードウェアを追加し、コマンドラインからを実行する限り、ドライバーをローカルでの管理もことができます。

いくつかの重要な制限事項とヒントを Server Core を使用するときに注意してください。

- すべてのコマンド プロンプト ウィンドウを閉じて新しいコマンド プロンプト ウィンドウを開く場合、行うことができるタスク マネージャーから。 キーを押して**CTRL\+ALT\+削除**、 をクリックして**タスク マネージャーの起動**、 をクリックして**詳細 > ファイル > 実行**、し、入力**cmd.exe**します。 (型**Powershell.exe**を PowerShell コマンド ウィンドウを開きます)。または、サインアウトして、再びサインインすることができます。
- エクスプローラーを起動しようとするコマンドまたはツールは機能しません。 たとえば、実行している**を開始します。** コマンド プロンプトからは機能しません。
- HTML レンダリングまたは Server Core での HTML ヘルプのサポートはありません。
- Server Core は、Windows インストーラー ファイルからツールとユーティリティをインストールできるように、quiet モードで Windows インストーラーをサポートします。 Server Core での Windows インストーラー パッケージをインストールするときに使用して、 **/qb**基本的なユーザー インターフェイスを表示するにはオプションです。
- タイム ゾーンを変更するには、実行**Set-date**します。
- 国際対応の設定を変更するには、実行**control intl.cpl**します。
- **Control.exe**単独で実行しません。 いずれかで実行する必要があります**Timedate.cpl**または**Intl.cpl**します。
- **Winver.exe** Server Core では使用できません。 バージョン情報の使用を取得する**Systeminfo.exe**します。

## <a name="managing-server-core-with-windows-admin-center"></a>Server Core と Windows Admin Center を管理します。
[Windows Admin Center](../../manage/windows-admin-center/overview.md) は、Azure やクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ブラウザー ベースの管理アプリです。 Windows Admin Center では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。 Windows 10、ゲートウェイ サーバー、またはデスクトップ エクスペリエンス搭載の Windows Server のインストールは、Windows Admin Center をインストールし、管理するの Server Core システムに接続できます。

## <a name="managing-server-core-remotely-with-server-manager"></a>Server Core サーバー マネージャーをリモートで管理します。

サーバー マネージャーは、プロビジョニングおよびサーバーへの物理アクセスまたはリモート デスクトップ プロトコル (RDP) を有効にする必要のいずれかを必要とせず、デスクトップからローカルとリモートの両方の Windows ベースのサーバーを管理するのに役立つ Windows server 管理コンソール各サーバーに接続します。 サーバー マネージャーでは、リモートのマルチ サーバー管理をサポートします。

ローカル サーバーをリモート サーバーで実行されているサーバー マネージャーで管理を有効にするには、Windows PowerShell コマンドレットを実行**SMRemoting.exe – 有効にする**します。

## <a name="managing-with-microsoft-management-console"></a>Microsoft 管理コンソールで管理します。

Server Core サーバーの管理に数多くスナップインを Microsoft 管理コンソール (MMC) をリモートで使用することができます。

MMC スナップインを使用して、ドメイン メンバーである Server Core サーバーを管理します。 

1. MMC スナップインで、コンピューターの管理などを開始します。
2. スナップインを右クリックし、をクリックし、**別のコンピューターへの接続**します。
2. Server Core サーバーのコンピューター名を入力し、クリックして**OK**します。 MMC スナップインを使用して、他の PC やサーバーと同様に、Server Core サーバーを管理することができますようになりました。

MMC スナップインを使用している Server Core サーバーを管理する*いない*ドメイン メンバー。 

1. リモート コンピューターでコマンド プロンプトで次のコマンドを入力して、Server Core コンピューターへの接続に使用する代替の資格情報を設定します。
1. 
   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```

   パスワードを要求する場合は、省略、 **渡す/** オプション。

2. メッセージが表示されたら、指定したユーザー名のパスワードを入力します。
   MMC スナップインの接続に許可する Server Core サーバーのファイアウォールが構成されていない場合は MMC スナップインを許可する Windows ファイアウォールを構成する次の手順に従います。 手順 3 に進みます。
3. 別のコンピューターに MMC スナップインなど起動**コンピュータの管理**します。
4. 左側のウィンドウで、スナップインを右クリックし、クリックして**別のコンピューターへの接続**します。 (たとえば、コンピューターの管理の例では右クリックした**コンピューターの管理 (ローカル)** )。
5. **別のコンピューター**の Server Core サーバーのコンピューター名を入力し、 **OK**します。 これで、MMC スナップインを使用して、Windows Server オペレーティング システムを実行している他のコンピューターと同じように Server Core サーバーを管理できるようになります。

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>MMC スナップインの接続を許可するように Windows ファイアウォールを構成するには
すべて MMC スナップインへの接続を許可するのには、次のコマンドを実行します。

```
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

特定 MMC スナップインだけに接続できるように、次の手順を実行します。
```
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

場所*rulegroup*接続するスナップインによって、次の 1 つです。

| MMC スナップイン                            | 規則グループ                                            |
|----------------------------------------|-------------------------------------------------------|
| イベント ビューアー                           | リモート イベントのログ管理                           |
| サービス                               | リモート サービス管理                             |
| 共有フォルダー                         | ファイルとプリンターの共有                              |
| タスク スケジューラ                         | パフォーマンス ログとアラート、ファイルとプリンターの共有 |
| ディスクの管理                        | リモート ボリューム管理                              |
| Windows ファイアウォールと高度なセキュリティ | Windows ファイアウォール リモート管理                    |


> [!NOTE] 
> MMC スナップインは、ファイアウォール経由で接続するための対応するルール グループにありません。 ただし、イベント ビューアー、サービス、または共有フォルダーの規則グループを有効にすると、他のほとんどのスナップインが接続できるようになります。 
>
> さらに、スナップインの中には、次のように、Windows ファイアウォール経由で接続する前に追加の構成が必要なものがあります。
>
> - ディスクの管理 :最初に Server Core コンピューターで仮想ディスク サービス (VDS) を開始する必要があります。 また、MMC スナップインを実行しているコンピューターで、ディスク管理規則を正しく構成する必要もあります。
> - IP セキュリティ モニター :最初にこのスナップインのリモート管理を有効にする必要があります。 コマンド プロンプトで、次のように入力します**Cscript \windows\system32\scregedit.wsf/im 1。**
> - 信頼性とパフォーマンス :このスナップインは追加の構成を必要としませんが、このスナップインを使用して Server Core コンピューターを監視するときには、パフォーマンス データしか監視できません。 信頼性データは使用できません。

## <a name="managing-with-remote-desktop-services"></a>リモート デスクトップ サービスの使用を管理します。

使用することができます[リモート デスクトップ](../../remote/remote-desktop-services/welcome-to-rds.md)リモート コンピューターから Server Core サーバーを管理します。

Server Core にアクセスする前に、次のコマンドを実行する必要があります。 
```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```
これにより、管理用リモート デスクトップ モードが接続を受け入れられるようになります。

## <a name="add-hardware-and-manage-drivers-locally"></a>ハードウェアを追加し、ドライバーをローカルでの管理

ハードウェアを Server Core サーバーを追加するには、新しいハードウェアをインストールするため、ハードウェア ベンダーの指示に従います。 

ハードウェアがプラグ アンド プレイでない場合は、ドライバーを手動でインストールする必要があります。 サーバーで、一時的な場所にドライバー ファイルをコピーし、次のコマンドを実行します。

```
pnputil –i –a <driverinf>
```

場所*driverinf*ドライバーの .inf ファイルのファイルの名前です。

ダイアログが表示されたら、コンピューターを再起動します。

どのようなドライバーがインストールされているを表示するには、次のコマンドを実行します。 

```
sc query type= driver
```

> [!NOTE] 
> コマンドを正常に完了するには、等号の後にスペースを入れる必要があります。

デバイス ドライバーを無効にするには、次の手順を実行します。

```
sc delete <service_name>
```

場所*service_name*を実行したときに取得したサービスの名前を指定**sc クエリの種類 = ドライバー**します。