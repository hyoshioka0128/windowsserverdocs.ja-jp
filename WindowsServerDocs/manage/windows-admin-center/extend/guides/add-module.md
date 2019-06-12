---
title: ツール拡張機能にモジュールを追加する
description: ツールの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) の作成 - ツールの拡張機能にモジュールを追加
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d8d901097eb280679a388ff66161e3514befcd13
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452654"
---
# <a name="add-a-module-to-a-tool-extension"></a>ツール拡張機能にモジュールを追加する

>適用先:Windows Admin Center、Windows Admin Center プレビュー

この記事では、Windows Admin Center CLI を使用して作成したツールの拡張機能に、空のモジュールを追加します。

## <a name="prepare-your-environment"></a>環境の準備

まだインストールしていない場合、手順を実行では、開発、[ツール](../develop-tool.md)(または[ソリューション](../develop-solution.md)) 環境を準備し、新しい空のツールの拡張機能を作成する拡張機能。

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>Angular CLI を使用して、モジュール (およびコンポーネント) を作成するには

Angular を初めて使用する場合は、Angular.Io Web サイトのドキュメントを読み、Angular および NgModule の詳細を確認することを強くお勧めします。 NgModule の詳細については、 https://angular.io/guide/ngmodule を参照してください。

* Angular CLI での新しいモジュールの生成の詳細については、 https://github.com/angular/angular-cli/wiki/generate-module を参照してください。
* Angular CLI での新しいコンポーネントの生成の詳細については、 https://github.com/angular/angular-cli/wiki/generate-component を参照してください。


コマンド プロンプトを開き、\src\app プロジェクトで、ディレクトリを変更し、次のコマンドを実行```{!ModuleName}```をモジュール名 (スペースを削除)。

```
cd \src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |

使用例:
```
cd \src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## <a name="add-routing-information"></a>ルーティングの情報の追加

Angular に慣れていない場合は、Angular のルーティングとナビゲーションの詳細を確認することを強くお勧めします。 次のセクションでは、Windows Admin Center で拡張機能に移動し、ユーザー アクティビティに応じて拡張機能のビュー間を移動できるようにするために必要なルーティング要素を定義します。 詳細については、 https://angular.io/guide/router を参照してください。

上記の手順で使用した同じモジュール名を使用します。

### <a name="add-content-to-new-routing-file"></a>新しいルーティング ファイルへのコンテンツの追加

* 前の手順で ``` ng generate ``` によって作成されたモジュール フォルダーを参照します。

* 次の名前付け規則に従い、新しいファイル ```{!module-name}.routing.ts``` を作成します。

    | Value | 説明 | ファイル名の例 |
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

    | Value | 説明 | 例 |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

### <a name="add-content-to-new-module-file"></a>新しいモジュール ファイルへのコンテンツの追加

次の命名規則で見つかったファイル ```{!module-name}.module.ts``` を開きます。

| Value | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.module.ts``` |

* コンテンツをファイルに追加します。

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* 追加したコンテンツ内の値を目的の値に置き換えます。

    | Value | 説明 | 例 |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

* ルーティングをインポートするために Imports ステートメントを次のように変更します。

    | 元の値 | 新しい値 |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* ```import``` ステートメントがソースでアルファベット順になっていることを確認します。

### <a name="add-content-to-new-component-typescript-file"></a>新しいコンポーネントの typescript ファイルにコンテンツを追加します。

次の命名規則で見つかったファイル ```{!module-name}.component.ts``` を開きます。

| Value | 説明 | ファイル名の例 |
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
### <a name="update-app-routingmodulets"></a>アプリ routing.module.ts を更新します。

ファイルを開く```app-routing.module.ts```、および作成した新しいモジュールが読み込まれますので、既定のパスを変更します。  エントリを探します```path: ''```、および更新```loadChildren```既定モジュールではなく、モジュールを読み込めません。

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | モジュール名 (スペースを削除) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal``` |

``` ts
    {
        path: '', 
        loadChildren: 'app/{!module-name}/{!module-name}.module#{!ModuleName}Module'
    },
```
更新された既定のパスの例を次に示します。
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## <a name="build-and-side-load-your-extension"></a>ビルドと側は、拡張機能を読み込む

拡張機能にモジュールを追加したようになりました。  次に、実行できます[ビルドおよび負荷を側](../develop-tool.md#build-and-side-load-your-extension)結果を表示する Windows Admin Center で、拡張機能。
