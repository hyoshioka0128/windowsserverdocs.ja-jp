---
title: ツール拡張機能の開発
description: Windows Admin Center SDK (Project Honolulu) ツール拡張機能を開発します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 2269a2ac2cabda6f8fdd829994f36e89d581bd23
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297011"
---
# 管理ノードでの拡張機能のペイロードをインストールします。

>適用対象: Windows Admin Center、Windows Admin Center Preview

## セットアップ
> [!NOTE]
> 1.2.1904.02001 にこのガイドに従って、ビルド必要以上。 ビルド確認するには、番号が Windows Admin Center を開くし、右上の疑問符 () をクリックします。

まだの場合は、Windows Admin center[ツール拡張機能](../develop-tool.md)を作成します。 このが完了した後、拡張機能を作成するときに使われる値を書き留めます。
| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso``` |
| ```{!Tool Name}``` | (スペース) をツール名 | ```InstallOnNode``` |

ツール拡張機能フォルダー内に作成、```Node```フォルダー (```{!Tool Name}\Node```)。 このフォルダーに配置何もアドレスは、この API を使用する場合に管理ノードにコピーされます。 使用事例に必要なすべてのファイルを追加します。 

作成も、```{!Tool Name}\Node\installNode.ps1```スクリプト。 このスクリプトからすべてのファイルがコピーされる管理ノードで実行は、```{!Tool Name}\Node```管理ノードにフォルダー。 使用事例に、追加のロジックを追加します。 例```{!Tool Name}\Node\installNode.ps1```ファイル。

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` 特定の名前は、API を探しますがいます。 このファイルの名前を変更すると、エラーが発生します。


## UI との統合

更新```\src\app\default.component.ts```次。

``` ts
import { Component } from '@angular/core';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Observable } from 'rxjs';

@Component({
  selector: 'default-component',
  templateUrl: './default.component.html',
  styleUrls: ['./default.component.css']
})

export class DefaultComponent {
  constructor(private appContextService: AppContextService) { }

  public response: any;
  public loading = false;

  public installOnNode() {
    this.loading = true;
    this.post('{!Company Name}.{!Tool Name}', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
  }

  public post(id: string, version: string, targetNode: string): Observable<any> {
    return this.appContextService.node.post(targetNode,
      `features/extensions/${id}/versions/${version}/install`);
  }

}
```
拡張機能を作成するときに使用された値にプレース ホルダーを更新します。
``` ts
this.post('contoso.install-on-node', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
```

更新も```\src\app\default.component.html```します。
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
最後に```\src\app\default.module.ts```:
``` ts
import { CommonModule } from '@angular/common';
import { NgModule } from '@angular/core';

import { LoadingWheelModule } from '@microsoft/windows-admin-center-sdk/angular';
import { DefaultComponent } from './default.component';
import { Routing } from './default.routing';

@NgModule({
  imports: [
    CommonModule,
    LoadingWheelModule,
    Routing
  ],
  declarations: [DefaultComponent]
})
export class DefaultModule { }

```

## 作成して、NuGet パッケージをインストールします。

最後のステップがファイルを追加しました NuGet パッケージを作成し、Windows Admin Center でそのパッケージをインストールします。

前に拡張機能パッケージを作成していない場合は、[[拡張機能の公開](../publish-extensions.md)ガイドに従ってください。 
> [!IMPORTANT]
> この拡張機能の .nuspec ファイルには重要なを```<id>```値が、プロジェクトの名前と一致する```manifest.json```と```<version>```に追加された内容に一致する```\src\app\default.component.ts```します。 下のエントリを追加も```<files>```: 

> ```<file src="Node\**\*.*" target="Node" />```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>contoso.install-on-node</id>
    <version>1.0.0</version>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.install-on-node-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Install on node extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
  </metadata>
    <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
    <file src="Node\**\*.*" target="Node" />
  </files>
</package>
```

このパッケージが作成されると、そのフィードへのパスを追加します。 Windows Admin Center では、設定 _gt _gt フィードの拡張機能に移動し、そのパッケージが存在するパスを追加します。 拡張機能を終了するとき、インストールされることができます] をクリックして、```install```ボタンと API が呼び出されます。  