---
title: サーバーの主要な更新プログラムの適用
description: Windows Server のサーバー コア インストールを更新する方法について説明します。
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: f51ffae5ed8f91cca386eb209e7a1d8cc664ceeb
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448113"
---
# <a name="patch-a-server-core-installation"></a>Server Core インストールを修正します。

> 対象: Windows Server (半年チャネル) および Windows Server 2016

次の方法で Server Core インストールを実行しているサーバーを修正できます。

- **自動"または"と Windows Server WSUS) を使用する Windows の更新**します。 いずれかに自動的にまたはのコマンド ライン ツール]、または Windows Server WSUS)、Windows Update を使用すると、サーバー コア インストールを実行しているサーバーをサービスことができます。

- **手動で**します。 Windows update または WSUS を使用していない組織でも更新プログラムを手動で適用することができます。

## <a name="view-the-updates-installed-on-your-server-core-server"></a>お使いのサーバーの主要なサーバーにインストールされている更新プログラムを表示します。
Server Core に新しい更新プログラムを追加する前にどのような更新プログラムが既にインストールされているかを表示することをお勧めします。

更新プログラムを表示するには、Windows PowerShell を使用して、**取り込み、修正プログラム**を実行します。

更新プログラムを表示するには、コマンドを実行して、 **systeminfo.exe**を実行します。 このツールは、システムを検査中に少し時間がかかることがあります。

コマンドラインから**wmic qfe] ボックスの一覧**を実行することもできます。 

## <a name="patch-server-core-automatically-with-windows-update"></a>Windows Update に自動的に修正プログラム Server Core

Windows Update を使用して自動的にサーバーを修正するのにには、次の手順を使用します。

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

3. 自動更新を無効にするには、次のコマンドを実行します。

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

サーバーがドメインのメンバーである場合は、グループ ポリシーを使用して、Windows の更新を構成することもできます。 詳細については、次を参照してください。https://go.microsoft.com/fwlink/?LinkId=192470します。 ただし、この方法を使用するときにだけオプション 4 (「自動ダウンロードとインストールのスケジュール」) に関連するがサーバー コア インストール グラフィカル インターフェイスがないのためです。 その他のコントロールの更新プログラムがインストールされているし、するには、Windows Update のグラフィカル インターフェイスのほとんどのコマンド ライン同等の設定を提供するスクリプトを使用することができます。 スクリプトの詳細については、次を参照してください。https://go.microsoft.com/fwlink/?LinkId=192471します。

すぐに検出して、利用可能な更新プログラムをインストールする Windows Update を強制的には、次のコマンドを実行します。

```
Wuauclt /detectnow 
```

によっては、インストールされている更新する必要があります、コンピューターを再起動するのには、システムに通知するこのしないが。 インストールのプロセスが完了するには、 **Wuauclt**または**信頼できるインストーラー**のプロセスを実際に実行されていないことを確認するのにタスク マネージャーを使用します。 インストールされている更新プログラムの一覧をチェックするのに[Server Core サーバー上の更新プログラムがインストールされているビュー](#view-the-updates-installed-on-your-Server-Core-server)でメソッドを使用することもできます。

## <a name="patch-the-server-with-wsus"></a>Wsus では、サーバーの更新プログラム 

サーバーの主要なサーバーがドメインのメンバーである場合を WSUS サーバーを使用して、グループ ポリシーを設定できます。 詳細については、[グループ ポリシーの参照情報](https://www.microsoft.com/download/details.aspx?id=25250)をダウンロードします。 [自動更新のグループ ポリシー設定の構成](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)を確認することも

## <a name="patch-the-server-manually"></a>サーバーを手動で更新プログラムします。

更新プログラムをダウンロードし、サーバー コア インストールに使用できるようにします。
コマンド プロンプトで、次のコマンドを実行します。

```
Wusa <update>.msu /quiet 
```

によっては、インストールされている更新する必要があります、コンピューターを再起動するのには、システムに通知するこのしないが。

更新プログラムを手動でアンインストールするには、次のコマンドを実行します。

```
Wusa /uninstall <update>.msu /quiet 
```

