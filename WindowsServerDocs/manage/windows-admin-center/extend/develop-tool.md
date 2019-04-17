---
title: ツール拡張機能を開発します。
description: Windows Admin Center SDK (Project Honolulu) ツールの拡張機能を開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7dd213f7032ab77021bbfcbdc966c9c2307b86eb
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081059"
---
# ツール拡張機能を開発します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

ツール拡張機能は、ユーザーは、サーバーまたはクラスターなどの接続を管理する Windows Admin Center を操作する主な方法です。 Windows Admin Center のホーム画面で接続をクリックして接続するに、左側のナビゲーション ウィンドウでツールの一覧が表示し、されます。 ツールをクリックすると、ツールの拡張機能が読み込まれ、右側のウィンドウに表示されます。

ツール拡張機能が読み込まれるとき、対象のサーバーまたはクラスターで WMI の呼び出しまたは PowerShell スクリプトを実行 UI に情報を表示し、ユーザー入力に基づいてコマンドを実行またはできます。 ツール拡張機能は、それが表示される、さまざまな各ソリューションのツールのセットを生成するソリューションを定義します。

> [!NOTE]
> さまざまな拡張機能の種類に精通していないかどうか。 [拡張機能のアーキテクチャと拡張機能の種類](understand-extensions.md)について説明します。

## 環境の準備

いない場合、依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることによって[環境の準備](prepare-development-environment.md)をします。

## Windows Admin Center CLI を使用した新しいツール拡張機能を作成します。 ##

インストールされているすべての依存関係を作成したら、新しいツール拡張機能を作成する準備ができます。  作成または、プロジェクト ファイルが含まれているフォルダーを参照して、コマンド プロンプトを開いておよび作業ディレクトリとしてそのフォルダーを設定します。  以前にインストールされた Windows Admin Center CLI を使用して、次の構文で新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペース) を | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペース) をツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

これは、ツールは、指定したすべての必要なテンプレート ファイルをプロジェクトにコピー、および会社とツールの名前を使ってファイルを構成名を使用して、現在の作業ディレクトリ内の新しいフォルダーが作成されます。  

次に、先ほど作成したフォルダーにディレクトリを変更し、次のコマンドを実行して、必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、したすべての設定を新しい拡張機能を Windows Admin Center に読み込む必要があります。 

## 拡張機能にコンテンツを追加します。

Windows Admin Center CLI を使用して拡張機能を作成したらは、コンテンツをカスタマイズする準備ができたらします。  例については、実行できるは、これらのガイドを参照してください。

- [空のモジュール](guides\add-module.md)を追加します。
- [IFrame](guides\add-iframe.md)を追加します。
 
さらに多くの例には、当社の[GitHub SDK サイト](https://aka.ms/wacsdk)が見つかんだことができます。
-  [開発者ツール](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools)サイド ローディング Windows Admin Center には、完全に機能の拡張機能は、サンプル機能とツールの例を参照して、独自の拡張機能で使用できる豊富なコレクションが含まれています。

## ビルドとサイドロード拡張機能を読み込む

次に、ビルドとサイドロードは、Windows Admin Center に拡張機能を読み込みます。  コマンド ウィンドウを開き、ビルドする準備ができたら、ソース ディレクトリにディレクトリを変更します。

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

## Windows Admin Center SDK のさまざまなバージョンをターゲットします。

拡張機能を SDK の変更とプラットフォームの変更を最新の状態に保つことは簡単です。  Windows Admin Center SDK の[さまざまなバージョンを対象](target-sdk-version.md)にする方法について参照してください。