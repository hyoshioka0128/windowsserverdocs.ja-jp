---
title: ツール拡張機能にモジュールを追加します。
description: Windows Admin Center SDK (Project Honolulu) ツールの拡張機能の開発 - モジュール ツールの拡張機能を追加します
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: e6978ce20a7c6da8addb217de8d30f733b40d261
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081209"
---
# ツール拡張機能にモジュールを追加します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

この記事では、Windows Admin Center CLI を使用して作成しましたツール拡張機能に、空のモジュールを追加します。

## 環境の準備

まだの場合は、次の環境を準備して、新しい空のツールの拡張機能を作成する[ツール](..\develop-tool.md)(または[ソリューション](..\develop-solution.md)) の拡張機能の開発に指示します。

## Angular CLI を使用して、モジュール (とコンポーネント) を作成するには

Angular を初めて使用する場合は、Angular.Io Web サイトのドキュメントを読み、Angular および NgModule の詳細を確認することを強くお勧めします。 NgModule の詳細については、https://angular.io/guide/ngmodule を参照してください。

* Angular CLI での新しいモジュールの生成の詳細については、https://github.com/angular/angular-cli/wiki/generate-module を参照してください。
* Angular CLI での新しいコンポーネントの生成の詳細については、https://github.com/angular/angular-cli/wiki/generate-component を参照してください。


コマンド プロンプトを開き、プロジェクトで、\src\app をディレクトリに変更し、次のコマンドを実行```{!ModuleName}```使用するモジュール名 (スペースを削除)。

```
cd \src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |

使用例:
```
cd \src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## ルーティングの情報の追加

Angular に慣れていない場合は、Angular のルーティングとナビゲーションの詳細を確認することを強くお勧めします。 次のセクションでは、Windows Admin Center で拡張機能に移動し、ユーザー アクティビティに応じて拡張機能のビュー間を移動できるようにするために必要なルーティング要素を定義します。 詳細については、https://angular.io/guide/router を参照してください。

上記の手順で使用すると同じモジュール名を使用します。

### 新しいルーティング ファイルへのコンテンツの追加

* 前の手順で ``` ng generate ``` によって作成されたモジュール フォルダーを参照します。

* 次の名前付け規則に従い、新しいファイル ```{!module-name}.routing.ts``` を作成します。

    | 値 | 説明 | ファイル名の例 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.routing.ts``` |

* このコンテンツを先ほど作成したファイルに追加します。

    ``` ts
    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { {!ModuleName}Component } from './{!module-name}.component';

    const routes: Routes = [
        {
            path: '',
            component: {!ModuleName}Component,
            // if the component has child components that need to be routed to, include them in the children array.
            children: [
                {
                    path: '', 
                    redirectTo: 'base',
                    pathMatch: 'full'
                }
            ]
    }];

    @NgModule({
        imports: [
            RouterModule.forChild(routes)
        ],
        exports: [
            RouterModule
        ]
    })
    export class Routing { }
    ```

* 作成したファイル内の値を目的の値に置き換えます。

    | 値 | 説明 | 例 |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

### 新しいモジュール ファイルへのコンテンツの追加

次の命名規則で見つかったファイル ```{!module-name}.module.ts``` を開きます。

| 値 | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.module.ts``` |

* コンテンツをファイルに追加します。

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* 追加したコンテンツ内の値を目的の値に置き換えます。

    | 値 | 説明 | 例 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

* ルーティングをインポートするために Imports ステートメントを次のように変更します。

    | 元の値 | 新しい値 |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* ```import``` ステートメントがソースでアルファベット順になっていることを確認します。

### 新しいコンポーネント typescript ファイルへのコンテンツを追加します。

次の命名規則で見つかったファイル ```{!module-name}.component.ts``` を開きます。

| 値 | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.component.ts``` |
    
ファイル内のコンテンツを次に変更します。

``` ts
constructor() {
    // TODO
}

public ngOnInit() {
    // TODO
}
```
### アプリ routing.module.ts を更新します。

ファイルを開く```app-routing.module.ts```、先ほど作成した新しいモジュールが読み込まれますが、既定のパスを変更します。  検索のエントリ```path: ''```、および更新```loadChildren```既定のモジュールではなく、モジュールをロードします。

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

``` ts
    {
        path: '', 
        loadChildren: 'app/{!module-name}/{!module-name}.module#{!ModuleName}Module'
    },
```
更新された既定のパスの例を以下に示します。
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## ビルドとサイドロード拡張機能を読み込む

拡張機能にモジュールを追加するようになりました。  次に、結果を表示する Windows Admin Center で拡張機能[と側のビルドの負荷](..\develop-tool.md#build-and-side-load-your-extension)をできます。
