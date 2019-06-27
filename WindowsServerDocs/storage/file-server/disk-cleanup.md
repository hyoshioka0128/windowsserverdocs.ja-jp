---
title: ディスク クリーンアップを使用して、Windows server
description: コマンド ライン オプションを使用して、特定のファイルを自動的にクリーンアップするには、(Cleanmgr.exe) ディスク クリーンアップ ツールを構成する方法について説明します。
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: fbec7cd2b8312f03998cfb27b739d0866d3a47c5
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407668"
---
# <a name="using-disk-cleanup-on-windows-server"></a>ディスク クリーンアップを使用して、Windows server

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

ディスク クリーンアップ ツールは、Windows Server 環境での不要なファイルを消去します。 このツールは Windows Server 2019 および Windows Server 2016 では、既定で使用できますが、以前のバージョンの Windows Server で有効にするいくつかの手動手順を実行する必要があります。

ディスク クリーンアップ ツールを起動する Cleanmgr.exe のコマンドを実行または選択**開始**を選択します**Windows 管理ツール**、し、**ディスク クリーンアップ**します。

使用して、ディスク クリーンアップを実行することも、 [cleanmgr Windows コマンド](../../administration/windows-commands/cleanmgr.md)しコマンド ライン オプションを使用して、ディスク クリーンアップが特定のファイルをクリーンアップするかを指定します。

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>デスクトップ エクスペリエンスをインストールすることで、Windows Server の以前のバージョンでディスク クリーンアップを有効にします。

追加の役割と機能のウィザードを使用して、Windows Server 2012 R2 を実行するサーバーにデスクトップ エクスペリエンスをインストールする次の手順またはディスク クリーンアップもインストールする前にします。

1. サーバー マネージャーを既に開いている場合は、次の手順に進んでください。 サーバー マネージャーをまだ開いていない場合は、次のいずれかの方法で開きます。

   - Windows デスクトップで、Windows タスク バーの **[サーバー マネージャー]** をクリックし、サーバー マネージャーを開始します。

   - 移動して**開始**サーバー マネージャー タイルを選択します。

1. **管理** メニューの 追加 を選択**役割と機能の**します。

1. **開始する前に** ページで、インストールする機能、移行先サーバーとネットワーク環境を準備したことを確認します。 **[次へ]** を選びます。

1. **インストールの種類を選択します。** ] ページで [**役割ベースまたは機能ベースのインストール**部分のすべての機能を 1 台のサーバーにインストールします。 **[次へ]** を選びます。

1. **[対象サーバーの選択]** ページで、サーバー プールからサーバーを選択するか、オフライン VHD を選択します。 **[次へ]** を選びます。

1. **サーバーの役割の選択**ページで、選択**次**します。

1. **機能の選択** ページで **ユーザー インターフェイスとインフラストラクチャ**、し、**デスクトップ エクスペリエンス**します。

1. **デスクトップ エクスペリエンスに必要な機能を追加しますか?** を選択します**機能の追加**します。

1. インストールを続行し、システムを再起動します。

1. いることを確認、**ディスク クリーンアップ**オプション ボタン、[プロパティ] ダイアログ ボックスに表示されます。

   ![ディスクのディスク クリーンアップのオプションのプロパティ ダイアログ ボックス](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>ディスク クリーンアップを Windows Server の以前のバージョンを手動で追加します。

ディスク クリーンアップ ツール (cleanmgr.exe) が存在しない Windows Server 2012 R2 またはそれ以前インストールされているデスクトップ エクスペリエンス機能がない限り、します。

Cleanmgr.exe を使用するには、前述したとおり、デスクトップ エクスペリエンスをインストールまたは server や cleanmgr.exe cleanmgr.exe.mui にすでに存在する 2 つのファイルをコピーします。 次の表を使用して、オペレーティング システムのファイルを探します。

| オペレーティング システム  | Architecture  | ファイルの場所  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64 ビット | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Cleanmgr.exe を見つけて、ファイルの移動 **%systemroot%\System32**します。

Cleanmgr.exe.mui を見つけて、ファイルの移動 **%systemroot%\System32\en-US**します。

コマンド プロンプトから、Cleanmgr.exe を実行するかをクリックしてディスクのクリーンアップ ツールを今すぐ起動**開始**」と入力**Cleanmgr**検索バーにします。

ディスクのプロパティ ダイアログ ボックスに表示されるディスク クリーンアップ ボタンには、デスクトップ エクスペリエンス機能をインストールする必要があります。

## <a name="additional-references"></a>その他の参照情報

[Windows 10 のドライブの領域を解放します。](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
