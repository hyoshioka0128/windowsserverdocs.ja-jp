---
title: ツール拡張機能の開発
description: 開発ツールの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1a068c0d33887e8e9287ff15c1aa14f3dc84915a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445935"
---
# <a name="install-extension-payload-on-a-managed-node"></a>拡張機能のペイロードを管理対象ノードにインストールします。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

## <a name="setup"></a>セットアップ
> [!NOTE]
> 1.2.1904.02001 このガイドには、ビルドが必要またはそれ以降。 ビルドを確認するには、数は、Windows Admin Center を開くし、右上にある疑問符をクリックします。

まだインストールしていない場合は、作成、[ツールの拡張機能](../develop-tool.md)Windows Admin Center をします。 この作成が完了した後の拡張機能を作成するときに使用されている値に注意してください。

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso``` |
| ```{!Tool Name}``` | (スペース) を含む、ツール名 | ```InstallOnNode``` |

ツール拡張機能のフォルダー内に作成、```Node```フォルダー (```{!Tool Name}\Node```)。 何もこのフォルダーに配置アドレスは、この API を使用する場合に、管理対象ノードにコピーされます。 ユース ケースに必要な任意のファイルを追加します。 

作成することも、```{!Tool Name}\Node\installNode.ps1```スクリプト。 すべてのファイルをコピーしたら、管理対象ノードに対してこのスクリプトを実行は、```{!Tool Name}\Node```管理ノードにフォルダー。 使用状況に合わせて追加のロジックを追加します。 たとえば```{!Tool Name}\Node\installNode.ps1```ファイル。

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` 特定の名前を検索する API があります。 このファイルの名前を変更すると、エラーが発生します。


## <a name="integration-with-ui"></a>UI との統合

Update```\src\app\default.component.ts```次。

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
プレース ホルダーを拡張機能を作成するときに使用された値に更新します。
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

更新も```\src\app\default.component.html```に。
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

## <a name="creating-and-installing-a-nuget-package"></a>作成して、NuGet パッケージをインストールします。

最後の手順が追加されましたファイルに NuGet パッケージの作成と、Windows Admin Center でそのパッケージをインストールします。

に従って、[拡張機能の公開](../publish-extensions.md)ガイドの前に、拡張機能パッケージを作成していない場合。 
> [!IMPORTANT]
> この拡張機能の .nuspec ファイルのことが重要ですが、```<id>```値が、プロジェクトの名前と一致する```manifest.json```と```<version>```に追加された内容と一致する```\src\app\default.component.ts```。 エントリの下にも追加```<files>```: 
> 
> ```<file src="Node\**\*.*" target="Node" />``` の順にクリックします。

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

このパッケージが作成されると、そのフィードをパスを追加します。 Windows Admin Center の設定 に移動 > 拡張機能 > フィードし、そのパッケージが存在するパスを追加します。 拡張機能が完了すると、インストールされているおく必要がある をクリックして、```install```ボタンと、API が呼び出されます。  