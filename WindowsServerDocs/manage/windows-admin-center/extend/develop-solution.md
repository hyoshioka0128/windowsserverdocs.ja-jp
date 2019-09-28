---
title: ソリューション拡張機能の開発
description: ソリューション拡張機能の開発 Windows 管理センター SDK (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ac9c6296fdf9159c9f50a1304dd345932052ac9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357147"
---
# <a name="develop-a-solution-extension"></a>ソリューション拡張機能の開発

>適用先:Windows Admin Center、Windows Admin Center Preview

ソリューションは、主に Windows 管理センターを通じて管理するオブジェクトの一意の種類を定義します。  既定では、Windows 管理センターには、次のソリューション/接続の種類が含まれています。

* Windows Server 接続
* Windows PC 接続
* フェールオーバークラスター接続
* ハイパー収束クラスター接続

Windows 管理センターの [接続] ページから接続を選択すると、その接続の種類のソリューション拡張が読み込まれ、Windows 管理センターがターゲットノードへの接続を試行します。 接続に成功すると、ソリューション拡張機能の UI が読み込まれ、Windows 管理センターの左側のナビゲーションウィンドウにそのソリューションのツールが表示されます。

上記の既定の接続の種類 (ネットワークスイッチなど) で定義されていないサービス、またはコンピューター名で検出できないその他のハードウェアの管理 GUI を構築する場合は、独自のソリューション拡張機能を作成することをお勧めします。

> [!NOTE]
> さまざまな拡張機能の種類に慣れていない場合は、 拡張[機能のアーキテクチャと拡張機能の種類](understand-extensions.md)の詳細については、こちらを参照してください。

## <a name="prepare-your-environment"></a>環境の準備

まだインストールしていない場合は、すべてのプロジェクトに必要な依存関係とグローバルな前提条件をインストールして[環境を準備](prepare-development-environment.md)します。

## <a name="create-a-new-solution-extension-with-the-windows-admin-center-cli"></a>Windows 管理センター CLI を使用して新しいソリューション拡張機能を作成する ##

すべての依存関係をインストールしたら、新しいソリューション拡張機能を作成できます。  プロジェクトファイルが格納されているフォルダーを作成または参照し、コマンドプロンプトを開き、そのフォルダーを作業ディレクトリとして設定します。  以前にインストールされた Windows 管理センター CLI を使用して、次の構文で新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso Inc``` |
| ```{!Solution Name}``` | ソリューション名 (スペースを含む) | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

これにより、ソリューションに指定した名前を使用して現在の作業ディレクトリ内に新しいフォルダーが作成され、必要なすべてのテンプレートファイルがプロジェクトにコピーされ、会社、ソリューション、およびツール名でファイルが構成されます。  

次に、作成したフォルダーにディレクトリを変更し、次のコマンドを実行して必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、Windows 管理センターに新しい拡張機能を読み込むために必要なすべての設定が完了します。 

## <a name="add-content-to-your-extension"></a>拡張機能にコンテンツを追加する

Windows 管理センター CLI を使用して拡張機能を作成したので、コンテンツをカスタマイズする準備ができました。  実行できる操作の例については、次のガイドを参照してください。

- 空の[モジュール](guides/add-module.md)を追加する
- [IFrame](guides/add-iframe.md)を追加する
- [カスタム接続プロバイダー](guides/create-connection-provider.md)を作成する
- [ルートナビゲーション動作](guides/modify-root-navigation.md)の変更
 
その他の例については、 [GITHUB SDK サイト](https://aka.ms/wacsdk)を参照してください。
-  [開発者ツール](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools)は、完全に機能する拡張機能であり、Windows 管理センターにサイドロードすることができます。また、独自の拡張機能で参照して使用できる、サンプル機能とツール例の豊富なコレクションが含まれています。

## <a name="build-and-side-load-your-extension"></a>拡張機能をビルドしてサイドロードする

次に、拡張機能をビルドして Windows 管理センターに読み込みます。  コマンドウィンドウを開き、ディレクトリをソースディレクトリに変更します。その後、ビルドする準備が整います。

* 次のように gulp build および gulp serve を指定します。

    ```
    gulp build
    gulp serve -p 4201
    ```

現在空いているポートを選択する必要があることに注意してください。 Windows Admin Center が実行されているポートは使用しないでください。

ローカルで提供されるプロジェクトを Windows Admin Center に追加することで、プロジェクトをテスト用に Windows Admin Center のローカル インスタンスにサイド ローディングすることができます。

* Web ブラウザーで Windows Admin Center を起動します
* デバッガーを起動します (F12)
* コンソールを開き、次のコマンドを入力します

    ```
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Web ブラウザーを更新します

これで、プロジェクトは、名前の横に (side loaded) が追加された状態でツール一覧に表示されるようになります。

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョンの Windows 管理センター SDK をターゲットにする

SDK の変更とプラットフォームの変更によって拡張機能を最新の状態に保つことは簡単です。  [別のバージョン](target-sdk-version.md)の Windows 管理センター SDK をターゲットにする方法については、こちらを参照してください。