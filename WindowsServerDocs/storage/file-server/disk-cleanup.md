---
title: Windows Server でのディスク クリーンアップの使用
description: コマンドライン オプションを使用して、特定のファイルを自動的にクリーンアップするようにディスク クリーンアップ ツール (Cleanmgr.exe) を構成する方法について説明します。
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: bb93ec15fd138ee65797c9d27413552c3a1759a6
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949669"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Windows Server でのディスク クリーンアップの使用

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ディスク クリーンアップ ツールでは、Windows Server 環境内の不要なファイルが削除されます。 このツールは、Windows server 2019 および Windows Server 2016 では既定で使用できますが、以前のバージョンの Windows Server で有効にするには、手動でいくつかの手順を実行する必要がある場合があります。

ディスク クリーンアップ ツールを起動するには、Cleanmgr.exe コマンドを実行するか、 **[開始]** を選択し、 **[Windows 管理ツール]** を選択し、 **[ディスク クリーンアップ]** を選択します。

また、[cleanmgr Windows コマンド](../../administration/windows-commands/cleanmgr.md)を使用してディスク クリーンアップを実行し、コマンドライン オプションを使用して、ディスク クリーンアップで特定のファイルをクリーンアップするように指定することもできます。

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>デスクトップ エクスペリエンスをインストールして、以前のバージョンの Windows Server でのディスク クリーンアップを有効にする

次の手順に従って、役割と機能の追加ウィザードを使用して、Windows Server 2012 R2 以前を実行するサーバーにデスクトップ エクスペリエンスをインストールすることでも、ディスク クリーンアップがインストールされます。

1. サーバー マネージャーを既に開いている場合は、次の手順に進んでください。 サーバー マネージャーをまだ開いていない場合は、次のいずれかの方法で開きます。

   - Windows デスクトップで、Windows タスク バーの **[サーバー マネージャー]** をクリックし、サーバー マネージャーを開始します。

   - **[開始]** に移動し、[サーバー マネージャー] タイルを選択します。

1. **[管理]** メニューで **[役割と機能の追加]** を選択します。

1. **[開始する前に]** ページで、対象サーバーとネットワーク環境でインストールする機能の準備が整っていることを確認してください。 **[次へ]** を選びます。

1. **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** を選択し、単一サーバーにすべてのパーツの機能をインストールします。 **[次へ]** を選びます。

1. **[対象サーバーの選択]** ページで、サーバー プールからサーバーを選択するか、オフライン VHD を選択します。 **[次へ]** を選びます。

1. **[サーバーの役割の選択]** ページで、 **[次へ]** を選択します。

1. **[機能の選択]** ページで、 **[User Interface and Infrastructure]\(ユーザー インターフェイスとインフラストラクチャ\)** を選択し、 **[デスクトップ エクスペリエンス]** を選択します。

1. **[Add features that are required for Desktop Experience?]\(デスクトップ エクスペリエンスに必要な機能を追加しますか?\)** で、 **[機能の追加]** をクリックします。

1. インストールを続行し、システムを再起動します。

1. **[ディスク クリーンアップ]** オプションのボタンが [プロパティ] ダイアログ ボックスに表示されることを確認します。

   ![ディスク プロパティ ダイアログとディスク クリーンアップ オプション](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>以前のバージョンの Windows Server にディスク クリーンアップを手動で追加する

ディスク クリーンアップ ツール (cleanmgr.exe) は、デスクトップ エクスペリエンス機能をインストールしない限り、Windows Server 2012 R2 以前上には見つけられません。

cleanmgr.exe を使用するには、前述のようにデスクトップ エクスペリエンスをインストールするか、既にサーバー、cleanmgr.exe、および cleanmgr.exe.mui 上に存在する 2 つのファイルをコピーします。 次の表を使用して、オペレーティング システムのファイルを見つけます。

| オペレーティング システム  | アーキテクチャ  | ファイルの場所  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

cleanmgr.exe を見つけて、ファイルを **%systemroot%\System32** に移動します。

cleanmgr.exe.mui を見つけて、ファイルを **%systemroot%\System32\en-US** に移動します。

これで、コマンド プロンプトから Cleanmgr.exe を実行するか、 **[開始]** をクリックし、検索バー「**Cleanmgr**」と入力して、ディスク クリーンアップ ツールを起動できるようになりました。

ディスクの [プロパティ] ダイアログに [ディスク クリーンアップ] ボタンを表示させるには、デスクトップ エクスペリエンス機能もインストールする必要があります。

## <a name="additional-references"></a>その他の参照情報

[Windows 10 のドライブの空き領域を増やす](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)」も参照してください

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
