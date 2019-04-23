---
title: ツール拡張機能の開発
description: 開発ツールの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 092a97c1166f1090dd7c556f1ab86d42a1f46ee4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889273"
---
# <a name="develop-a-tool-extension"></a>ツール拡張機能の開発

>適用先:Windows Admin Center、Windows Admin Center プレビュー

ツールの拡張機能は、サーバーまたはクラスターなどの接続を管理する Windows Admin Center でユーザーが操作する主な方法です。 Windows Admin Center のホーム画面での接続 をクリックし、接続するととき、に、左側のナビゲーション ウィンドウでツールの一覧が表示し、されます。 ツールをクリックすると、ツールの拡張機能が読み込まれ、右側のウィンドウに表示されます。

ツールの拡張機能が読み込まれるときに対象サーバーまたはクラスター上の WMI 呼び出しまたは PowerShell スクリプトを実行する UI に情報を表示し、ユーザー入力に基づいてコマンドを実行もできます。 ツールの拡張は、それが表示、各ソリューション用のツールのさまざまなセットを生成するソリューションを定義します。

> [!NOTE]
> 別の拡張機能の種類に精通していないか。 詳細については、[機能拡張のアーキテクチャと拡張機能の種類](understand-extensions.md)します。

## <a name="prepare-your-environment"></a>環境の準備

既に、していない場合は[環境を準備する](prepare-development-environment.md)依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることで。

## <a name="create-a-new-tool-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI を使用した新しいツールの拡張機能を作成します。 ##

インストールされているすべての依存関係を作成したら、新しいツールの拡張機能を作成する準備が整いました。  作成またはプロジェクト ファイルを含むフォルダーを参照、コマンド プロンプトを開いておよびそのフォルダーを作業ディレクトリとして設定します。  以前にインストールされた Windows Admin Center CLI を使用して、次の構文で、新しい拡張機能を作成します。

``` cmd
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペース) を含む、ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

これは、ツールに指定されたプロジェクトにすべての必要なテンプレート ファイルをコピー、および、会社とツールの名前を持つファイルを構成します。 名前を使用して現在の作業ディレクトリ内の新しいフォルダーを作成します。  

次に、先ほど作成したフォルダーにディレクトリを変更し、次のコマンドを実行して、必要なローカルの依存関係をインストールします。

``` cmd
npm install
```

これが完了すると、Windows Admin Center に新しい拡張機能を読み込む必要があるすべてのものを設定します。 

## <a name="add-content-to-your-extension"></a>拡張機能へのコンテンツを追加します。

Windows Admin Center CLI を使用した拡張機能を作成するので、コンテンツをカスタマイズする準備が整いました。  例については、何ができるは、これらのガイドを参照してください。

- 追加、[空のモジュール](guides\add-module.md)
- 追加、 [iFrame](guides\add-iframe.md)
 
さらに多くの例を参照して、 [SDK の GitHub サイト](https://aka.ms/wacsdk):
-  [開発者ツール](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools)Windows Admin Center にサイドロードできる完全に機能の拡張機能は、サンプルの機能とツール例を参照して、独自の拡張機能で使用できますの豊富なコレクションが含まれています。

## <a name="customize-your-extensions-icon"></a>拡張機能のアイコンをカスタマイズします。

ツールの一覧に、拡張機能のアイコンが表示されますをカスタマイズできます。  これを行うには、すべての変更```icon```エントリ```manifest.json```拡張機能。

``` json
"icon": "{!icon-uri}",
```

| 値 | 説明 | Uri の例 |
| ----- | ----------- | ------- |
| ```{!icon-uri}``` | アイコン リソースの場所 | ```assets/foo-icon.svg``` |

注: 現時点では、カスタム アイコンは、側の開発モードで、拡張機能を読み込むときに表示されません。  この問題を回避するには、内容を削除```target```次のようにします。

``` json
"target": "",
```

この構成に含まれている値を保持することが重要であるために、開発モードでのサイド ローディングの有効なのみ```target```し、拡張機能を公開する前に復元します。

## <a name="build-and-side-load-your-extension"></a>ビルドと側は、拡張機能を読み込む

次に、ビルドと側は、Windows Admin Center に、拡張機能を読み込みます。  コマンド ウィンドウを開き、ビルドする準備ができたし、ソース ディレクトリにディレクトリを変更します。

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

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョン、Windows Admin Center SDK の対象します。

拡張機能の最新の SDK の変更点とプラットフォームの変更を維持することは簡単です。  」を参照して[別のバージョンをターゲット](target-sdk-version.md)Windows Admin Center SDK の。