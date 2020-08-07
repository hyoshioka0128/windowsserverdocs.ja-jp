---
title: Server Core の管理
description: Windows Server の Server Core インストールの管理方法について説明します。
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 07/23/2019
ms.openlocfilehash: ac35d7a761547f32b0e7873ebfdd9fa77a09a1c1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895898"
---
# <a name="manage-a-server-core-server"></a>Server Core サーバーの管理
 
> 適用対象: Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Server Core サーバーは、次の方法で管理できます。
- [Windows 管理センター](../../manage/windows-admin-center/overview.md)を使用する
- Windows 10 で実行されている[リモートサーバー管理ツール](../../remote/remote-server-administration-tools.md)の使用
- Windows PowerShell を使用してローカルおよびリモートで管理する
- [サーバーマネージャー](../server-manager/server-manager.md)のリモートでの使用
- [MMC スナップ](#managing-with-microsoft-management-console)インを使用してリモートで
- リモートで[リモートデスクトップサービス](#managing-with-remote-desktop-services)

また、コマンドラインから実行する場合は、ハードウェアを追加し、ドライバーをローカルで管理することもできます。

Server Core を使用する場合は、注意すべき重要な制限事項とヒントがいくつかあります。

- すべてのコマンドプロンプトウィンドウを閉じて新しいコマンドプロンプトウィンドウを開く場合は、タスクマネージャーから実行できます。 CTRL キーを押しながら** \+ \+ del**キーを押し、[**タスクマネージャーの起動**] をクリックし、[詳細] をクリックして **> ファイル > 実行**] をクリックし、「 **cmd.exe**」と入力します。 (「 **Powershell.exe** 」と入力して、PowerShell コマンドウィンドウを開きます)。または、サインアウトしてからもう一度サインインすることもできます。
- エクスプローラーを起動しようとするコマンドまたはツールは機能しません。 たとえば、start を実行**します。** コマンドプロンプトからは機能しません。
- Server Core では、HTML 表示や HTML ヘルプはサポートされていません。
- Server Core は、Windows インストーラーファイルからツールとユーティリティをインストールできるように、quiet モードでの Windows インストーラーをサポートしています。 Server Core に Windows インストーラーパッケージをインストールする場合は、 **/qb**オプションを使用して基本的なユーザーインターフェイスを表示します。
- タイムゾーンを変更するには、[ **Set-Date**] を実行します。
- インターナショナル設定を変更するには、**コントロール intl.cpl**を実行します。
- **Control.exe**は、それ自体では実行されません。 **Timedate.cpl**または**Intl.cpl**のいずれかを使用して実行する必要があります。
- **Winver.exe**は、Server Core では使用できません。 バージョン情報を取得するには、 **Systeminfo.exe**を使用します。

## <a name="managing-server-core-with-windows-admin-center"></a>Windows 管理センターを使用した Server Core の管理
[Windows Admin Center](../../manage/windows-admin-center/overview.md) は、Azure やクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ブラウザー ベースの管理アプリです。 Windows Admin Center では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。 Windows 管理センターは、windows 10、ゲートウェイサーバー、またはデスクトップエクスペリエンスを搭載した Windows Server のインストールにインストールし、管理する Server Core システムに接続できます。

## <a name="managing-server-core-remotely-with-server-manager"></a>サーバーマネージャーを使用したリモートでの Server Core の管理

サーバーマネージャーは、Windows Server の管理コンソールです。これを使用すると、サーバーに物理的にアクセスしたり、各サーバーへのリモートデスクトッププロトコル (RDP) 接続を有効にしたりすることなく、デスクトップからローカルとリモートの両方の Windows ベースのサーバーをプロビジョニングして管理することができます。 サーバーマネージャーは、リモートのマルチサーバー管理をサポートします。

リモートサーバーで実行されているサーバーマネージャーでローカルサーバーを管理できるようにするには、Windows PowerShell コマンドレット**Configure-SMRemoting.exe-enable**を実行します。

## <a name="managing-with-microsoft-management-console"></a>Microsoft 管理コンソールを使用した管理

Microsoft 管理コンソール (MMC) の多くのスナップインをリモートで使用して、Server Core サーバーを管理できます。

MMC スナップインを使用して、ドメインメンバーである Server Core サーバーを管理するには、次のようにします。

1. [コンピューターの管理] などの MMC スナップインを起動します。
2. スナップインを右クリックし、[**別のコンピューターへ接続**] をクリックします。
2. Server Core サーバーのコンピューター名を入力し、[ **OK]** をクリックします。 これで、MMC スナップインを使用して、他の PC またはサーバーと同様に Server Core サーバーを管理できるようになりました。

MMC スナップインを使用して、ドメインメンバーでは*ない*server Core サーバーを管理するには、次のようにします。

1. リモートコンピューターのコマンドプロンプトで次のコマンドを入力して、Server Core コンピューターへの接続に使用する別の資格情報を設定します。

   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```

   パスワードの入力を求められる場合は、 **/pass**オプションを省略します。

2. プロンプトが表示されたら、指定したユーザー名のパスワードを入力します。
   Server Core サーバー上のファイアウォールがまだ MMC スナップインの接続を許可するように構成されていない場合は、次の手順に従って、MMC スナップインを許可するように Windows ファイアウォールを構成します。 その後、手順 3. に進みます。
3. 別のコンピューターで、[**コンピューターの管理**] などの MMC スナップインを起動します。
4. 左側のウィンドウでスナップインを右クリックし、[**別のコンピューターへ接続**] をクリックします。 (たとえば、コンピューターの管理の例では、[**コンピューターの管理 (ローカル)**] を右クリックします)。
5. [**別のコンピューター**] に server Core サーバーのコンピューター名を入力し、[ **OK]** をクリックします。 これで、MMC スナップインを使用して、Windows Server オペレーティング システムを実行している他のコンピューターと同じように Server Core サーバーを管理できるようになります。

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>MMC スナップインの接続を許可するように Windows ファイアウォールを構成するには
すべての MMC スナップインが接続できるようにするには、次のコマンドを実行します。

```PowerShell
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

特定の MMC スナップインだけが接続できるようにするには、次のように実行します。

```PowerShell
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

ここで、 *rulegroup*は、接続するスナップインに応じて、次のいずれかになります。

| MMC スナップイン                            | 規則グループ                                            |
| ---------------------------------------- | ------------------------------------------------------- |
| イベント ビューアー                           | リモート イベントのログ管理                           |
| サービス                               | リモート サービス管理                             |
| 共有フォルダー                         | ファイルとプリンターの共有                              |
| タスク スケジューラ                         | パフォーマンスログと警告、ファイルとプリンターの共有 |
| ディスクの管理                        | リモート ボリューム管理                              |
| Windows ファイアウォールとセキュリティ強化 | Windows ファイアウォール リモート管理                    |


> [!NOTE]
> 一部の MMC スナップインには、ファイアウォール経由での接続を許可する、対応する規則グループがありません。 ただし、イベント ビューアー、サービス、または共有フォルダーの規則グループを有効にすると、他のほとんどのスナップインが接続できるようになります。
>
> さらに、スナップインの中には、次のように、Windows ファイアウォール経由で接続する前に追加の構成が必要なものがあります。
>
> - ディスクの管理 :最初に Server Core コンピューターで仮想ディスク サービス (VDS) を開始する必要があります。 また、MMC スナップインを実行しているコンピューターで、ディスク管理規則を正しく構成する必要もあります。
> - IP セキュリティ モニター :最初にこのスナップインのリモート管理を有効にする必要があります。 これを行うには、コマンドプロンプトで「 **Cscript \windows\system32\scregedit.wsf/im 1** 」と入力します。
> - 信頼性とパフォーマンス :このスナップインは追加の構成を必要としませんが、このスナップインを使用して Server Core コンピューターを監視するときには、パフォーマンス データしか監視できません。 信頼性データは使用できません。

## <a name="managing-with-remote-desktop-services"></a>リモートデスクトップサービスを使用した管理

リモート[デスクトップ](../../remote/remote-desktop-services/welcome-to-rds.md)を使用して、リモートコンピューターから server Core サーバーを管理できます。

Server Core にアクセスするには、次のコマンドを実行する必要があります。

```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```

これにより、管理用リモート デスクトップ モードが接続を受け入れられるようになります。

## <a name="add-hardware-and-manage-drivers-locally"></a>ハードウェアを追加してドライバーをローカルに管理する

Server Core サーバーにハードウェアを追加するには、ハードウェアベンダーが新しいハードウェアをインストールするための指示に従ってください。

ハードウェアがプラグアンドプレイでない場合は、ドライバーを手動でインストールする必要があります。 これを行うには、ドライバーファイルをサーバー上の一時的な場所にコピーしてから、次のコマンドを実行します。

```
pnputil –i –a <driverinf>
```

*Driverinf:* は、ドライバーの .inf ファイルのファイル名です。

ダイアログが表示されたら、コンピューターを再起動します。

インストールされているドライバーを確認するには、次のコマンドを実行します。

```
sc query type= driver
```

> [!NOTE]
> コマンドを正常に完了するには、等号の後にスペースを入れる必要があります。

デバイスドライバーを無効にするには、次のように実行します。

```
sc delete <service_name>
```

ここで*service_name*は、 **sc query type = driver**を実行したときに入手したサービスの名前です。