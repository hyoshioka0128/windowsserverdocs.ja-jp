---
title: 開発環境を準備する
description: 開発環境 Windows Admin Center SDK (Project Honolulu) の準備
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.openlocfilehash: 09d39aa027adf360c339da434b16038a3b8e5c90
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964598"
---
# <a name="prepare-your-development-environment"></a>開発環境を準備する

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センター SDK を使用して拡張機能の開発を開始しましょう。  このドキュメントでは、Windows 管理センターの拡張機能をビルドしてテストするために、環境を稼働させるためのプロセスについて説明します。

> [!NOTE]
> Windows Admin Center SDK を初めて使用する場合  [Windows Admin Center の拡張機能](extensibility-overview.md)の詳細

開発環境を準備するには、次の手順を実行します。

## <a name="install-prerequisites"></a>必須コンポーネントをインストールする

SDK で開発を開始するには、次の前提条件をダウンロードしてインストールします。

* [Windows 管理センター](https://aka.ms/WACDownloadPage) (GA またはプレビューバージョン)
* Visual Studio または [Visual Studio Code](https://code.visualstudio.com)
* [Node.js](https://nodejs.org/en/download/releases/) (バージョン 10.3.0)
* [ノードパッケージマネージャー](https://npmjs.com/get-npm) (8.12.0 以降)
* [Nuget](https://www.nuget.org/downloads) (拡張機能の公開用)

> [!NOTE]
> 開発者モードで Windows Admin Center をインストールして実行し、次の手順に従う必要があります。 開発者モードでは、Windows Admin Center で署名されていない拡張機能パッケージを読み込むことができます。 Windows 管理センターは、Windows 10 コンピューターの開発モードでのみインストールできます。
>
>  開発者モードを有効にするには、パラメーター DEV_MODE=1 を指定して、コマンド ラインから Windows Admin Center をインストールします。 次の例では、```<version>``` を、インストールしているバージョンに置き換えます。(```WindowsAdminCenter1809.msi``` など)。
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>グローバル依存関係のインストール

次に、ノードパッケージマネージャーを使用して、プロジェクトに必要な依存関係をインストールまたは更新します。 これらの依存関係は、グローバルにインストールされ、すべてのプロジェクトで使用可能になります。

```
npm install -g npm

npm install -g @angular/cli@7.1.2

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>新しいバージョンのをインストールすることはできますが @angular/cli 、7.1.2 よりも大きいバージョンをインストールすると、gulp のビルド手順で、ローカル cli のバージョンがインストールされているバージョンと一致しないという警告が表示されます。

## <a name="next-steps"></a>次のステップ

環境が準備できたので、コンテンツの作成を開始する準備ができました。

- [ツール](develop-tool.md)の拡張機能の作成
- [ソリューション](develop-solution.md)の拡張機能の作成
- [ゲートウェイのプラグイン](develop-gateway-plugin.md)の作成
- [ガイド](guides.md)での詳細の確認

## <a name="sdk-design-toolkit"></a>SDK design toolkit

Windows 管理センター [SDK design toolkit](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)をご覧ください。 このツールキットは、Windows 管理センターのスタイル、コントロール、およびページテンプレートを使用して、PowerPoint の拡張機能を迅速にモックアップできるように設計されています。 コーディングを開始する前に、Windows 管理センターで拡張機能がどのように表示されるかを確認してください。

