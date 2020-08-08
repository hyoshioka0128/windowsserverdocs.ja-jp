---
title: ツール拡張機能にモジュールを追加する
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-ツール拡張機能へのモジュールの追加
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: e7875f8aa2320d7292b314cb18f3e17894e76fa0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945045"
---
# <a name="add-a-module-to-a-tool-extension"></a>ツール拡張機能にモジュールを追加する

>適用先:Windows Admin Center、Windows Admin Center Preview

この記事では、Windows 管理センター CLI で作成したツール拡張機能に空のモジュールを追加します。

## <a name="prepare-your-environment"></a>環境を準備する

まだ行っていない場合は、「[ツール](../develop-tool.md)(または[ソリューション](../develop-solution.md)) の拡張機能の開発」の指示に従って、環境を準備し、新しい空のツール拡張を作成します。

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>角 CLI を使用してモジュール (およびコンポーネント) を作成する

Angular を初めて使用する場合は、Angular.Io Web サイトのドキュメントを読み、Angular および NgModule の詳細を確認することを強くお勧めします。 NgModule の詳細については、https://angular.io/guide/ngmodule を参照してください。

* Angular CLI での新しいモジュールの生成の詳細については、https://github.com/angular/angular-cli/wiki/generate-module を参照してください。
* Angular CLI での新しいコンポーネントの生成の詳細については、https://github.com/angular/angular-cli/wiki/generate-component を参照してください。


コマンドプロンプトを開き、プロジェクトのディレクトリを-src\ app に変更してから、次のコマンドを実行します ```{!ModuleName}``` 。をモジュール名 (スペースが削除されたもの) に置き換えます。

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


## <a name="add-routing-information"></a>ルーティングの情報の追加

Angular に慣れていない場合は、Angular のルーティングとナビゲーションの詳細を確認することを強くお勧めします。 次のセクションでは、Windows Admin Center で拡張機能に移動し、ユーザー アクティビティに応じて拡張機能のビュー間を移動できるようにするために必要なルーティング要素を定義します。 詳細については、https://angular.io/guide/router を参照してください。

前の手順で使用したのと同じモジュール名を使用します。

### <a name="add-content-to-new-routing-file"></a>新しいルーティング ファイルへのコンテンツの追加

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

### <a name="add-content-to-new-module-file"></a>新しいモジュール ファイルへのコンテンツの追加

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

### <a name="add-content-to-new-component-typescript-file"></a>新しいコンポーネント typescript ファイルにコンテンツを追加する

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
### <a name="update-app-routingmodulets"></a>App-v を更新します。

ファイル ```app-routing.module.ts``` を開き、作成した新しいモジュールが読み込まれるように、既定のパスを変更します。  のエントリを検索 ```path: ''``` し、を更新して、既定のモジュールで ```loadChildren``` はなくモジュールを読み込みます。

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
次に、更新された既定のパスの例を示します。
``` ts
    {
        path: '',
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## <a name="build-and-side-load-your-extension"></a>拡張機能をビルドしてサイドロードする

これで、拡張機能にモジュールを追加しました。  次に、Windows 管理センターで拡張機能を[ビルドしてサイドロード](../develop-tool.md#build-and-side-load-your-extension)し、結果を確認することができます。
