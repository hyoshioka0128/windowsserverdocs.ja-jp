---
title: ツール拡張機能でカスタムのゲートウェイ プラグインを使用する
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-ツール拡張機能でカスタムゲートウェイプラグインを使用する
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 829cbf6df8cc2738bf4066b36210b860595774ed
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385232"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>ツール拡張機能でカスタムのゲートウェイ プラグインを使用する

>適用対象: Windows Admin Center、Windows Admin Center Preview

この記事では、Windows 管理センター CLI で作成した新しい空のツール拡張機能でカスタムゲートウェイプラグインを使用します。

## <a name="prepare-your-environment"></a>環境の準備 ##

まだ行っていない場合は、「[ツール拡張機能の開発](../develop-tool.md)」の指示に従って、環境を準備し、新しい空のツール拡張を作成します。

## <a name="add-a-module-to-your-project"></a>モジュールをプロジェクトに追加する ##

新しい[空のモジュール](add-module.md)をプロジェクトに追加していない場合は、次の手順で使用します。  

## <a name="add-integration-to-custom-gateway-plugin"></a>カスタムゲートウェイプラグインに統合を追加する ##

ここでは、先ほど作成した新しい空のモジュールでカスタムゲートウェイプラグインを使用します。

### <a name="create-pluginservicets"></a>プラグインの作成. service. ts

上で作成した新しいツールモジュール (```\src\app\{!Module-Name}```) のディレクトリに移動し、新しいファイル ```plugin.service.ts```を作成します。

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

```Sample Uno``` への参照を変更し、必要に応じて機能名に ```Sample%20Uno``` します。

[!WARNING]
> 組み込みの ```this.appContextService.node``` は、カスタムゲートウェイプラグインで定義されている API を呼び出すために使用することをお勧めします。 これにより、ゲートウェイプラグイン内で資格情報が要求された場合に、適切に処理されるようになります。

### <a name="modify-modulets"></a>モジュールを変更します。

前の手順で作成した新しいモジュール (```{!Module-Name}.module.ts```) の ```module.ts``` ファイルを開きます。

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

前の手順で作成した新しいモジュール (```{!Module-Name}.component.ts```) の ```component.ts``` ファイルを開きます。

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

### <a name="modify-componenthtml"></a>コンポーネント .html を変更する ###

前の手順で作成した新しいモジュール (```{!Module-Name}.component.html```) の ```component.html``` ファイルを開きます。

次の内容を html ファイルに追加します。
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>拡張機能をビルドしてサイドロードする

これで、Windows 管理センターで拡張機能を[ビルドしてサイドロード](../develop-tool.md#build-and-side-load-your-extension)する準備ができました。
