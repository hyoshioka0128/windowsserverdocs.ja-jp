---
title: ゲートウェイ プラグインを開発します。
description: ゲートウェイ プラグイン Windows Admin Center SDK (Project Honolulu) の開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cee5b8e3611a264119947103d22d9aa3b9a56b
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081159"
---
# ゲートウェイ プラグインを開発します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center ゲートウェイ プラグインと通信 API UI から、ツールやソリューションのターゲット ノードにします。  Windows Admin Center は、ターゲット ノード上で実行するには、コマンドおよびゲートウェイ プラグインからスクリプトをリレーするゲートウェイ サービスをホストします。 ゲートウェイ サービスは、既定の以外のプロトコルをサポートするカスタム ゲートウェイ プラグインを含めるに拡張できます。

既定では Windows Admin Center では、これらのゲートウェイ プラグインが含まれていません。

* PowerShell のゲートウェイ プラグイン
* WMI ゲートウェイ プラグイン

PowerShell または WMI 以外のプロトコルと通信する場合は、ように、残りの部分を構築できます、独自のゲートウェイ プラグイン。  ゲートウェイ プラグインは既存のゲートウェイ プロセスから別の AppDomain に読み込まれるが、権限の同じレベルの昇格を使用します。

> [!NOTE]
> さまざまな拡張機能の種類に精通していないかどうか。 [拡張機能のアーキテクチャと拡張機能の種類](understand-extensions.md)について説明します。

## 環境の準備

いない場合、依存関係とすべてのプロジェクトに必要なグローバルの前提条件をインストールすることによって[環境の準備](prepare-development-environment.md)をします。

## ゲートウェイ プラグイン (c# ライブラリ) の作成します。

カスタムのゲートウェイ プラグインを作成する新しい C# のコードを実装するクラスを作成、```IPlugIn```からインターフェイス、```Microsoft.ManagementExperience.FeatureInterfaces```名前空間です。  

> [!NOTE]
> ```IFeature``` 、SDK の以前のバージョンで利用可能なインターフェイスが廃止としてフラグが設定できるようになりました。  ゲートウェイ プラグインのすべての開発には、IPlugIn (または、必要に応じて HttpPlugIn 抽象クラス) を使用する必要があります。

### GitHub のサンプルをダウンロードします。

カスタム ゲートウェイ プラグインをすばやく開始するのに複製するか、Windows Admin Center SDK [GitHub サイト](https://aka.ms/wacsdk)から、[サンプルの c# プラグイン プロジェクト](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)のコピーをダウンロードすることができます。

### コンテンツを追加します。

複製された独自のカスタム Api を含む[プロジェクトのサンプルは、c# プラグイン](https://github.com/Microsoft/windows-admin-center-sdk/tree/master/GatewayPluginExample/Plugin)プロジェクト (または、独自のプロジェクト) のコピーを新しいコンテンツを追加し、次の手順で使用するには、カスタムのゲートウェイ プラグイン DLL ファイルをビルドします。

### プラグインをテストするための展開します。

Windows Admin Center ゲートウェイ プロセスに読み込むことによって、カスタムのゲートウェイ プラグイン DLL をテストします。

Windows Admin Center がすべてのプラグインでの検索、 ```plugins``` (メンバー列挙体の CommonApplicationData 値を使用)、現在のコンピューターのアプリケーション データ フォルダー内のフォルダーです。 この場所は、Windows 10 で```C:\ProgramData\Server Management Experience```します。  場合、```plugins```フォルダーが存在しない、まだ自分でフォルダーを作成できます。

> [!NOTE]
> デバッグ ビルドでプラグインの場所を上書きするには、"StaticsFolder"構成値を更新します。 ローカルでデバッグする場合、この設定は、デスクトップのソリューションの読み込みますです。 

プラグインの実行フォルダー内で (この例では```C:\ProgramData\Server Management Experience\plugins```)

* 同じ名前の新しいフォルダーを作成、```Name```プロパティの値、 ```Feature``` 、カスタムのゲートウェイ プラグイン DLL で (、サンプル プロジェクトで、```Name```は"サンプル Uno")
* この新しいフォルダーにカスタムのゲートウェイ プラグインの DLL ファイルをコピーします。
* Windows Admin Center の処理を再開します。

Windows Admin プロセスが再起動したら、ことができます、GET を発行して、カスタムのゲートウェイ プラグイン DLL で Api を行使する配置、修正プログラム、削除、またはに投稿するには ```http(s)://{domain|localhost}/api/nodes/{node}/features/{feature name}/{identifier}```

### 省略可能: がプラグインをデバッグするためにアタッチします。

Visual Studio 2017 でのデバッグ] メニューから「プロセスにアタッチ」を選択します。 次のウィンドウで利用可能なプロセスの一覧をスクロールして、SMEDesktop.exe を選択し、「アタッチ」] をクリックします。 1 回、デバッガーが起動することができますにブレークポイントを設定、機能のコードと作業では、上記の URL の形式でします。 このサンプル プロジェクトについて (機能名:"サンプル Uno") url:"http://localhost:6516/api/nodes/fake-server.my.domain.com/features/Sample%20Uno"

## Windows Admin Center CLI を使用したツールの拡張機能を作成します。 ##

そこから、カスタムのゲートウェイ プラグインを呼び出すことができますツール拡張機能を作成する必要があります。  作成またはプロジェクト ファイルの保存、コマンド プロンプトを開き、作業ディレクトリとしてそのフォルダーを設定するフォルダーを参照します。  以前にインストールされた Windows Admin Center CLI を使用して、次の構文で新しい拡張機能を作成します。

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

## ツール拡張機能に接続する、カスタムのゲートウェイ プラグイン

Windows Admin Center CLI を使用して拡張機能を作成したのではツール拡張機能を次の手順に従って、カスタムのゲートウェイ プラグインを接続できます。

- [空のモジュール](guides\add-module.md)を追加します。
- ツール拡張機能で、[カスタムのゲートウェイ プラグイン](guides\use-custom-gateway-plugin.md)を使用します。
 
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