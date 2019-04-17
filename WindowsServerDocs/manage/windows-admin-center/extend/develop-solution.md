---
title: ソリューション拡張機能を開発します。
description: Windows Admin Center SDK (Project Honolulu) のソリューション拡張機能を開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ed5ecddbaef91f127846825e408a9a6ec65ff741
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081069"
---
# ソリューション拡張機能を開発します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

ソリューションは、主に Windows Admin Center を通じて管理するオブジェクトの一意の種類を定義します。  これらのソリューション/接続の種類は、既定で Windows Admin Center に含まれています。

* Windows Server の接続
* Windows PC の接続
* フェールオーバー クラスターの接続
* ハイパーコンバージド クラスターの接続

Windows Admin Center の接続] ページからの接続を選択すると接続の種類のソリューション拡張機能が読み込まれ、Windows Admin Center は、ターゲット ノードに接続しようとしています。 接続が成功した場合は、ソリューション拡張機能の UI が読み込み、および Windows Admin Center は、左側のナビゲーション ウィンドウで、そのソリューションのツールを表示します。

コンピューター名を使って、既定の接続の種類の上、このようなネットワーク スイッチでは、またはできないその他のハードウェアで定義されていないサービスの管理の GUI をビルドする場合は、独自のソリューション拡張機能を作成することがあります。

> [!NOTE]
> さまざまな拡張機能の種類に精通していないかどうか。 [拡張機能のアーキテクチャと拡張機能の種類](understand-extensions.md)について説明します。

## 環境の準備

いない場合、依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることによって[環境の準備](prepare-development-environment.md)をします。

## Windows Admin Center CLI を使用した新しいソリューション拡張機能を作成します。 ##

インストールされているすべての依存関係を作成したら、新しいソリューション拡張機能を作成する準備ができます。  作成または、プロジェクト ファイルが含まれているフォルダーを参照して、コマンド プロンプトを開いておよび作業ディレクトリとしてそのフォルダーを設定します。  以前にインストールされた Windows Admin Center CLI を使用して、次の構文で新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペース) を | ```Contoso Inc``` |
| ```{!Solution Name}``` | (スペース) をソリューションの名前 | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | (スペース) をツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

これは、ソリューションに指定したすべての必要なテンプレート ファイルをプロジェクトにコピー、および会社、ソリューションでは、ツールの名前と、ファイルを構成名を使用して、現在の作業ディレクトリ内の新しいフォルダーが作成されます。  

次に、先ほど作成したフォルダーにディレクトリを変更し、次のコマンドを実行して、必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、したすべての設定を新しい拡張機能を Windows Admin Center に読み込む必要があります。 

## 拡張機能にコンテンツを追加します。

Windows Admin Center CLI を使用して拡張機能を作成したらは、コンテンツをカスタマイズする準備ができたらします。  例については、実行できるは、これらのガイドを参照してください。

- [空のモジュール](guides\add-module.md)を追加します。
- [IFrame](guides\add-iframe.md)を追加します。
- [カスタム接続プロバイダー](guides\create-connection-provider.md)を作成します。
- [ルートのナビゲーションの動作](guides\modify-root-navigation.md)を変更します。
 
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