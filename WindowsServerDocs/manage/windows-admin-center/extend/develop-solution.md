---
title: ソリューション拡張機能の開発
description: ソリューションの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) の開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 268a7d2833f73e9fab006501e9b3dc261d1b1d9e
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452579"
---
# <a name="develop-a-solution-extension"></a>ソリューション拡張機能の開発

>適用先:Windows Admin Center、Windows Admin Center プレビュー

ソリューションは、主に、Windows Admin Center で管理するオブジェクトの一意の型を定義します。  これらのソリューション/接続の種類は、既定では、Windows Admin Center でインクルードされます。

* Windows Server の接続
* Windows PC の接続
* フェールオーバー クラスターの接続
* ハイパー コンバージド クラスター接続

Windows Admin Center の [接続] ページからの接続を選択してその接続の種類のソリューションの拡張機能が読み込まれると、Windows Admin Center は、ターゲット ノードに接続しようとしています。 接続が成功した場合、ソリューションの拡張機能の UI が読み込まれます、および Windows Admin Center は、左側のナビゲーション ウィンドウでそのソリューションのツールに表示されます。

コンピューター名で、既定の接続型の上、このようなネットワーク スイッチでは、または探索されないその他のハードウェアで定義されていないサービスの管理 GUI を構築する場合は、独自のソリューションの拡張機能を作成する可能性があります。

> [!NOTE]
> 別の拡張機能の種類に精通していないか。 詳細については、[機能拡張のアーキテクチャと拡張機能の種類](understand-extensions.md)します。

## <a name="prepare-your-environment"></a>環境の準備

既に、していない場合は[環境を準備する](prepare-development-environment.md)依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることで。

## <a name="create-a-new-solution-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI を使用したソリューションの新しい拡張機能を作成します。 ##

インストールされているすべての依存関係を作成したら、新しいソリューションの拡張機能を作成する準備が整いました。  作成またはプロジェクト ファイルを含むフォルダーを参照、コマンド プロンプトを開いておよびそのフォルダーを作業ディレクトリとして設定します。  以前にインストールされた Windows Admin Center CLI を使用して、次の構文で、新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --solution "{!Solution Name}" --tool "{!Tool Name}"
```

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso Inc``` |
| ```{!Solution Name}``` | (スペース) を含む、ソリューションの名前 | ```Contoso Foo Works Suite``` |
| ```{!Tool Name}``` | (スペース) を含む、ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --solution "Contoso Foo Works Suite" --tool "Manage Foo Works"
```

これは、プロジェクトにすべての必要なテンプレート ファイルをコピー、し、会社、ソリューションでは、ツール名とファイルを構成、ソリューションの指定した名前を使用して現在の作業ディレクトリ内の新しいフォルダーを作成します。  

次に、先ほど作成したフォルダーにディレクトリを変更し、次のコマンドを実行して、必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、Windows Admin Center に新しい拡張機能を読み込む必要があるすべてのものを設定します。 

## <a name="add-content-to-your-extension"></a>拡張機能へのコンテンツを追加します。

Windows Admin Center CLI を使用した拡張機能を作成するので、コンテンツをカスタマイズする準備が整いました。  例については、何ができるは、これらのガイドを参照してください。

- 追加、[空のモジュール](guides/add-module.md)
- 追加、 [iFrame](guides/add-iframe.md)
- 作成、[カスタム接続プロバイダー](guides/create-connection-provider.md)
- 変更[ナビゲーションの動作をルート](guides/modify-root-navigation.md)
 
さらに多くの例を参照して、 [SDK の GitHub サイト](https://aka.ms/wacsdk):
-  [開発者ツール](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/windows-admin-center-developer-tools)Windows Admin Center にサイドロードできる完全に機能の拡張機能は、サンプルの機能とツール例を参照して、独自の拡張機能で使用できますの豊富なコレクションが含まれています。

## <a name="build-and-side-load-your-extension"></a>ビルドと側は、拡張機能を読み込む

次に、ビルドと側は、Windows Admin Center に、拡張機能を読み込みます。  コマンド ウィンドウを開き、ビルドする準備ができたし、ソース ディレクトリにディレクトリを変更します。

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

## <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョン、Windows Admin Center SDK の対象します。

拡張機能の最新の SDK の変更点とプラットフォームの変更を維持することは簡単です。  」を参照して[別のバージョンをターゲット](target-sdk-version.md)Windows Admin Center SDK の。