---
title: ゲートウェイ プラグインの開発
description: ゲートウェイ プラグイン Windows Admin Center SDK (プロジェクト ホノルル) の開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cee5b8e3611a264119947103d22d9aa3b9a56b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834393"
---
# <a name="develop-a-gateway-plugin"></a>ゲートウェイ プラグインの開発

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center ゲートウェイ プラグインには、ターゲット ノードに、ツールやソリューションの UI からの通信の API ができます。  Windows Admin Center では、ターゲット ノードで実行するには、コマンドおよびゲートウェイ プラグインからスクリプトを中継するゲートウェイ サービスをホストします。 ゲートウェイ サービスは、既定の以外のプロトコルをサポートするカスタム ゲートウェイ プラグインを含める拡張できます。

Windows Admin Center では既定では、これらのゲートウェイ プラグインが含まれています。

* PowerShell ゲートウェイ プラグイン
* WMI ゲートウェイ プラグイン

PowerShell または WMI 以外のプロトコルと通信したい場合など、残りの部分で構築できますゲートウェイ プラグイン。  ゲートウェイ プラグインは、既存のゲートウェイ プロセスから別の AppDomain に読み込まれますが、権利については、同じレベルの昇格を使用します。

> [!NOTE]
> 別の拡張機能の種類に精通していないか。 詳細については、[機能拡張のアーキテクチャと拡張機能の種類](understand-extensions.md)します。

## <a name="prepare-your-environment"></a>環境の準備

既に、していない場合は[環境を準備する](prepare-development-environment.md)依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることで。

## <a name="create-a-gateway-plugin-c-library"></a>ゲートウェイのプラグインを作成 (C#ライブラリ)

ゲートウェイのカスタム プラグインを作成するには、新規作成C#を実装するクラス、```IPlugIn```からインターフェイス、```Microsoft.ManagementExperience.FeatureInterfaces```名前空間。  

> [!NOTE]
> ```IFeature``` SDK の以前のバージョンで使用可能なインターフェイスが不使用とフラグが設定ようになりました。  ゲートウェイのすべてのプラグイン開発には、IPlugIn (または必要に応じて HttpPlugIn 抽象クラス) を使用する必要があります。

### <a name="download-sample-from-github"></a>GitHub からサンプルをダウンロードします。

手始めにゲートウェイのカスタム プラグインを使用した、複製またはのコピーをダウンロード、[サンプルC#プラグイン プロジェクト](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)Windows Admin Center SDK から[GitHub サイト](https://aka.ms/wacsdk)します。

### <a name="add-content"></a>コンテンツを追加します。

複製されたコピーの新しいコンテンツの追加、[サンプルC#プラグイン プロジェクト](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)プロジェクト (または独自のプロジェクト) に含めるカスタム Api、ゲートウェイのカスタム プラグイン DLL のビルドは、次の手順で使用するファイルします。

### <a name="deploy-plugin-for-testing"></a>配置をテストするためのプラグイン

カスタム ゲートウェイ プラグイン DLL をテストするには、Windows Admin Center ゲートウェイ プロセスに読み込みます。

Windows Admin Center がすべてのプラグインを探し、 ```plugins``` (Environment.SpecialFolder 列挙体の CommonApplicationData 値を使用して) 現在のコンピューターのアプリケーション データ フォルダー内のフォルダー。 この場所は、Windows 10 で```C:\ProgramData\Server Management Experience```します。  場合、```plugins```フォルダーが存在しない時点では、フォルダーを自分で作成できます。

> [!NOTE]
> デバッグ ビルドでプラグインの場所をオーバーライドするには、"StaticsFolder"構成値を更新します。 ローカルでデバッグしている場合、この設定はデスクトップ ソリューションの App.Config では。 

Plugins フォルダー内 (この例で```C:\ProgramData\Server Management Experience\plugins```)

* 同じ名前の新しいフォルダーを作成、```Name```プロパティの値、```Feature```カスタム ゲートウェイ プラグイン DLL の (このサンプル プロジェクトで、```Name```は"サンプル Uno")
* ゲートウェイのカスタム プラグインの DLL ファイルをこの新しいフォルダーにコピーします。
* Windows Admin Center プロセスを再起動します。

Windows の管理プロセスを再起動した後は、GET を発行することによってカスタム ゲートウェイ プラグイン DLL の Api を練習するができます PUT、PATCH、DELETE、または投稿するには ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### <a name="optional-attach-to-plugin-for-debugging"></a>省略可能: デバッグ用のプラグインにアタッチします。

Visual Studio 2017 でのデバッグ メニューから"プロセスにアタッチ を選択します。 次のウィンドウでは、使用可能なプロセスの一覧をスクロールして、「SMEDesktop.exe、を選択し、"Attach"をクリックします。 1 回、デバッガーが開始することができますにブレークポイントを設定、機能のコードと、上記の URL 形式を演習します。 このサンプル プロジェクトの (機能名。"サンプル Uno") の URL です:"http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno"

## <a name="create-a-tool-extension-with-the-windows-admin-center-cli"></a>Windows Admin Center CLI を使用したツールの拡張機能を作成します。 ##

元のゲートウェイのカスタム プラグインを呼び出すことができますツール拡張を作成する必要があります。  作成またはプロジェクト ファイルの保存、コマンド プロンプトを開き、そのフォルダーを作業ディレクトリとして設定しフォルダーを参照します。  既にインストールされている Windows Admin Center CLI を使用して、次の構文で、新しい拡張機能を作成します。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}"
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペース) を含む、ツール名 | ```Manage Foo Works``` |

次に使用方法の例を示します。

```
wac create --company "Contoso Inc" --tool "Manage Foo Works"
```

これは、ツールに指定されたプロジェクトにすべての必要なテンプレート ファイルをコピー、および、会社とツールの名前を持つファイルを構成します。 名前を使用して現在の作業ディレクトリ内の新しいフォルダーを作成します。  

次に、先ほど作成したフォルダーにディレクトリを変更し、次のコマンドを実行して、必要なローカルの依存関係をインストールします。

```
npm install
```

これが完了すると、Windows Admin Center に新しい拡張機能を読み込む必要があるすべてのものを設定します。 

## <a name="connect-your-tool-extension-to-your-custom-gateway-plugin"></a>ツール拡張機能をカスタム ゲートウェイ プラグインに接続します。

Windows Admin Center CLI を使用した拡張機能を作成するのでは、次の手順に従って、ツールの拡張機能をカスタム ゲートウェイ プラグインに接続する準備が完了したら。

- 追加、[空のモジュール](guides\add-module.md)
- 使用して、[カスタム ゲートウェイ プラグイン](guides\use-custom-gateway-plugin.md)ツールの拡張機能
 
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