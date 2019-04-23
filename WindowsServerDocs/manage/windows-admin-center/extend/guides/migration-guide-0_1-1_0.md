---
title: Windows Admin Center SDK 0.1 ~ 1.0 からの移行します。
description: このガイドでは、Windows Admin Center SDK バージョン 0.1 ~ 1.0 からの移行を利用します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886473"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Windows Admin Center SDK 0.1 ~ 1.0 からの移行します。

>適用先:Windows Admin Center Preview

このガイドを使用すると、Windows Admin Center SDK 0.1 ~ 1.0 のバージョンから移行できます。  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. 開発ガイド拡張子を持つ新しいコントロールの概要について説明します

Windows Admin Center 1902 およびそれ以降のバージョンが含まれています、**開発ガイド**拡張機能は、コントロール (新しく利用可能なコントロールを含む) と、独自の拡張機能を構築するためのシナリオの例を見つけるに使用することができます。  開発ガイドが置き換えられます、 **Developer Tools**以前のバージョンの SDK からの拡張機能。

### <a name="use-the-dev-guide-in-windows-admin-center"></a>Windows Admin Center での開発ガイドを使用します。

開発ガイドとは、以降では、Windows Admin Center バージョン 1902 ソリューションとして利用可能です。  開発ガイドは、プレインストールされているが、設定を使用して有効にする必要があります。

**Windows Admin Center での開発ガイドを有効にします。**

* 開く Windows Admin Center (1902 およびそれ以降のバージョン)
* をクリックして、**設定**ウィンドウの右上隅のアイコン
* 選択、**詳細** タブ
* [*実験キー*、] をクリックして**追加**
* 新しい値を入力```msft.sme.shell.devguide```前の手順で作成された空のフィールドに
* クリックして**を保存し、再読み込み**

**Windows Admin Center での開発ガイドを開きます。**

* 開く Windows Admin Center (1902 およびそれ以降のバージョン)
* ソリューションのすべての型の表示を左上のドロップダウンをクリックします。
* 選択、**開発ガイド**ソリューション 
    * 表示されているソリューションが表示されない場合、は、開発ガイドが有効になっていることを確認してください (前のセクションを参照してください)、Windows Admin Center が再読み込みします。
* タブのいずれかを選択して開発ガイドの内容を参照します。
    * **ランディング:** コード サンプルが含まれます*管理に*と*通知*シナリオ
    * **コントロール:** SDK の使用可能な各コントロールの例が含まれています
    * **パイプします。** コンバーターとフォーマッタの使用可能な関数の例が含まれています
    * **スタイル:** SDK で使用できる CSS スタイルの例が含まれています
    * **MsftSme:** 例と高度なシナリオのガイダンスが含まれています 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>GitHub での開発ガイドのソース コードを参照します。

参照することができます、[ソース コード](https://github.com/Microsoft/windows-admin-center-sdk/)の例の HTML、CSS、および TypeScript のコード サンプルを見つけるには、GitHub での開発ガイド。

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. 最新の SDK の開発環境を準備します。

Node.js のバージョンの更新のインストールまたは[10.15.1 LTS 以降](https://nodejs.org/en/)します。

最新バージョンには、Windows Admin Center CLI を更新します。

[//]: # "npm-g をアンインストールします。 windows-admin-center-cli@next"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

これらのバージョンには、グローバルな依存関係を更新します。

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3.最新の SDK を使用した新しいプロジェクトを作成します。

Windows Admin Center CLI を使用して、新しいプロジェクトのターゲットを作成する、```next```バージョン (SDK 1.0)。

[//]: # "wac create - 会社"Contoso Inc--' ' 管理 Foo Works'--実験的なバージョンのツール"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

次に、先ほど作成したフォルダーにディレクトリを変更しを実行して必要なローカルの依存関係をインストール```npm install ```します。

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4。最新の SDK を使用して既存のプロジェクトを変更します。

重要:続行する前に、プロジェクトのバックアップを作成します。

次の行を変更```package.json```ターゲットに、```next```バージョン (SDK 1.0)。

[//]: # "'@microsoft/windows-admin-center-sdk': 'experimental'"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

実行して```npm install```プロジェクト全体での参照を更新します。

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5。SDK CLI を使用して、移行の一般的な問題を修正するには

重要:続行する前に、プロジェクトのバックアップを作成します。

プロジェクトのルート フォルダーから、プロジェクトの移行の一般的な問題を自動的に解決する、次の CLI コマンドを実行します。

``` cmd
wac updateSeven --update
```

この CLI コマンドでは、次の問題を自動的にアドレスします。

* 再生成します。 ```package-lock.json```
* Angular のコンパイル環境でのファイルを更新します。
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6。SDK CLI を使用して、移行の一般的な問題を理解するには

プロジェクトのルート フォルダーからプロジェクトを監査し、手動で対処する必要がある一般的な移行の問題を見つけるには、次の CLI コマンドを実行します。

``` cmd
wac updateSeven --audit
```

これにより、プロジェクトで、次の問題のインスタンスが検索します。

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>次の CSS クラスの使用状況をこれらの sme クラスに置き換えます。

| 古い CSS クラス | 新しい CSS クラス |
| -- | -- |
| .auto フレックス-サイズ |  .sme 位置柔軟な自動 |
| .border すべて |  .sme-border-inset-sm AND .sme-border-color-base-90 |
| .border 下部 |  .sme-border-bottom-sm AND .sme-border-bottom-color-base-90 |
| .border 水平 |  .sme-border-horizontal-sm AND .sme-border-horizontal-color-base-90 |
| .border 左 |  .sme-border-left-sm AND .sme-border-left-color-base-90 |
| .border 右 |  .sme-border-right-sm AND .sme-border-right-color-base-90 |
| .border 上部 |  .sme-border-top-sm AND .sme-border-top-color-base-90 |
| .border 垂直 |  .sme-border-vertical-sm AND .sme-border-vertical-color-base-90 |
| .break word |  .sme-arrange-ws-wrap |
| .btn |  .sme ボタン OR ボタン |
| .btn プライマリ |  .sme button.sme ボタン プライマリ OR.button.sme- ボタン-プライマリ |
| .color-濃い |  .sme 色 alt キーを |
| .color ライト |  .sme ベースの色 |
| .color-淡い灰色 |  .sme-color-base-90 |
| .fixed フレックス-サイズ |  .sme-position-flex-none |
| .flex レイアウト |  .sme-arrange-stack-h OR .sme-arrange-stack-v |
| .font 太字 |  .sme-フォントに斜体 1 |
| .highlight |  .sme-background-color-yellow |
| .horizontal |  .sme-arrange-stack-h |
| されないスクロール |  .sme 位置柔軟な自動 |
| .nowrap |  .sme-arrange-stack-h OR .sme-arrange-stack-v |
| .relative |  .sme-layout-relative |
| .relative-center |  .sme-layout-absolute .sme-position-center |
| .reverse |  .sme-arrange-stack-reversed |
| .stretch-absolute |  .sme レイアウトの絶対 .sme-位置-埋め込み-なし |
| .stretch-fixed |  .sme-layout-fixed .sme-position-inset-none |
| .stretch-vertical |  .sme-position-stretch-v |
| .stretch-width |  .sme-position-stretch-h |
| .vertical |  .sme-arrange-stack-v |
| .vertical スクロールのみ |  .sme-配置-オーバーフロー-非表示にする-x sme と配置のオーバーフロー-自動-y |
| .wrap |  .sme-arrange-wrapstack-h OR .sme-arrange-wrapstack-v |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>次のコンポーネントの使用状況をこれらの sme コンポーネントに置き換えます。

| 古いコンポーネント | 新しいコンポーネント |
| -- | -- |
| .alert |  sme アラート |
| .alert 危険性 |  sme アラート |
| .breadCrumb |  sme アラート |
| .checkbox |  フォーム フィールドの sme [型 ="checkbox"] |
| .combobox |  sme-form-field[type="select"] |
| .dashboard |  sme をレイアウト-コンテンツのゾーンに埋め込まれた sme-配置-スタック-h |
| .details パネル |  sme プロパティ グリッド |
| .details-panel-container |  sme プロパティ グリッド |
| .details-tab |  プロパティ グリッドの sme OR sme のピボット |
| .details-wrapper |  sme プロパティ グリッド |
| .disabled |  sme 無効 |
| .form ボタン | sme フォーム フィールド |
| .form コントロール | sme フォーム フィールド |
| .form コントロール | sme フォーム フィールド |
| .form グループ | sme フォーム フィールド |
| .form グループのラベル | sme フォーム フィールド |
| .form 入力 | sme フォーム フィールド |
| .form stretch | sme フォーム フィールド |
| .input ファイル | sme フォーム フィールド |
| .nav-tabs |  sme ピボット |
| .radio |  フォーム フィールドの sme [型 ="radio"] |
| .required-clue | sme フォーム フィールド |
| .searchbox |  フォーム フィールドの sme [型 =「検索」] |
| .toggle スイッチ |  フォーム フィールドの sme [型 =「トグル スイッチ」] |
| .tool-container |  sme レイアウト コンテンツ ゾーンまたは sme をレイアウト-コンテンツのゾーンに埋め込まれました。 |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>これらの CSS クラスは非推奨し、現在サポートされていません。

| 古いクラス | 非推奨 |
| -- | -- |
| .acceptable | (非推奨) |
| .color-error | (非推奨) |
| .color 情報 | (非推奨) |
| .color 成功 | (非推奨) |
| .color-warning | (非推奨) |
| .delete-button | (非推奨) |
| .details-content | (非推奨) |
| .error-cover | (非推奨) |
| メッセージ | (非推奨) |
| .guided ウィンドウ-ボタン | (非推奨) |
| .header-container | (非推奨) |
| .icon win | (非推奨) |
| .indent | (非推奨) |
| .invalid | (非推奨) |
| .item 一覧 | (非推奨) |
| .modal スクロール可能です | (非推奨) |
| 。 複数のセクション | (非推奨) |
| されないアクション-バー | (非推奨) |
| .overflow 余白 | (非推奨) |
| .overflow ツール | (非推奨) |
| .progress-cover | (非推奨) |
| ですパネル | (非推奨) |
| .rollup | (非推奨) |
| .rollup 状態 | (非推奨) |
| .rollup タイトル | (非推奨) |
| .rollup 値 | (非推奨) |
| .searchbox-操作バー | (非推奨) |
| .size-h-1 | (非推奨) |
| .size-h-2 | (非推奨) |
| .size-h-3 | (非推奨) |
| .size-h-4 | (非推奨) |
| .size-full h | (非推奨) |
| .size h-1.5 | (非推奨) |
| .size-v-1 | (非推奨) |
| .size-v-2 | (非推奨) |
| .size-v-3 | (非推奨) |
| .size-v-4 | (非推奨) |
| .status-icon | (非推奨) |
| .svg-16px | (非推奨) |
| .table インデント | (非推奨) |
| .table sm | (非推奨) |
| .thin | (非推奨) |
| .tile | (非推奨) |
| .tile 本文 | (非推奨) |
| .tile コンテンツ | (非推奨) |
| .tile フッター | (非推奨) |
| .tile ヘッダー | (非推奨) |
| .tile レイアウト | (非推奨) |
| .tile テーブル | (非推奨) |
| .toolbar | (非推奨) |
| .tool バー | (非推奨) |
| .tool ヘッダー | (非推奨) |
| .tool インボックス ヘッダー | (非推奨) |
| .tool ウィンドウ | (非推奨) |
| .usage バー | (非推奨) |
| バー領域の .usage | (非推奨) |
| .usage、バーの背景 | (非推奨) |
| .usage のタイトル バー | (非推奨) |
| .usage とバーの値 | (非推奨) |
| .usage グラフ | (非推奨) |
| .usage メッセージ | (非推奨) |
| .usage メッセージ-領域 | (非推奨) |
| .usage メッセージ-タイトル | (非推奨) |
| .warning | (非推奨) |
| .white 領域 | (非推奨) |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7.理解し、監視可能なオブジェクトに関する問題を解決するには

### <a name="update--rxjs-function-use-for-observable-objects"></a>Update```rxjs```関数の監視可能なオブジェクトの使用

これらは変更されているいくつかの一般的な関数名、他のユーザーにありますプロジェクト。

* Update```Observable.empty()```に ```empty()```
* Update```Observable.of()```に ```of()```
* Update```.switchMap()```に ```.pipe(switchMap())```
* Update```.map()```に ```.pipe(map())```
* Update```flatMap()```に ```mergeMap()```


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>ランタイムの問題を解決```.map()```と```.filter()```観測可能なオブジェクトに使用する関数

コンパイラは正しく識別できない場合、```observable```オブジェクトの種類、```.map()```と```.filter()```から関数、```array```オブジェクトは、オブジェクトは、実行時にエラーが発生する代わりにマップすることがあります。  関数が返すかどうかを確認、```observable```この問題を回避するために、明示的なデータ型を指定するオブジェクト。

```any``` 戻り値の型がこの問題が発生する、これらのパターンを使用したコードを探します。

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8.その他の一般的な問題を解決するには

これらの手法では、その他の一般的な問題を解決するのに役立ちます。

* 実行```ng lint --fix```lint の一般的な問題を修正するには
* 実行```gulp build```繰り返し増分を解決する問題```gulp build```自動的に解決することができます

## <a name="9-build-and-serve-your-project"></a>9.構築して、プロジェクトを返します

ビルド、最新バージョン (SDK 1.0) で、プロジェクトを提供する次のコマンドを実行します。

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10.ダーク テーマでは、Windows Admin Center で有効にします。

1902 およびそれ以降、Windows Admin Center バージョンにダーク テーマをオンにするには、次の手順に従います。

* 開く Windows Admin Center (1902 およびそれ以降のバージョン)
* をクリックして、**設定**ウィンドウの右上隅のアイコン
* 選択、**詳細** タブ
* [*実験キー*、] をクリックして**追加**
* 新しい値を入力```msft.sme.shell.personalization```前の手順で作成された空のフィールドに
* クリックして**を保存し、再読み込み**
* 設定は、新しいタブに今度は**パーソナル化**します。  このタブを選択します。
* 変更**色**に**ダーク モード (プレビュー)**
