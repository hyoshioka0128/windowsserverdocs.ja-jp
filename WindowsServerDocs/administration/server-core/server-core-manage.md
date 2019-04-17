---
title: Server Core を管理します。
description: Windows Server のサーバー コア インストールを管理する方法を学習します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 6836e5db36727294d215f7f98e0faeede55a612a
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718712"
---
# <a name="manage-a-server-core-server"></a>サーバーの主要なサーバーを管理します。
 
> 対象: Windows Server (半年チャネル) および Windows Server 2016

Server Core サーバーは、次の方法で管理できます。
- [Windows 管理センター](../../manage/windows-admin-center/overview.md)を使用します。
- Windows 10 で実行されている[リモート サーバー管理ツール](../../remote/remote-server-administration-tools.md)を使用します。
- ローカルとリモートでは、Windows PowerShell を使用します。
- リモート[サーバー マネージャー](../server-manager/server-manager.md)を使用します。
- リモートの使用を[スナップイン](#managing-with-microsoft-management-console)
- [リモート デスクトップ サービス](#managing-with-remote-desktop-services)をリモートで

ハードウェアを追加し、コマンドラインから操作するとローカルでのドライバーを管理することもします。

いくつかの重要な制限と Server Core を操作する際に注意するヒントがあります。

- すべてのコマンド プロンプト ウィンドウを閉じますして新しいコマンド プロンプト ウィンドウを開く、できることをタスク マネージャー] からします。 **CTRL\ と ALT\ キーを押しながら DEL**キーを押して、[**タスク マネージャーを開始する**] をクリックして] をクリックして**詳細 > ファイル > 実行**、し**cmd.exe**を入力します。 (PowerShell コマンド ウィンドウを開くには、 **Powershell.exe**を入力します)。または、後、再びサインインしてサインインすることができます。
- すべてのコマンドまたは Windows エクスプ ローラーを起動しようとするツールは使用できません。 たとえば、実行されている**を開始します**。 コマンド プロンプトでは動作しません。
- HTML レンダリングまたは Server Core の HTML ヘルプのサポートはありません。
- Server Core では、非表示モードで Windows インストーラーがサポートされているため、Windows インストーラー ファイルからのツールとユーティリティをインストールすることができます。 サーバーのコアの Windows インストーラー パッケージをインストールする場合は、基本的なユーザー インターフェイスを表示する **/qb**オプションを使用します。
- タイムゾーンを変更するには、**設定する日付**を実行します。
- 地域の設定を変更するには、**コントロール intl.cpl**を実行します。
- **Control.exe**単独で実行しません。 **Timedate.cpl**または**Intl.cpl**のいずれかを実行する必要があります。
- **Winver.exe**では、サーバー コアで使用できません。 取得するのには、バージョン情報は、 **Systeminfo.exe**を使用します。

## <a name="managing-server-core-with-windows-admin-center"></a>管理センターの Windows Server Core を管理します。
[管理センターの Windows](../../manage/windows-admin-center/overview.md) Azure またはクラウドの依存はせずに、Windows のサーバーの内部設置型の管理を有効にするブラウザー ベースの管理アプリには Windows 管理センターでは、サーバー インフラストラクチャのあらゆる要素に対するフル コントロールと、インターネットに接続されていないプライベート ネットワーク上の管理に便利です。 Windows 10、ゲートウェイ サーバー、またはデスクトップ環境では、Windows Server のインストール、管理センターの Windows をインストールし、管理する Server Core システムに接続できます。

## <a name="managing-server-core-remotely-with-server-manager"></a>Server Core サーバー マネージャーでリモートで管理します。

サーバー マネージャーはプロビジョニングや、サーバーへのアクセスを物理またはリモート デスクトップ プロトコル (RDP) を有効にする必要があるのいずれかを必要とせず、デスクトップからローカルおよびリモートの Windows ベースのサーバーを管理するために役立つ Windows Server で管理コンソール各サーバーに接続します。 サーバー マネージャーは、リモートで複数のサーバー管理をサポートしています。

リモート サーバーで実行されているサーバー マネージャーで管理するローカル サーバーを有効にするには、Windows PowerShell コマンドレットを実行**構成 SMRemoting.exe – を有効にする**します。

## <a name="managing-with-microsoft-management-console"></a>Microsoft 管理コンソールで管理します。

リモートでサーバー コア サーバーの管理に多くスナップイン Microsoft 管理コンソール (MMC) を使用できます。

MMC スナップインを使用して、ドメインのメンバーである Server Core サーバーを管理します。 

1. スナップイン、コンピューターの管理などを起動します。
2. スナップインで右クリックし、**別のコンピューターに接続**] をクリックします。
2. Server Core サーバーのコンピューター名を入力し、[ **OK**] をクリックします。 その他の任意の PC やサーバーどおり Server Core サーバーを管理するのに MMC スナップインで使用できます。

MMC スナップインを使って Server Core サーバーを管理するには*ない*ドメイン メンバー。 

1. 使用してリモート コンピューター上のコマンド プロンプトで、次のコマンドを入力し、Server Core コンピューターに接続する別の資格情報を確立します。
   ```
   cmdkey /add:<ServerName> /user:<UserName> /pass:<password>
   ```
   パスワードを要求する場合は、**** 渡す/オプションを省略します。

2. メッセージが表示されたら、指定したユーザー名に使用するパスワードを入力します。
   MMC スナップインの接続を許可する、サーバーの主要なサーバー上のファイアウォールが構成されていない場合は、Windows ファイアウォール スナップインを構成するのには、次の手順に従います。 手順 3 に進みます。
3. 別のコンピューターで、スナップイン、**コンピューターの管理**などを起動します。
4. 左側のウィンドウで、スナップインを右クリックし、**別のコンピューターに接続**] をクリックします。 (たとえば、例では、コンピューターの管理、すると右クリック**コンピューターの管理 (ローカル)**)。
5. **別のコンピューター**のでは、Server Core サーバーのコンピューター名を入力し、[ **OK**] をクリックします。 Windows Server オペレーティング システムを実行して、他のコンピューターと同じように、サーバーの主要なサーバーを管理するのに MMC スナップインで使用できます。

### <a name="to-configure-windows-firewall-to-allow-mmc-snap-ins-to-connect"></a>MMC スナップ (s) への接続を許可する Windows ファイアウォールを構成するには
すべて MMC スナップインの接続を許可するには、次のコマンドを実行します。

```
Enable-NetFirewallRule -DisplayGroup "Remote Administration"
```

のみ特定 MMC スナップインの接続を許可するには、次の手順を実行します。
```
Enable-NetFirewallRule -DisplayGroup "<rulegroup>"
```

*Rulegroup*が接続するスナップインに応じて、次のいずれか。

| スナップイン                            | ルール グループ                                            |
|----------------------------------------|-------------------------------------------------------|
| イベント ビューアー                           | リモートのイベント ログの管理                           |
| サービス                               | リモート サービスの管理                             |
| 共有フォルダー                         | ファイルとプリンターの共有                              |
| タスク スケジューラ                         | パフォーマンスのログ、通知、ファイルとプリンターの共有 |
| ディスクの管理                        | リモート ボリューム管理                              |
| Windows ファイアウォールと高度なセキュリティ | Windows ファイアウォールのリモート管理                    |


> [!NOTE] 
> MMC スナップインは、対応するルール グループ ファイアウォール経由で接続する必要がありません。 ただし、イベント ビューアー、サービス、または共有フォルダーのルールのグループを有効にすると、その他のほとんどスナップインに接続することができます。 
>
> さらに、特定のスナップイン構成する必要前に、Windows ファイアウォール経由で接続することができます。
>
> - ディスクの管理します。 Server Core コンピューターに仮想ディスク サービス (VDS) を初めて起動する必要があります。 MMC スナップインを実行しているコンピューターで適切にディスクの管理のルールを構成する必要がありますもします。
> - IP セキュリティ モニターします。 まず、このスナップインのリモート管理を有効にする必要があります。 コマンド プロンプトで、これには、入力**コマンド \windows\system32\scregedit.wsf/im 1**
> - 信頼性、パフォーマンスします。 スナップインは必要ありませんその他の構成が Server Core コンピューターを監視することを使用する場合は、パフォーマンス データをのみ監視することができます。 信頼性データは使用できません。

## <a name="managing-with-remote-desktop-services"></a>リモート デスクトップ サービスを管理します。

[Remote Desktop](../../remote/remote-desktop-services/welcome-to-rds.md)を使用して、リモート コンピューターから Server Core サーバーを管理することができます。

サーバー コア、アクセスするには、次のコマンドを実行する必要があります。 
```
cscript C:\Windows\System32\Scregedit.wsf /ar 0
```
これにより、管理モードのリモート デスクトップ接続を受け入れるようになります。

## <a name="add-hardware-and-manage-drivers-locally"></a>ハードウェアを追加し、[ローカルのドライバーを管理します。

ハードウェアをサーバーの主要なサーバーに追加するには、新しいハードウェアをインストールする場合のハードウェア製造元が提供する指示に従います。 

ハードウェアがプラグと再生でない場合は、ドライバーを手動でインストールする必要があります。 そのためは、サーバー上の一時的な場所にドライバー ファイルをコピーし、次のコマンドを実行します。
```
pnputil –i –a <driverinf>
```
*Driverinf*がドライバーの .inf ファイルのファイルの名前です。

メッセージが表示されたら、コンピューターを再起動します。

どのようなドライバーがインストールされているを表示するには、次のコマンドを実行します。 
```
sc query type= driver
```

> [!NOTE] 
> 正常に完了するためのコマンドの等号の後にスペースを含める必要があります。

デバイス ドライバーを無効にするには、次の手順を実行します。 
```
sc delete <service_name>
```

*サービス名*は、サービスの実行時に取得した名前**sc クエリの種類のドライバーを =** します。