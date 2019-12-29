---
title: Windows 管理センター SDK 0.1 から1.0 への移行
description: このガイドでは、Windows 管理センター SDK バージョン0.1 から1.0 に移行する方法について説明します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 02/26/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c52870178e7caff0abc8ddcccc62966d637dd3c9
ms.sourcegitcommit: ac9946deb4fa70203a9b05e0386deb4244b8ca55
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2019
ms.locfileid: "71357059"
---
# <a name="migrate-from-windows-admin-center-sdk-01-to-10"></a>Windows 管理センター SDK 0.1 から1.0 への移行

>適用対象: Windows 管理センタープレビュー

このガイドでは、Windows 管理センター SDK バージョン0.1 から1.0 に移行する方法について説明します。  

## <a name="1-learn-about-new-controls-with-the-dev-guide-extension"></a>1. 開発ガイド拡張機能を使用した新しいコントロールについて説明します。

Windows 管理センターバージョン1902以降には、**開発ガイド**の拡張機能が含まれています。この拡張機能を使用して、コントロールの例 (新しく使用できるコントロールを含む) や、独自の拡張機能の構築に役立つシナリオを見つけることができます。  **開発者ツール**拡張機能は、以前のバージョンの SDK からの開発ガイドで置き換えられています。

### <a name="use-the-dev-guide-in-windows-admin-center"></a>Windows 管理センターの開発ガイドを使用する

開発ガイドは、Windows 管理センターバージョン1902以降のソリューションとして提供されています。  開発ガイドはプレインストールされていますが、設定を使用して有効にする必要があります。

**Windows 管理センターで開発ガイドを有効にする:**

* Windows 管理センター (バージョン1902以降) を開きます。
* ウィンドウの右上隅にある**設定**アイコンをクリックします。
* **[詳細設定]** タブを選択します。
* [*実験キー*] で、 **[追加]** をクリックします。
* 前の手順で作成した空のフィールドに ```msft.sme.shell.devguide``` 新しい値を入力します。
* [**保存して再読み込み] を**クリックします。

**Windows 管理センターで開発ガイドを開く:**

* Windows 管理センター (バージョン1902以降) を開きます。
* 左上のドロップダウンをクリックして、すべてのソリューションの種類を表示します
* **開発ガイド**ソリューションを選択する 
    * ソリューションが表示されない場合は、開発ガイドを有効にしていることを確認し (上記のセクションを参照)、Windows 管理センターを再読み込みしてください。
* 開発ガイドの内容を参照するには、いずれかのタブを選択します。
    * **ランディング:** *管理*および*通知*シナリオのコードサンプルが含まれています
    * **コントロール:** SDK で使用可能な各コントロールの例が含まれています。
    * **パイプ:** 使用できるコンバーターおよびフォーマッタ関数の例が含まれています。
    * **スタイル:** SDK で使用できる CSS スタイルの例が含まれています。
    * **MsftSme:** 高度なシナリオの例とガイダンスが含まれています。 

### <a name="browse-the-source-code-of-dev-guide-on-github"></a>GitHub の開発ガイドのソースコードを参照する

GitHub の開発ガイドの[ソースコード](https://github.com/Microsoft/windows-admin-center-sdk/)を参照して、サンプルの HTML、CSS、TypeScript コードサンプルを見つけることができます。

## <a name="2-prepare-your-development-environment-for-the-latest-sdk"></a>2. 最新の SDK の開発環境を準備する

Node.js バージョン[10.15.1 LTS](https://nodejs.org/en/)以降をインストールまたは更新します。

Windows 管理センター CLI を最新バージョンに更新します。

[//]: # "npm uninstall-g windows-admin-center-cli@next"

``` cmd
npm uninstall -g windows-admin-center-cli
npm install -g windows-admin-center-cli
```

グローバル依存関係を次のバージョンに更新します。

``` cmd
npm install npm@6.4.1 -g
npm install @angular/cli@7.1.2 -g
npm install gulp -g
npm install typescript@3.1.6 -g
npm install tslint@5.11.0 -g
```

## <a name="3-create-a-new-project-with-the-latest-sdk"></a>3. 最新の SDK を使用して新しいプロジェクトを作成する

Windows 管理センター CLI を使用して、```next``` バージョン (SDK 1.0) を対象とする新しいプロジェクトを作成します。

[//]: # "wac create--company ' Contoso Inc. '--tool ' Manage Foo Works '--バージョンの試験段階"

``` cmd
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version next
```

次に、先ほど作成したフォルダーにディレクトリを変更し、```npm install ```を実行して、必要なローカルの依存関係をインストールします。

## <a name="4-modify-an-existing-project-to-use-the-latest-sdk"></a>4. 最新の SDK を使用するように既存のプロジェクトを変更する

重要: 続行する前に、プロジェクトのバックアップを作成してください。

```package.json``` の次の行を変更して、```next``` バージョン (SDK 1.0) をターゲットにします。

[//]: # "'@microsoft/windows-admin-center-sdk': ' 実験的 '"

``` json
"@microsoft/windows-admin-center-sdk": "next",
```

次に、```npm install``` を実行して、プロジェクト全体で参照を更新します。

## <a name="5-use-the-sdk-cli-to-fix-common-migration-issues"></a>5. SDK CLI を使用して、移行に関する一般的な問題を修正する

重要: 続行する前に、プロジェクトのバックアップを作成してください。

プロジェクトのルートフォルダーから、次の CLI コマンドをプロジェクトで実行し、移行に関する一般的な問題を自動的に修正します。

``` cmd
wac updateSeven --update
```

この CLI コマンドは、次の問題に自動的に対処します。

* 再生成 ```package-lock.json```
* 角度コンパイル環境でファイルを更新します。
    - ```.gitignore```
    - ```tslint.json```
    - ```tsconfig.json```
    - ```tsconfig.inline.json```
    - ```ng-package.json```
    - ```angular.json```
    - ```src\tsconfig.app.json```
    - ```src\tsconfig.lib.json```
    - ```src\tsconfig.spec.json```

## <a name="6-use-the-sdk-cli-to-understand-common-migration-issues"></a>6. SDK CLI を使用して、移行に関する一般的な問題を理解する

プロジェクトのルートフォルダーから、次の CLI コマンドを実行してプロジェクトを監査し、手動で対処する必要がある一般的な移行の問題を見つけます。

``` cmd
wac updateSeven --audit
```

これにより、プロジェクトで次の問題のインスタンスが検出されます。

### <a name="replace-usage-of-the-following-css-classes-with-these-sme-classes"></a>これらの sme クラスを使用して、次の CSS クラスを置き換えます。

| 以前の CSS クラス | 新しい CSS クラス |
| -- | -- |
| 。自動フレックスサイズ |  . sme-position-flex-auto |
| 。罫線-すべて |  . sme-枠線と、sme-border-color-90 |
| 。罫線-下 |  . sme-ボーダー-底-sm、および sme-ボーダー-底-90 |
| 。罫線-横 |  . sme-ボーダー-横-sm および sme-枠線-水平色-90 |
| 。罫線-左 |  . sme-罫線-左-sm および sme-罫線-左-90 |
| 。罫線-右 |  . sme-罫線-右-sm、sme-境界線、右側-90 |
| 。罫線-上 |  . sme-ボーダー-トップ-sm および sme-枠線-基本色-90 |
| 。罫線-縦 |  . sme-ボーダー-横-sm および sme-罫線-縦-カラー-90 |
| . break-word |  . sme-wrap |
| .btn |  . sme-ボタンまたはボタン |
| . btn-プライマリ |  . sme-button-button-primary または............ |
| 。色-濃色 |  . sme-color-alt |
| . color-薄い |  . sme-color-base |
| . color-淡い-灰色 |  . sme-base-90 |
| 。固定のフレックスサイズ |  . sme-position-flex-なし |
| . flex-レイアウト |  . sme-stack-h または sme-stack-v |
| . font-bold |  sme-emphasis1 |
| 。強調表示 |  sme-背景色-黄 |
| 。横方向 |  . sme-stack-h |
| . なし-スクロール |  . sme-position-flex-auto |
| nowrap |  . sme-stack-h または sme-stack-v |
| 。相対 |  . sme-layout-相対 |
| . 相対中心 |  . sme-layout-完全な sme-位置-中央 |
| 。逆 |  . sme-積み重ね-反転 |
| . stretch-絶対 |  . sme-layout-(完全な sme-位置-埋め込み-なし) |
| . stretch-固定 |  . sme-layout-fixed-inset-none |
| . stretch-縦 |  . sme-position-stretch-v |
| . stretch-幅 |  . sme-position-stretch-h |
| . vertical |  . sme-stack-v |
| . vertical-スクロールのみ |  . sme-overflow-非表示-x sme-配置-オーバーフロー-自動-y |
| . wrap |  wrapstack-h または wrapstack-v のようになります。 |

### <a name="replace-usage-of-the-following-components-with-these-sme-components"></a>次のコンポーネントの使用を、これらの sme コンポーネントに置き換えます。

| 古いコンポーネント | 新しいコンポーネント |
| -- | -- |
| 。アラート |  sme-アラート |
| . alert-危険 |  sme-アラート |
| . 階層リンク |  sme-アラート |
| . checkbox |  sme-フォームフィールド [type = "checkbox"] |
| . combobox |  sme-フォームフィールド [type = "select"] |
| . ダッシュボード |  sme-レイアウト-コンテンツ-ゾーンに埋め込まれる sme-スタック-h |
| . details-panel |  sme-プロパティ-グリッド |
| . details-panel-container |  sme-プロパティ-グリッド |
| . details-tab |  sme-プロパティ-グリッドまたは sme-ピボット |
| . details-ラッパー |  sme-プロパティ-グリッド |
| 。 disabled |  sme-無効 |
| . フォーム-ボタン | sme-フォームフィールド |
| . フォーム-コントロール | sme-フォームフィールド |
| . フォーム-コントロール | sme-フォームフィールド |
| . フォーム-グループ | sme-フォームフィールド |
| . フォーム-グループ-ラベル | sme-フォームフィールド |
| . フォーム-入力 | sme-フォームフィールド |
| . フォーム-stretch | sme-フォームフィールド |
| 。入力-ファイル | sme-フォームフィールド |
| . nav-タブ |  sme-ピボット |
| . radio |  sme-フォームフィールド [type = "radio"] |
| . 必須-手掛かり | sme-フォームフィールド |
| ... |  sme-フォームフィールド [type = "search"] |
| . トグル-スイッチ |  sme-フォームフィールド [type = "トグルスイッチ"] |
| . ツール-コンテナー |  sme-レイアウト-ゾーンまたは sme-コンテンツ-ゾーンに埋め込まれる |

### <a name="these-css-classes-are-deprecated-and-are-no-longer-supported"></a>これらの CSS クラスは非推奨とされており、現在サポートされていません。

| Old クラス | 非推奨 |
| -- | -- |
| 。許容される | れ |
| . color-エラー | れ |
| . color-info | れ |
| 。色-成功 | れ |
| 。色-警告 | れ |
| . delete-button | れ |
| 。詳細-コンテンツ | れ |
| 。エラー-表紙 | れ |
| . エラー-メッセージ | れ |
| 。ガイド付きウィンドウ-ボタン | れ |
| . header-コンテナー | れ |
| . icon-win | れ |
| . インデント | れ |
| 。無効 | れ |
| 。項目一覧 | れ |
| . モーダル-スクロール可能 | れ |
| . マルチセクション | れ |
| .-アクションバー | れ |
| 。オーバーフロー-余白 | れ |
| . オーバーフロー-ツール | れ |
| 。進行状況-カバー | れ |
| 。右パネル | れ |
| 。ロールアップ | れ |
| ロールアップ-状態 | れ |
| 。 rollup-title | れ |
| 。 rollup-値 | れ |
| ...-アクションバー | れ |
| . size-h-1 | れ |
| . size-h-2 | れ |
| . size-h-3 | れ |
| . size-h-4 | れ |
| . size-h-full | れ |
| . size-1/2 | れ |
| . size-v-1 | れ |
| . size-v-2 | れ |
| . size-v-3 | れ |
| . size-v-4 | れ |
| . status-アイコン | れ |
| svg-16px | れ |
| 。テーブル-インデント | れ |
| . table-sm | れ |
| . thin | れ |
| 。タイル | れ |
| 。タイル-本文 | れ |
| . タイル-コンテンツ | れ |
| 。タイル-フッター | れ |
| . tile-ヘッダー | れ |
| 。タイル-レイアウト | れ |
| . tile-テーブル | れ |
| . ツールバー | れ |
| . ツールバー | れ |
| . ツールヘッダー | れ |
| . ツールヘッダー-ボックス | れ |
| . ツール-ウィンドウ | れ |
| . 使用状況-バー | れ |
| 。使用状況バー-領域 | れ |
| . 使用状況-バー-背景 | れ |
| . usage-bar-title | れ |
| 。使用状況-棒-値 | れ |
| . 使用状況-グラフ | れ |
| . usage-message | れ |
| . usage-message-area | れ |
| . usage-message-title | れ |
| 。警告 | れ |
| 。空白 | れ |

## <a name="7-understand-and-resolve-issues-with-observable-objects"></a>7. 監視可能なオブジェクトに関する問題を理解し、解決する

### <a name="update--rxjs-function-use-for-observable-objects"></a>観測可能なオブジェクトの ```rxjs``` 関数の使用を更新する

これらは、変更されたいくつかの一般的な関数の名前であり、プロジェクト内に他の関数名が存在する可能性があります。

* ```empty()``` への ```Observable.empty()``` の更新
* ```of()``` への ```Observable.of()``` の更新
* ```.pipe(switchMap())``` への ```.switchMap()``` の更新
* ```.pipe(map())``` への ```.map()``` の更新
* ```mergeMap()``` への ```flatMap()``` の更新


### <a name="resolve-runtime-issues-with-map-and-filter-functions-on-observable-objects"></a>監視可能なオブジェクトの ```.map()``` および ```.filter()``` 関数に関する実行時の問題を解決する

コンパイラが ```observable``` オブジェクトの型を正しく識別できない場合は、```array``` オブジェクトの関数 ```.map()``` と ```.filter()``` がオブジェクトにマップされ、実行時にエラーが発生する可能性があります。  この問題を回避するには、関数が明示的なデータ型を指定する ```observable``` オブジェクトを返すようにします。

```any``` 戻り値の型がないと、この問題が発生する可能性があります。次のパターンでコードを探してください。

``` ts
public getMyObservable(): any { //any return type can cause issues
 ...
}

public getMyObservable() { //no return type can cause issues
...
}
```

## <a name="8-resolve-other-common-issues"></a>8. その他の一般的な問題を解決する

これらの手法は、その他の一般的な問題を解決するのに役立ちます。

* ```ng lint --fix``` を実行して、糸くずに関する一般的な問題を修正します
* ```gulp build``` によって自動的に解決される問題を段階的に修復するには ```gulp build``` を繰り返し実行します

## <a name="9-build-and-serve-your-project"></a>9. プロジェクトをビルドしてサービスを提供する

次のコマンドを実行して、最新バージョン (SDK 1.0) でプロジェクトをビルドし、サービスを提供します。

``` cmd
gulp build
gulp serve --port 4201
```

## <a name="10-turn-on-dark-theme-in-windows-admin-center"></a>10. Windows 管理センターでダークテーマを有効にする

Windows 管理センターバージョン1902以降でダークテーマを有効にするには、次の手順を実行します。

* Windows 管理センター (バージョン1902以降) を開きます。
* ウィンドウの右上隅にある**設定**アイコンをクリックします。
* **[詳細設定]** タブを選択します。
* [*実験キー*] で、 **[追加]** をクリックします。
* 前の手順で作成した空のフィールドに ```msft.sme.shell.personalization``` 新しい値を入力します。
* [**保存して再読み込み] を**クリックします。
* 設定に新しいタブ [**個人用**設定] が追加されました。  このタブを選択します
* **色**を濃色モードに変更する **(プレビュー)**
