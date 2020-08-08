---
title: ツール拡張機能の開発
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3bf885cd86015842be26124e7374f622d38a9c2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954128"
---
# <a name="develop-a-tool-extension"></a>ツール拡張機能の開発

>適用先:Windows Admin Center、Windows Admin Center Preview

ツール拡張機能は、ユーザーがサーバーやクラスターなどの接続を管理するために Windows 管理センターと対話する主な方法です。 Windows 管理センターのホーム画面で接続をクリックして接続すると、左側のナビゲーションウィンドウにツールの一覧が表示されます。 ツールをクリックすると、ツールの拡張機能が読み込まれ、右側のウィンドウに表示されます。

ツール拡張機能が読み込まれると、対象サーバーまたはクラスターで WMI 呼び出しまたは PowerShell スクリプトを実行し、UI に情報を表示したり、ユーザー入力に基づいてコマンドを実行したりできます。 ツールの拡張機能では、表示するソリューションを定義します。これにより、ソリューションごとに異なるツールセットが生成されます。

> [!NOTE]
> さまざまな拡張機能の種類に慣れていない場合は、 拡張[機能のアーキテクチャと拡張機能の種類](understand-extensions.md)の詳細については、こちらを参照してください。

## <a name="prepare-your-environment"></a>環境を準備する

まだインストールしていない場合は、すべてのプロジェクトに必要な依存関係とグローバルな前提条件をインストールして[環境を準備](prepare-development-environment.md)します。

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Windows 管理センター CLI を使用して新しいツール拡張機能を作成する ##

すべての依存関係をインストールしたら、新しいツール拡張機能を作成できます。  プロジェクトファイルが格納されているフォルダーを作成または参照し、コマンドプロンプトを開き、そのフォルダーを作業ディレクトリとして設定します。  以前にインストールされた Windows 管理センター CLI を使用して、次の構文で新しい拡張機能を作成します。

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

これにより、ツールで指定した名前を使用して現在の作業ディレクトリ内に新しいフォルダーが作成され、必要なすべてのテンプレートファイルがプロジェクトにコピーされ、会社名とツール名を使用してファイルが構成されます。

次に、作成したフォルダーにディレクトリを変更し、次のコマンドを実行して必要なローカルの依存関係をインストールします。

``` cmd
npm install
```

これが完了すると、Windows 管理センターに新しい拡張機能を読み込むために必要なすべての設定が完了します。

## <a name="add-content-to-your-extension"></a>拡張機能にコンテンツを追加する

Windows 管理センター CLI を使用して拡張機能を作成したので、コンテンツをカスタマイズする準備ができました。  実行できる操作の例については、次のガイドを参照してください。

- 空の[モジュール](guides/add-module.md)を追加する
- [IFrame](guides/add-iframe.md)を追加する

その他の例については、 [GITHUB SDK サイト](https://aka.ms/wacsdk)を参照してください。
-  [開発者ツール](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools)は、完全に機能する拡張機能であり、Windows 管理センターにサイドロードすることができます。また、独自の拡張機能で参照して使用できる、サンプル機能とツール例の豊富なコレクションが含まれています。

## <a name="customize-your-extensions-icon"></a>拡張機能のアイコンをカスタマイズする

ツール一覧に表示される拡張機能のアイコンをカスタマイズできます。  これを行うには、拡張機能ののすべてのエントリを変更し ```icon``` ```manifest.json``` ます。

``` json
"icon": "{!icon-uri}",
```

| 値 | 説明 | Uri の例 |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | アイコンリソースの場所 | ```assets/foo-icon.svg``` |

メモ: 現時点では、開発モードで拡張機能をサイドローディングするときに、カスタムアイコンは表示されません。  回避策として、次のようにの内容を削除し ```target``` ます。

``` json
"target": "",
```

この構成は、開発モードでサイドローディングを行う場合にのみ有効です。したがって、に含まれる値を保持して ```target``` から、拡張機能を発行する前に復元することが重要です。

## <a name="build-and-side-load-your-extension"></a>拡張機能をビルドしてサイドロードする

次に、拡張機能をビルドして Windows 管理センターに読み込みます。  コマンドウィンドウを開き、ディレクトリをソースディレクトリに変更します。その後、ビルドする準備が整います。

* 次のように gulp build および gulp serve を指定します。

    ``` cmd
    gulp build
    gulp serve -p 4201
    ```

現在空いているポートを選択する必要があることに注意してください。 Windows Admin Center が実行されているポートは使用しないでください。

ローカルで提供されるプロジェクトを Windows Admin Center に追加することで、プロジェクトをテスト用に Windows Admin Center のローカル インスタンスにサイド ローディングすることができます。

* Web ブラウザーで Windows Admin Center を起動します
* デバッガーを起動します (F12)
* コンソールを開き、次のコマンドを入力します

    ``` cmd
    MsftSme.sideLoad("http://localhost:4201")
    ```

*   Web ブラウザーを更新します

これで、プロジェクトは、名前の横に (side loaded) が追加された状態でツール一覧に表示されるようになります。

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョンの Windows 管理センター SDK をターゲットにする

SDK の変更とプラットフォームの変更によって拡張機能を最新の状態に保つことは簡単です。  [別のバージョン](target-sdk-version.md)の Windows 管理センター SDK をターゲットにする方法については、こちらを参照してください。