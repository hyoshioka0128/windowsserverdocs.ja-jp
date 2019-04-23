---
title: ツール拡張機能でカスタムのゲートウェイ プラグインを使用する
description: ツールの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) の作成 - ゲートウェイのカスタム プラグインを使用して、ツールの拡張機能で
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c9b2e9201d58472286b42a9c89a36423f40d143d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834513"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>ツール拡張機能でカスタムのゲートウェイ プラグインを使用する

>適用先:Windows Admin Center、Windows Admin Center プレビュー

この記事では、Windows Admin Center CLI を使用して作成した新しい、空のツールの拡張機能でゲートウェイのカスタム プラグインを使用します。

## <a name="prepare-your-environment"></a>環境の準備 ##

まだインストールしていない場合の手順を実行[ツールの拡張機能を開発](..\develop-tool.md)環境の準備を新規作成は、ツールの拡張機能を空にします。

## <a name="add-a-module-to-your-project"></a>モジュール プロジェクトへの追加します。 ##

まだインストールしていない場合は、新しい追加[空モジュール](add-module.md)をプロジェクトに次の手順で使用します。  

## <a name="add-integration-to-custom-gateway-plugin"></a>カスタム ゲートウェイ プラグインに統合を追加します。 ##

先ほど作成した新しい、空のモジュールでカスタム ゲートウェイ プラグインを使用します。

### <a name="create-pluginservicets"></a>Plugin.service.ts を作成します。

上記で作成した新しいツール モジュールのディレクトリに変更 (```\src\app\{!Module-Name}```)、新しいファイルを作成および```plugin.service.ts```します。

先ほど作成したファイルには、次のコードを追加します。
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

参照を変更する```Sample Uno```と```Sample%20Uno```に応じて、機能名にします。

### <a name="modify-modulets"></a>Module.ts を変更します。

開く、```module.ts```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.module.ts```)。

次の import ステートメントを追加します。

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

(宣言) 後に、次のプロバイダーを追加します。

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>Component.ts を変更します。

開く、```component.ts```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.component.ts```)。

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

コンス トラクターを変更し、次の関数の変更/追加します。

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

### <a name="modify-componenthtml"></a>Component.html を変更します。 ###

開く、```component.html```前に作成した新しいモジュールのファイル (つまり```{!Module-Name}.component.html```)。

次の内容を html ファイルに追加します。
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>ビルドと側は、拡張機能を読み込む

準備ができましたに[ビルドおよび負荷の側](..\develop-tool.md#build-and-side-load-your-extension)Windows Admin Center で、拡張機能。
