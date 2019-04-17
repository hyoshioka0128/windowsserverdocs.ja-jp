---
title: Windows Admin Center SDK 0.1 ~ 1.0 からの移行します。
description: このガイドは Windows Admin Center SDK バージョン 1.0 を 0.1 から移行する場合に役立ちます
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ba0e8cda35c51763b5c10b89c76e2bf07e064dfd
ms.sourcegitcommit: 10d7606a5c2a1ddb234af597f199b6779b0058d4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2019
ms.locfileid: "9116588"
---
# Windows Admin Center SDK 0.1 ~ 1.0 からの移行します。

>適用対象: Windows Admin Center Preview

このガイドは Windows Admin Center SDK バージョン 1.0 を 0.1 から移行する場合に役立ちます。  

## 1. デベロッパー ガイド拡張子を持つ新しいコントロールについて説明します。

Windows Admin Center 1902 以降のバージョンには、コントロール (新しく利用可能なコントロールを含む) と、独自の拡張機能を構築するためのシナリオの例を検索するために使用できる**デベロッパー ガイド**拡張機能が含まれています。  開発ガイドには、以前のバージョンの SDK から**開発者ツール**の拡張機能が置き換えられます。

### Windows Admin Center でデベロッパー ガイドを使用します。

デベロッパー ガイドでは、Windows Admin Center バージョン 1902 ソリューションとして利用可能なおよびそれ以降でです。  デベロッパー ガイドは、プレインストールされているが、設定を通じて有効にする必要があります。

**Windows Admin Center でデベロッパー ガイドを有効にします。**

* オープン Windows Admin Center (バージョン 1902 以降)
* ウィンドウの右上隅にある**設定**アイコンをクリックします。
* **詳細設定**] タブを選択します。
* *実験のキー*は、[**追加**を] をクリックします。
* 新しい値を入力```msft.sme.shell.devguide```で、前の手順で作成された、空のフィールド
* [**保存して再読み込み**

**Windows Admin Center では、デベロッパー ガイドを開きます。**

* オープン Windows Admin Center (バージョン 1902 以降)
* 左上にあるすべてのソリューションの種類を表示するにはドロップダウンをクリックします。
* **デベロッパー ガイド**ソリューションを選択します。 
    * ソリューションの一覧が表示されない場合、は、デベロッパー ガイドが有効になっていることを確認してください (前のセクションをご覧ください)、Windows Admin Center が再読み込みします。
* タブのいずれかを選択することによってデベロッパー ガイドの内容を参照します。
    * **ランディング:***[管理*と*通知*のシナリオのコード サンプルが含まれています
    * **コントロール:** SDK で利用可能な各コントロールの例を示します
    * **パイプ:** 利用可能なコンバーターとフォーマッタ関数の例が含まれています
    * **スタイル:** SDK で利用可能な CSS スタイルの例が含まれています
    * **MsftSme:** 例や高度なシナリオのガイダンスが含まれています 

### GitHub でデベロッパー ガイドのソース コードを参照します。

HTML、CSS、および TypeScript サンプルのコード例を検索する github デベロッパー ガイドの[ソース コード](https://github.com/Microsoft/windows-admin-center-sdk/)を参照することができます。

## 2. 最新の SDK の開発環境を準備します。

インストールまたは更新 node.js バージョン[10.15.1 LTS またはそれ以降](https://nodejs.org/en/)します。

Windows Admin Center CLI を最新のバージョンに更新します。

[//]: # "npm-g windows-admin-center-cli@next をアンインストールします。"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

これらのバージョンをグローバルの依存関係を更新します。

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## 3. 最新の SDK を使って新しいプロジェクトを作成します。

ターゲットと新しいプロジェクトを作成する際の Windows Admin Center CLI を使用して、```next```バージョン (SDK 1.0)。

[//]: # "作成した wac--会社 'Contoso Inc-' '管理 Foo 動作'--試験的なバージョンのツール"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

次に、先ほど作成したフォルダーにディレクトリを変更し、必要なローカルの依存関係を実行して、インストール```npm install ```します。

## 4. 最新の SDK を使用して既存のプロジェクトを変更します。

重要: 続行する前に、プロジェクトのバックアップを作成します。

次の行を変更```package.json```ターゲットに、```next```バージョン (SDK 1.0)。

[//]: # "'@microsoft/windows-admin-center-sdk': '試験的な'"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

実行し、 ```npm install``` 、プロジェクト全体で参照を更新します。

## 5. SDK CLI を使用して移行の一般的な問題を解決します。

重要: 続行する前に、プロジェクトのバックアップを作成します。

プロジェクトのルート フォルダーから自動的に移行の一般的な問題を解決するプロジェクトで次の CLI コマンドを実行します。

``` cmd
wac updateSeven --update
```

この CLI コマンドは、次の問題を自動的に説明します。

* 再生成します。 ```package-lock.json```
* Angular コンパイル環境でファイルを更新します。
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## 6. SDK CLI を使用して移行の一般的な問題を理解します。

プロジェクトのルート フォルダーから、プロジェクトを監査し、手動で対処する必要がある一般的な移行の問題を見つけるには、次の CLI コマンドを実行します。

``` cmd
wac updateSeven --audit
```

これにより、プロジェクトで次の問題のインスタンスが検索します。

### これらの sme クラスに次の CSS クラスの使用状況を置き換えます。

| 古い CSS クラス | 新しい CSS クラス |
| -- | -- |
| .auto 規模柔軟 |  .sme 位置柔軟自動 |
| .border すべて |  .sme 境界線インセット sm と .sme-境界線の色の基本-90 |
| .border 下 |  .sme 境界線下部 sm と .sme-border-bottom-color-base-90 |
| 水平方向の .border |  .sme 境界線水平 sm と .sme-border-horizontal-color-base-90 |
| .border 左 |  .sme 境界線左 sm と .sme-border-left-color-base-90 |
| .border 右 |  .sme 境界線右 sm と .sme-border-right-color-base-90 |
| .border 上部 |  .sme 境界線上部 sm と .sme-border-top-color-base-90 |
| 垂直方向の .border |  .sme 境界線垂直 sm と .sme-border-vertical-color-base-90 |
| .break word |  .sme の配置の ws の折り返し |
| .btn |  .sme ボタンまたはボタン |
| .btn プライマリ |  .sme button.sme ボタン プライマリ OR.button.sme-ボタン-プライマリ |
| .color 濃色 |  .sme 色 alt キーを |
| .color 光 |  .sme ベースの色 |
| .color-明るい灰色 |  .sme 色 base 90 |
| .fixed 規模柔軟 |  .sme-位置に柔軟になし |
| .flex レイアウト |  .sme 配置-スタック--h または .sme 配置-スタック-v |
| .font 太字 |  .sme-フォント-斜体 1 |
| .highlight |  .sme 背景色黄色 |
| .horizontal |  .sme 配置-スタック--h |
| .no スクロール |  .sme 位置柔軟自動 |
| .nowrap |  .sme 配置-スタック--h または .sme 配置-スタック-v |
| .relative |  .sme の相対レイアウト |
| .relative センター |  絶対レイアウト .sme .sme 位置センター |
| .reverse |  .sme 配置-スタックの反転 |
| .stretch 絶対 |  .sme レイアウトの絶対 .sme-位置-インセット-なし |
| .stretch 固定 |  固定レイアウト .sme .sme-位置-インセット-なし |
| 垂直方向の .stretch |  .sme 位置 stretch v |
| .stretch 幅 |  .sme 位置 stretch h |
| .vertical |  .sme 配置-スタック-v |
| .vertical スクロールのみ |  .sme-配置-オーバーフローの非表示にする-sme の配置のオーバーフロー-自動-x-y |
| .wrap |  .sme 配置-wrapstack--h または .sme 配置-wrapstack-v |

### これらの sme コンポーネントと、次のコンポーネントの使用状況を置き換えます。

| 古いコンポーネント | 新しいコンポーネント |
| -- | -- |
| .alert |  sme アラート |
| .alert 危険 |  sme アラート |
| .breadCrumb |  sme アラート |
| .checkbox |  sme フォーム フィールド [種類] チェック ボックスをオン"=] |
| .combobox |  sme フォーム フィールド [型 =「選択」] |
| .dashboard |  sme をレイアウトのコンテンツのゾーンに埋め込まれた sme 配置-スタック--h |
| .details パネル |  sme プロパティのグリッド |
| .details からパネル コンテナー |  sme プロパティのグリッド |
| .details] タブ |  sme プロパティのグリッド OR sme-pivot |
| .details ラッパー |  sme プロパティのグリッド |
| .disabled |  sme 無効 |
| .form ボタン | sme フォーム フィールド |
| .form コントロール | sme フォーム フィールド |
| .form コントロール | sme フォーム フィールド |
| .form グループ | sme フォーム フィールド |
| .form グループのラベル | sme フォーム フィールド |
| .form 入力 | sme フォーム フィールド |
| .form stretch | sme フォーム フィールド |
| .input ファイル | sme フォーム フィールド |
| 複数のタブに移動 |  sme ピボット |
| .radio |  sme フォーム フィールド [型 =「オプション」] |
| .required 手掛かり | sme フォーム フィールド |
| .searchbox |  sme フォーム フィールド [型 =「検索」] |
| .toggle スイッチ |  sme フォーム フィールド [型 =「トグル スイッチ」] |
| .tool コンテナー |  sme レイアウト コンテンツ ゾーンまたは sme をレイアウトのコンテンツのゾーンに埋め込まれました。 |

### これらの CSS クラスは推奨されなくなり、現在サポートされていません。

| 古いクラス | 非推奨 |
| -- | -- |
| .acceptable | (非推奨) |
| .color エラー | (非推奨) |
| .color 情報 | (非推奨) |
| .color 成功 | (非推奨) |
| .color 警告 | (非推奨) |
| .delete ボタン | (非推奨) |
| .details コンテンツ | (非推奨) |
| カバー | (非推奨) |
| メッセージ | (非推奨) |
| .guided ウィンドウのボタン | (非推奨) |
| .header コンテナー | (非推奨) |
| .icon win | (非推奨) |
| .indent | (非推奨) |
| .invalid | (非推奨) |
| 追加されて一覧 | (非推奨) |
| .modal スクロール可能です | (非推奨) |
| 。 マルチ セクション | (非推奨) |
| .no-アクション バー | (非推奨) |
| .overflow 余白 | (非推奨) |
| .overflow ツール | (非推奨) |
| .progress カバー | (非推奨) |
| .right パネル | (非推奨) |
| .rollup | (非推奨) |
| .rollup 状態 | (非推奨) |
| .rollup タイトル | (非推奨) |
| .rollup 値 | (非推奨) |
| .searchbox-アクション バー | (非推奨) |
| .size-h-1 | (非推奨) |
| .size-h-2 | (非推奨) |
| .size-h-3 | (非推奨) |
| .size-h-4 | (非推奨) |
| .size h"完全" | (非推奨) |
| 半分半分 h .size | (非推奨) |
| .size-v-1 | (非推奨) |
| .size-v-2 | (非推奨) |
| .size-v-3 | (非推奨) |
| .size-v-4 | (非推奨) |
| .status アイコン | (非推奨) |
| .svg 残す | (非推奨) |
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
| .usage バーの領域 | (非推奨) |
| バック グラウンド バー .usage | (非推奨) |
| .usage のタイトル バー | (非推奨) |
| .usage バリュー バー | (非推奨) |
| .usage グラフ | (非推奨) |
| .usage メッセージ | (非推奨) |
| .usage メッセージ領域 | (非推奨) |
| .usage メッセージのタイトル | (非推奨) |
| .warning | (非推奨) |
| .white 領域 | (非推奨) |

## 7. 理解し、監視可能なオブジェクトの問題を解決します。

### 更新```rxjs```動作の監視可能なオブジェクトの使用

これらは、変更されているいくつかの一般的な関数名、他のユーザーにありますプロジェクトします。

* 更新```Observable.empty()```する ```empty()```
* 更新```Observable.of()```する ```of()```
* 更新```.switchMap()```する ```.pipe(switchMap())```
* 更新```.map()```する ```.pipe(map())```
* 更新```flatMap()```する ```mergeMap()```


### 実行時の問題を解決する```.map()```と```.filter()```監視可能なオブジェクト上の関数

コンパイラを正しく識別できない場合、```observable```オブジェクトの種類、```.map()```と```.filter()```から機能、```array```オブジェクトは、オブジェクトは、実行時にエラーが発生する代わりにマップする可能性があります。  関数を返すことを確認する```observable```オブジェクトをこの問題を回避するために、明示的なデータ型を指定します。

```any``` 戻り値の型がこの問題が発生する、これらのパターンを使ったコードを探します。

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## 8. 他の一般的な問題を解決します。

これらの手法は他の一般的な問題の解決に役立ちます。

* 実行```ng lint --fix```柔らかいの一般的な問題を解決するには
* 実行```gulp build```繰り返しを修正する段階的に問題を```gulp build```自動的に解決することができます

## 9. をビルドし、プロジェクトを提供

ビルドし、最新のバージョン (SDK 1.0) で、プロジェクトを提供するには、次のコマンドを実行します。

``` cmd
gulp build
gulp serve --port 4201
```

## 10. Windows Admin Center で濃色のテーマを有効にします。

1902 以降、Windows Admin Center バージョンで濃色のテーマをオンにするには、次の手順に従います。

* オープン Windows Admin Center (バージョン 1902 以降)
* ウィンドウの右上隅にある**設定**アイコンをクリックします。
* **詳細設定**] タブを選択します。
* *実験のキー*は、[**追加**を] をクリックします。
* 新しい値を入力```msft.sme.shell.personalization```で、前の手順で作成された、空のフィールド
* [**保存して再読み込み**
* 新しいタブ]、 **[パーソナル設定]** が設定されます。  このタブを選択します。
* **ダーク モード (プレビュー)** に**色**の変更します。
