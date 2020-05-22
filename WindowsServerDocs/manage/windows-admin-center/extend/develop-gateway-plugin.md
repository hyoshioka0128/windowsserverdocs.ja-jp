---
title: ゲートウェイ プラグインの開発
description: ゲートウェイプラグインの開発 Windows 管理センター SDK (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2b096b226190ad1ca3fd07c38b7b939d019ee30f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406939"
---
# <a name="develop-a-gateway-plugin"></a>ゲートウェイ プラグインの開発

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows 管理センターのゲートウェイプラグインを使用すると、ツールまたはソリューションの UI からターゲットノードへの API 通信が可能になります。  Windows 管理センターは、ターゲットノードで実行されるゲートウェイプラグインからコマンドとスクリプトをリレーするゲートウェイサービスをホストします。 ゲートウェイサービスを拡張して、既定のプロトコル以外のプロトコルをサポートするカスタムゲートウェイプラグインを含めることができます。

これらのゲートウェイプラグインは、既定で Windows 管理センターに含まれています。

* PowerShell ゲートウェイプラグイン
* WMI ゲートウェイプラグイン

REST など、PowerShell または WMI 以外のプロトコルと通信する場合は、独自のゲートウェイプラグインを作成できます。  ゲートウェイプラグインは、既存のゲートウェイプロセスとは別の AppDomain に読み込まれますが、権限については同じレベルの昇格を使用します。

> [!NOTE]
> さまざまな拡張機能の種類に慣れていない場合は、 拡張[機能のアーキテクチャと拡張機能の種類](understand-extensions.md)の詳細については、こちらを参照してください。

## <a name="prepare-your-environment"></a>環境の準備

まだインストールしていない場合は、すべてのプロジェクトに必要な依存関係とグローバルな前提条件をインストールして[環境を準備](prepare-development-environment.md)します。

## <a name="create-a-gateway-plugin-c-library"></a>ゲートウェイプラグイン (C#ライブラリ) を作成する

カスタムゲートウェイプラグインを作成するには、```Microsoft.ManagementExperience.FeatureInterfaces``` C#名前空間から ```IPlugIn``` インターフェイスを実装する新しいクラスを作成します。  

> [!NOTE]
> 以前のバージョンの SDK で利用可能な ```IFeature``` インターフェイスには、互換性のために残されているものとしてフラグが付けられました。  すべてのゲートウェイプラグイン開発では、IPlugIn (または必要に応じて HttpPlugIn 抽象クラス) を使用する必要があります。

### <a name="download-sample-from-github"></a>GitHub からサンプルをダウンロードする

カスタムゲートウェイプラグインを使用してすぐに開始するには、Windows 管理センター SDK [GitHub サイト](https://aka.ms/wacsdk)から[ C#サンプルプラグインプロジェクト](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)のクローンまたはダウンロードを行うことができます。

### <a name="add-content"></a>コンテンツを追加する

[ C#サンプルプラグインプロジェクト](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)プロジェクト (または独自のプロジェクト) のクローンしたコピーに新しいコンテンツを追加してカスタム api を含め、次の手順で使用するカスタムゲートウェイプラグイン DLL ファイルを作成します。

### <a name="deploy-plugin-for-testing"></a>テスト用のプラグインの配置

カスタムゲートウェイプラグイン DLL を Windows 管理センターゲートウェイプロセスに読み込んでテストします。

Windows 管理センターは、現在のコンピューターの Application Data フォルダーにある ```plugins``` フォルダー内のすべてのプラグインを検索します (System.environment.specialfolder 列挙型の CommonApplicationData 値を使用します)。 Windows 10 では、この場所は ```C:\ProgramData\Server Management Experience```です。  ```plugins``` フォルダーがまだ存在しない場合は、自分でフォルダーを作成することができます。

> [!NOTE]
> デバッグビルドでプラグインの場所をオーバーライドするには、"StaticsFolder" 構成値を更新します。 ローカルでデバッグしている場合、この設定はデスクトップソリューションの app.config にあります。 

プラグインフォルダー内 (この例では ```C:\ProgramData\Server Management Experience\plugins```)

* カスタムゲートウェイプラグイン DLL 内の ```Feature``` の ```Name``` プロパティ値と同じ名前の新しいフォルダーを作成します (サンプルプロジェクトでは、```Name``` は "Sample Uno")。
* カスタムゲートウェイプラグイン DLL ファイルをこの新しいフォルダーにコピーします
* Windows 管理センターのプロセスを再起動する

Windows 管理プロセスを再起動した後、GET、PUT、PATCH、DELETE、または POST ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}``` を発行して、カスタムゲートウェイプラグイン DLL で Api を実行できます。

### <a name="optional-attach-to-plugin-for-debugging"></a>省略可能: デバッグ用にプラグインにアタッチする

Visual Studio 2017 で、[デバッグ] メニューの [プロセスにアタッチ] をクリックします。 次のウィンドウで、[選択可能なプロセス] ボックスの一覧をスクロールして SMEDesktop を選択し、[アタッチ] をクリックします。 デバッガーが起動したら、機能コードにブレークポイントを設定してから、上記の URL 形式を使用することができます。 サンプルプロジェクト (機能名: "Sample Uno") の場合、URL は "<http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno>" になります。

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Windows 管理センター CLI を使用してツール拡張機能を作成する ##

ここで、カスタムゲートウェイプラグインを呼び出すことができるツール拡張機能を作成する必要があります。  プロジェクトファイルを格納するフォルダーを作成または参照し、コマンドプロンプトを開き、そのフォルダーを作業ディレクトリとして設定します。  以前にインストールされた Windows 管理センター CLI を使用して、次の構文で新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

これにより、ツールで指定した名前を使用して現在の作業ディレクトリ内に新しいフォルダーが作成され、必要なすべてのテンプレートファイルがプロジェクトにコピーされ、会社名とツール名を使用してファイルが構成されます。  

次に、作成したフォルダーにディレクトリを変更し、次のコマンドを実行して必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、Windows 管理センターに新しい拡張機能を読み込むために必要なすべての設定が完了します。 

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>ツール拡張機能をカスタムゲートウェイプラグインに接続する

Windows 管理センター CLI を使用して拡張機能を作成したので、次の手順に従って、ツール拡張機能をカスタムゲートウェイプラグインに接続する準備ができました。

- 空の[モジュール](guides/add-module.md)を追加する
- ツール拡張機能で[カスタムゲートウェイプラグイン](guides/use-custom-gateway-plugin.md)を使用する
 
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
