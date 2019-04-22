---
title: Server Core 修正プログラムの適用
description: Windows Server の Server Core インストールを更新する方法について説明します
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: f51ffae5ed8f91cca386eb209e7a1d8cc664ceeb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817353"
---
# <a name="patch-a-server-core-installation"></a>Server Core インストールのパッチ

> 適用対象:Windows Server (半期チャネル) および Windows Server 2016

次の方法で Server Core インストールを実行するサーバーの修正プログラムを適用できます。

- **Windows Update を使用して自動的にまたは Windows Server Update Services (WSUS) と**します。 いずれかで自動的にまたはコマンド ライン ツール、または Windows Server Update Services (WSUS)、Windows Update を使用すると、Server Core インストールを実行しているサーバーをサービスできます。

- **手動**。 Windows update または WSUS を使用しない組織であっても手動で更新プログラムを適用できます。

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Server Core サーバーにインストールされている更新プログラムを表示します。
新しい更新プログラムを Server Core に追加する前に、既にインストールされている更新プログラムを表示することをお勧めを勧めします。

Windows PowerShell を使用して更新プログラムを表示するには実行**Get-hotfix**します。

コマンドを実行して更新プログラムを表示するには実行**systeminfo.exe**します。 ツールによってシステムが検査中に少し時間がかかることがあります。

実行することも**wmic qfe 一覧**コマンドラインから。 

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows Update で自動的に修正プログラムの Server Core

Windows Update で自動的にサーバーにパッチを適用するのにには、次の手順を使用します。

1. 現在の Windows Update の設定を確認します。
   ```
   %systemroot%\system32\Cscript scregedit.wsf /AU /v 
   ```

2. 自動更新を有効にします。

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 4 
   Net start wuauserv
   ```  

3. 自動更新を無効にするには、次のように実行します。

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

サーバーがドメインのメンバーである場合は、グループ ポリシーを使用して Windows Update を構成することもできます。 詳しくは、「 https://go.microsoft.com/fwlink/?LinkId=192470 」をご覧ください。 ただし、このメソッドを使用する場合、唯一のオプション 4 (「自動ダウンロードしインストール日時を指定」) は、グラフィカル インターフェイスがないのためには Server Core インストールに関連するは。 インストールする更新プログラムとインストールするタイミングをより詳細に制御するには、ほとんどの Windows Update グラフィカル インターフェイスと同等のコマンド ライン機能を提供するスクリプトを使用します。 スクリプトの詳細については、次を参照してください。 https://go.microsoft.com/fwlink/?LinkId=192471します。

Windows Update が使用可能なすべての更新プログラムを即座に検出してインストールするように強制するには、次のコマンドを実行します。

```
Wuauclt /detectnow 
```

インストールされる更新プログラムによっては、コンピューターの再起動が必要になる場合があります。ただし、これはシステムから通知されません。 インストール プロセスが完了したかどうかを判断することを確認するタスク マネージャーを使用して、 **Wuauclt**または**Trusted Installer**プロセスがアクティブに実行されていません。 内のメソッドを使用することもできます。 [、Server Core サーバーにインストールされている更新プログラムを表示](#view-the-updates-installed-on-your-Server-Core-server)にインストールされた更新プログラムの一覧を確認します。

## <a name="patch-the-server-with-wsus"></a>Wsus サーバーの修正プログラムを適用します。 

Server Core サーバーがドメインのメンバーである場合は、WSUS サーバーとグループ ポリシーを使用するようにサーバーを構成できます。 詳細については、ダウンロード、[グループ ポリシーの参照情報](https://www.microsoft.com/download/details.aspx?id=25250)します。 確認することも[自動更新のグループ ポリシー設定を構成します。](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)

## <a name="patch-the-server-manually"></a>サーバーを手動で更新プログラムします。

更新プログラムをダウンロードし、Server Core インストールに使用できるようにします。
コマンド プロンプトで次のコマンドを実行します。

```
Wusa <update>.msu /quiet 
```

インストールされる更新プログラムによっては、コンピューターの再起動が必要になる場合があります。ただし、これはシステムから通知されません。

更新プログラムを手動でアンインストールするには、次のコマンドを実行します。

```
Wusa /uninstall <update>.msu /quiet 
```

