---
title: 開発環境の準備
description: 開発環境 Windows Admin Center SDK (Project Honolulu) の準備
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b1a0672ee374f3e2d1339c43576db0e5cabdc36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834763"
---
# <a name="prepare-your-development-environment"></a>開発環境の準備

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center SDK を使用して拡張機能の開発を始めましょう。  このドキュメントでは、環境を構築し、Windows Admin Center の拡張機能をテストする稼働させるためのプロセスを説明します。

> [!NOTE]
> Windows Admin Center SDK を初めて使用する場合  [Windows Admin Center の拡張機能](extensibility-overview.md)の詳細

開発環境を準備するには、次の手順を実行します。

## <a name="install-prerequisites"></a>前提条件のインストール

SDK で開発を開始するには、次の前提条件をダウンロードしてインストールします。

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA またはプレビュー バージョン)
* Visual Studio または [Visual Studio Code](http://code.visualstudio.com)
* [Node Package Manager](https://npmjs.com/get-npm) (8.12.0 またはそれ以降)
* [Nuget](https://www.nuget.org/downloads) (拡張機能の公開用)

> [!NOTE]
> 開発者モードで Windows Admin Center をインストールして実行し、次の手順に従う必要があります。 開発者モードでは、Windows Admin Center で署名されていない拡張機能パッケージを読み込むことができます。
>
>  開発者モードを有効にするには、パラメーター DEV_MODE=1 を指定して、コマンド ラインから Windows Admin Center をインストールします。 次の例では、```<version>``` を、インストールしているバージョンに置き換えます。(```WindowsAdminCenter1809.msi``` など)。
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>グローバルの依存関係をインストールします。

次に、インストールや、ノード パッケージ マネージャーで、プロジェクトに必要な依存関係を更新します。 これらの依存関係は、グローバルにインストールされ、すべてのプロジェクトで使用可能になります。

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>以降のバージョンをインストールする@angular/cli、ただし 1.6.5 より新しいバージョンをインストールする場合、ローカルの cli バージョンがインストールされているバージョンと一致しないこと、gulp のビルド手順の中に警告が表示されることに注意します。

## <a name="next-steps"></a>次のステップ

これで、お客様の環境を準備するは、コンテンツの作成を開始する準備が完了したら。

- [ツール](develop-tool.md)の拡張機能の作成
- [ソリューション](develop-solution.md)の拡張機能の作成
- [ゲートウェイのプラグイン](develop-gateway-plugin.md)の作成
- [ガイド](guides.md)での詳細の確認

## <a name="sdk-design-toolkit"></a>SDK のデザイン ツールキット

チェック アウト、Windows Admin Center [SDK デザイン ツールキット](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)! このツールキットは、Windows Admin Center スタイル、コントロール、およびページ テンプレートを使用して PowerPoint の拡張機能を迅速に模擬テストを実行するために設計されています。 拡張機能はどのように Windows Admin Center でコーディングを開始する前に参照してください。

