---
title: ツール拡張機能でカスタムのゲートウェイ プラグインを使用する
description: Windows Admin Center SDK (Project Honolulu) ツール拡張機能の開発 - ツール拡張機能でカスタムのゲートウェイ プラグインを使用
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4652616478b7b05bde97db48bf84648984b5a325
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296764"
---
# ツール拡張機能でカスタムのゲートウェイ プラグインを使用する

>適用対象: Windows Admin Center、Windows Admin Center Preview

この記事では、Windows Admin Center CLI を使用して作成しますが、新しい空のツールの拡張機能でカスタムのゲートウェイ プラグインを使用します。

## 環境の準備 ##

まだの場合は、[ツールの拡張機能の開発](..\develop-tool.md)環境を準備して、新しい空のツール拡張機能を作成するに指示に従います。

## モジュール、プロジェクトを追加します。 ##

まだの場合、プロジェクトでは、次の手順で使用する新しい[空のモジュール](add-module.md)を追加します。  

## カスタムのゲートウェイ プラグインを統合を追加します。 ##

先ほど作成した新しい、空のモジュールでカスタムのゲートウェイ プラグインを使用します。

### Plugin.service.ts を作成します。

上記で作成された新しいツール モジュールのディレクトリに変更 (```\src\app\{!Module-Name}```)、新しいファイルを作成および```plugin.service.ts```します。

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

参照を変更する```Sample Uno```と```Sample%20Uno```として適切な機能の名前。

[!WARNING]
> 推奨されるで、組み込み```this.appContextService.node```、カスタムのゲートウェイ プラグインで定義されているすべての API を呼び出すために使用します。 これは、ようにする資格情報が適切に処理するゲートウェイ プラグイン内で必要な場合です。

### Module.ts を変更します。

開いている、```module.ts```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.module.ts```)。

次のインポート ステートメントを追加します。

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

(後の宣言) には、次のプロバイダーを追加します。

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### Component.ts を変更します。

開いている、```component.ts```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.component.ts```)。

次のインポート ステートメントを追加します。

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

コンス トラクターを変更し、次の機能の変更/追加します。

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

### Component.html を変更します。 ###

開いている、```component.html```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.component.html```)。

次の内容を html ファイルに追加します。
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## ビルドとサイドロード拡張機能を読み込む

準備が整いました[ビルドとサイドロード負荷](..\develop-tool.md#build-and-side-load-your-extension)に Windows Admin Center で拡張機能です。
