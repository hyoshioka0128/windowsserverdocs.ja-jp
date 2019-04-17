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
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080919"
---
# 開発環境の準備

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center SDK を使用して拡張機能の開発を始めましょう。  このドキュメントで、環境とを構築して Windows Admin Center の拡張機能のテストを実行しているを取得するプロセスについて説明します。

> [!NOTE]
> Windows Admin Center SDK を初めて使用する場合  [Windows Admin Center の拡張機能](extensibility-overview.md)の詳細

開発環境を準備するには、次の手順を実行します。

## 前提条件のインストール

SDK で開発を開始するには、次の前提条件をダウンロードしてインストールします。

* [Windows Admin Center](https://aka.ms/WACDownloadPage)(GA またはプレビュー版)
* Visual Studio または [Visual Studio Code](http://code.visualstudio.com)
* [Node Package Manager](https://npmjs.com/get-npm)(8.12.0 またはそれ以降)
* [Nuget](https://www.nuget.org/downloads) (拡張機能の公開用)

> [!NOTE]
> 開発者モードで Windows Admin Center をインストールして実行し、次の手順に従う必要があります。 開発者モードでは、Windows Admin Center で署名されていない拡張機能パッケージを読み込むことができます。
>
>  開発者モードを有効にするには、パラメーター DEV_MODE=1 を指定して、コマンド ラインから Windows Admin Center をインストールします。 次の例では、```<version>``` を、インストールしているバージョンに置き換えます。(```WindowsAdminCenter1809.msi``` など)。
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## グローバルな依存関係をインストールします。

次に、インストールまたは Node Package Manager で、プロジェクトに必要な依存関係を更新します。 これらの依存関係は、グローバルにインストールされ、すべてのプロジェクトで使用可能になります。

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>@Angular/cli のそれ以降のバージョンをインストール、ただし 1.6.5 より新しいバージョンをインストールする場合、ローカル cli バージョンがインストールされているバージョンを一致しない gulp ビルド手順中に警告が表示されることに注意することができます。

## 次のステップ

これで、環境を準備しているコンテンツの作成を開始する準備がします。

- [ツール](develop-tool.md)の拡張機能の作成
- [ソリューション](develop-solution.md)の拡張機能の作成
- [ゲートウェイのプラグイン](develop-gateway-plugin.md)の作成
- [ガイド](guides.md)での詳細の確認

## SDK の設計ツールキット

この Windows Admin Center [SDK の設計ツールキット](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)を確認してください。 このツールキットは、Windows Admin Center スタイル、コントロール、およびページ テンプレートを使用して PowerPoint で拡張機能を迅速にモック作成するために設計されています。 拡張機能がどのように Windows Admin Center でコーディングを開始する前に参照してください。

