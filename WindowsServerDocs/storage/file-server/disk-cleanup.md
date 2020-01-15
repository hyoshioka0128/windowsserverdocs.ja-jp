---
title: Windows Server でのディスククリーンアップの使用
description: コマンドラインオプションを使用して、特定のファイルを自動的にクリーンアップするようにディスククリーンアップツール (Cleanmgr.exe) を構成する方法について説明します。
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: bb93ec15fd138ee65797c9d27413552c3a1759a6
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949669"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Windows Server でのディスククリーンアップの使用

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ディスククリーンアップツールは、Windows Server 環境内の不要なファイルを消去します。 このツールは、Windows server 2019 および Windows Server 2016 では既定で使用できますが、以前のバージョンの Windows Server で有効にするには、手動でいくつかの手順を実行する必要がある場合があります。

ディスククリーンアップツールを起動するには、Cleanmgr.exe コマンドを実行するか、 **[スタート]** を選択して **[Windows 管理ツール]** を選択し、 **[ディスククリーンアップ]** を選択します。

また、 [Cleanmgr.exe Windows コマンド](../../administration/windows-commands/cleanmgr.md)を使用してディスククリーンアップを実行し、コマンドラインオプションを使用して、ディスククリーンアップで特定のファイルをクリーンアップするように指定することもできます。

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>デスクトップエクスペリエンスをインストールして、以前のバージョンの Windows Server でのディスククリーンアップを有効にする

役割と機能の追加ウィザードを使用して、Windows Server 2012 R2 以前を実行しているサーバーにデスクトップエクスペリエンスをインストールするには、次の手順に従います。これにより、ディスククリーンアップもインストールされます。

1. サーバー マネージャーを既に開いている場合は、次の手順に進んでください。 サーバー マネージャーをまだ開いていない場合は、次のいずれかの方法で開きます。

   - Windows デスクトップで、Windows タスク バーの **[サーバー マネージャー]** をクリックし、サーバー マネージャーを開始します。

   - **スタート** にアクセスして、サーバーマネージャー タイルを選択します。

1. **[管理]** メニューの **[役割と機能]** の追加 を選択します。

1. **[開始する前に]** ページで、インストールする機能について、移行先サーバーとネットワーク環境が準備されていることを確認します。 **[次へ]** を選びます。

1. **[インストールの種類の選択]** ページで、 **[役割ベースまたは機能ベースのインストール]** を選択して、すべてのパーツ機能を1台のサーバーにインストールします。 **[次へ]** を選びます。

1. **[対象サーバーの選択]** ページで、サーバー プールからサーバーを選択するか、オフライン VHD を選択します。 **[次へ]** を選びます。

1. **[サーバーの役割の選択]** ページで、 **[次へ]** を選択します。

1. **[機能の選択]** ページで、 **[ユーザーインターフェイスとインフラストラクチャ]** を選択し、 **[デスクトップエクスペリエンス]** を選択します。

1. **[デスクトップエクスペリエンスに必要な機能を追加しますか?]** で、 **[機能の追加]** を選択します。

1. インストールを続行し、システムを再起動します。

1. プロパティ ダイアログボックスに **ディスククリーンアップ** オプションボタンが表示されていることを確認します。

   ![ディスククリーンアップオプションを使用したディスクのプロパティダイアログ](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>以前のバージョンの Windows Server にディスククリーンアップを手動で追加する

デスクトップエクスペリエンス機能がインストールされていない場合、ディスククリーンアップツール (cleanmgr.exe) は、Windows Server 2012 R2 以前には存在しません。

Cleanmgr.exe を使用するには、前述のようにデスクトップエクスペリエンスをインストールするか、既にサーバー、cleanmgr.exe、および cleanmgr.exe に存在する2つのファイルをコピーします。 次の表を使用して、オペレーティングシステムのファイルを検索します。

| オペレーティング システム  | アーキテクチャ  | ファイルの場所  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\ amd64_microsoft-Windows-cleanmgr_31bf3856ad364e35_6 16385_none_c9392808773cd7da \cleanmgr.exe 
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\ amd64_microsoft resources_31bf3856ad364e35_6-1.7600-\cleanmgr.exe.mui. 16385_en-us_b9cb6194b257cc63 |

Cleanmgr.exe を見つけて、ファイルを場所**System32**に移動します。

**%Systemroot%\System32\en-US**を見つけて、ファイルを移動します。

コマンドプロンプトから Cleanmgr.exe を実行するか、 **[スタート]** をクリックして、検索バーに「 **cleanmgr.exe** 」と入力して、ディスククリーンアップツールを起動できるようになりました。

ディスクの [プロパティ] ダイアログに [ディスククリーンアップ] ボタンが表示されるようにするには、デスクトップエクスペリエンス機能もインストールする必要があります。

## <a name="additional-references"></a>その他の参照情報

[Windows 10 でドライブの空き容量を増やす](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
