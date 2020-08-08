---
title: ツール拡張機能でカスタムのゲートウェイ プラグインを使用する
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-ツール拡張機能でカスタムゲートウェイプラグインを使用する
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 739b9e6769d1f2314e73a66d932586863063c7be
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952682"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>ツール拡張機能でカスタムのゲートウェイ プラグインを使用する

>適用先:Windows Admin Center、Windows Admin Center Preview

この記事では、Windows 管理センター CLI で作成した新しい空のツール拡張機能でカスタムゲートウェイプラグインを使用します。

## <a name="prepare-your-environment"></a>環境を準備する ##

まだ行っていない場合は、「[ツール拡張機能の開発](../develop-tool.md)」の指示に従って、環境を準備し、新しい空のツール拡張を作成します。

## <a name="add-a-module-to-your-project"></a>モジュールをプロジェクトに追加する ##

新しい[空のモジュール](add-module.md)をプロジェクトに追加していない場合は、次の手順で使用します。

## <a name="add-integration-to-custom-gateway-plugin"></a>カスタムゲートウェイプラグインに統合を追加する ##

ここでは、先ほど作成した新しい空のモジュールでカスタムゲートウェイプラグインを使用します。

### <a name="create-pluginservicets"></a>プラグインの作成. service. ts

上で作成した新しいツールモジュールのディレクトリ () に移動 ```\src\app\{!Module-Name}``` し、新しいファイルを作成し ```plugin.service.ts``` ます。

先ほど作成したファイルに次のコードを追加します。
``` ts
import { Injectable } from '@angular/core';
import { AppContextService, HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Cim, Http, PowerShell, PowerShellSession } from '@microsoft/windows-admin-center-sdk/core';
import { AjaxResponse, Observable } from 'rxjs';

@Injectable()
export class PluginService {
    constructor(private appContextService: AppContextService, private http: Http) {
    }

    public getGatewayRestResponse(): Observable<any> {
        let callUrl = this.appContextService.activeConnection.nodeName;

        return this.appContextService.node.get(callUrl, 'features/Sample%20Uno').map(
            (response: any) => {
                return response;
            }
        )
    }
}
```

およびへの参照を、必要に応じ ```Sample Uno``` ```Sample%20Uno``` て機能名に変更します。

> [!WARNING]
> 組み込みのは、 ```this.appContextService.node``` カスタムゲートウェイプラグインで定義されている API を呼び出すために使用することをお勧めします。 これにより、ゲートウェイプラグイン内で資格情報が要求された場合に、適切に処理されるようになります。

### <a name="modify-modulets"></a>モジュールを変更します。

```module.ts```前の手順で作成した新しいモジュールのファイル (つまり、) を開き ```{!Module-Name}.module.ts``` ます。

次の import ステートメントを追加します。

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

次のプロバイダーを追加します (宣言後)。

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>コンポーネントを変更します。 ts

```component.ts```前の手順で作成した新しいモジュールのファイル (つまり、) を開き ```{!Module-Name}.component.ts``` ます。

次の import ステートメントを追加します。

``` ts
import { ActivatedRouteSnapshot } from '@angular/router';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Subscription } from 'rxjs';
import { Strings } from '../../generated/strings';
import { PluginService } from './plugin.service';
```

次の変数を追加します。

``` ts
  private serviceSubscription: Subscription;
  private responseResult: string;
```

コンストラクターを変更し、次の関数を変更/追加します。

``` ts
  constructor(private appContextService: AppContextService, private plugin: PluginService) {
    //
  }

  public ngOnInit() {
    this.responseResult = 'click go to do something';
  }

  public onClick() {
    this.serviceSubscription = this.plugin.getGatewayRestResponse().subscribe(
      (response: any) => {
        this.responseResult = 'response: ' + response.message;
      },
      (error) => {
        console.log(error);
      }
    );
  }
```

### <a name="modify-componenthtml"></a>component.html を変更する ###

```component.html```前の手順で作成した新しいモジュールのファイル (つまり、) を開き ```{!Module-Name}.component.html``` ます。

次の内容を html ファイルに追加します。
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>拡張機能をビルドしてサイドロードする

これで、Windows 管理センターで拡張機能を[ビルドしてサイドロード](../develop-tool.md#build-and-side-load-your-extension)する準備ができました。
