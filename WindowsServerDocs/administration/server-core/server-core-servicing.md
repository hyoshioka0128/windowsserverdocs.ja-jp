---
title: Server Core への修正プログラムの適用
description: Windows Server の Server Core インストールを更新する方法について説明します。
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: eb444dd05359f033bec8b45aa9ed53a6ed5096c6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895856"
---
# <a name="patch-a-server-core-installation"></a>Server Core インストールにパッチを適用する

> 適用対象: Windows Server 2019、Windows Server 2016、および Windows Server (半期チャネル)

Server Core インストールを実行しているサーバーには、次の方法で修正プログラムを適用できます。

- **Windows Update の自動または Windows Server Update Services (WSUS) の使用**。 Windows Update を使用すると、自動またはコマンドラインツール、または Windows Server Update Services (WSUS) を使用して、Server Core インストールを実行しているサーバーにサービスを実行できます。

- **手動**。 Windows update または WSUS を使用していない組織でも、更新プログラムを手動で適用することができます。

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Server Core サーバーにインストールされている更新プログラムを表示する
Server Core に新しい更新プログラムを追加する前に、既にインストールされている更新プログラムを確認することをお勧めします。

Windows PowerShell を使用して更新プログラムを表示するには、 **get-help**を実行します。

コマンドを実行して更新プログラムを表示するには、 **systeminfo.exe**を実行します。 ツールがシステムを検査する間、しばらく時間がかかることがあります。

また、コマンドラインから**wmic qfe リスト**を実行することもできます。

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows Update で自動的に Server Core にパッチを適用する

次の手順に従って、Windows Update を使用してサーバーに自動的にパッチを適用します。

1. 現在の Windows Update 設定を確認します。
   ```
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU /v
   ```

2. 自動更新を有効にするには:

   ```
   Net stop wuauserv
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU 4
   Net start wuauserv
   ```

3. 自動更新を無効にするには、次のように実行します。

   ```
   Net stop wuauserv
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU 1
   Net start wuauserv
   ```

サーバーがドメインのメンバーである場合は、グループ ポリシーを使用して Windows Update を構成することもできます。 詳細については、「https://go.microsoft.com/fwlink/?LinkId=192470」を参照してください。 ただし、この方法を使用すると、グラフィカルインターフェイスがないため、Server Core インストールに関連するオプション 4 ("自動ダウンロードしてインストールをスケジュールする") のみが使用されます。 インストールする更新プログラムとインストールするタイミングをより詳細に制御するには、ほとんどの Windows Update グラフィカル インターフェイスと同等のコマンド ライン機能を提供するスクリプトを使用します。 スクリプトの詳細については、「」を参照してください https://go.microsoft.com/fwlink/?LinkId=192471 。

Windows Update が使用可能なすべての更新プログラムを即座に検出してインストールするように強制するには、次のコマンドを実行します。

```
Wuauclt /detectnow
```

インストールされる更新プログラムによっては、コンピューターの再起動が必要になる場合があります。ただし、これはシステムから通知されません。 インストールプロセスが完了したかどうかを判断するには、タスクマネージャーを使用して、 **wuauclt.exe**または**信頼さ**れたインストーラプロセスがアクティブに実行されていないことを確認します。 「 [Server Core サーバーにインストールされている更新プログラムを表示](#view-the-updates-installed-on-your-server-core-server)する」の方法を使用して、インストールされている更新プログラムの一覧を確認することもできます。

## <a name="patch-the-server-with-wsus"></a>WSUS を使用してサーバーに修正プログラムを適用する

Server Core サーバーがドメインのメンバーである場合は、WSUS サーバーとグループ ポリシーを使用するようにサーバーを構成できます。 詳細については、[グループポリシー参照情報](https://www.microsoft.com/download/details.aspx?id=25250)をダウンロードしてください。 また、[自動更新のグループポリシー設定の構成](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)を確認することもできます。

## <a name="patch-the-server-manually"></a>サーバーに手動で修正プログラムを適用する

更新プログラムをダウンロードし、Server Core インストールで使用できるようにします。
コマンド プロンプトで、次のコマンドを実行します。

```
Wusa <update>.msu /quiet
```

インストールされる更新プログラムによっては、コンピューターの再起動が必要になる場合があります。ただし、これはシステムから通知されません。

更新プログラムを手動でアンインストールするには、次のコマンドを実行します。

```
Wusa /uninstall <update>.msu /quiet
```

