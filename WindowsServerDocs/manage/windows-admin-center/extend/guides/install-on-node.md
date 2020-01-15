---
title: ツール拡張機能の開発
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 3a93a1105862ffbf4fcbd1d23b15d9bcaa6010dc
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950500"
---
# <a name="install-extension-payload-on-a-managed-node"></a>管理対象ノードに拡張機能のペイロードをインストールする

>適用対象: Windows Admin Center、Windows Admin Center Preview

## <a name="setup"></a>[セットアップ]
> [!NOTE]
> このガイドに従うには、build 1.2.1904.02001 以降が必要です。 ビルド番号を確認するには、Windows 管理センターを開き、右上にある疑問符をクリックします。

Windows 管理センター用の[ツール拡張機能](../develop-tool.md)をまだ作成していない場合は、作成します。 完了したら、拡張機能を作成するときに使用される値をメモしておきます。

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```InstallOnNode``` |

ツール拡張フォルダー内で、```Node``` フォルダー (```{!Tool Name}\Node```) を作成します。 この API を使用すると、このフォルダーに格納されているすべてのものが、管理対象ノードにコピーされます。 ユースケースに必要なすべてのファイルを追加します。 

また、```{!Tool Name}\Node\installNode.ps1``` スクリプトも作成します。 このスクリプトは、すべてのファイルが ```{!Tool Name}\Node``` フォルダーから管理対象ノードにコピーされると、管理ノードで実行されます。 ユースケースのロジックを追加します。 ```{!Tool Name}\Node\installNode.ps1``` ファイルの例を次に示します。

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` には、API が検索する特定の名前があります。 このファイルの名前を変更すると、エラーが発生します。


## <a name="integration-with-ui"></a>UI との統合

```\src\app\default.component.ts``` を次のように更新します。

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
拡張機能を作成するときに使用された値にプレースホルダーを更新します。
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

また、```\src\app\default.component.html``` を次のものに更新します。
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
最後に ```\src\app\default.module.ts```:
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

## <a name="creating-and-installing-a-nuget-package"></a>NuGet パッケージの作成とインストール

最後の手順では、追加したファイルを使用して NuGet パッケージをビルドし、そのパッケージを Windows 管理センターにインストールします。

以前に拡張機能パッケージを作成していない場合は、「[発行拡張機能](../publish-extensions.md)ガイド」に従ってください。 
> [!IMPORTANT]
> この拡張機能の nuspec ファイルでは、```<id>``` 値がプロジェクトの ```manifest.json``` の名前と一致し、```<version>``` が ```\src\app\default.component.ts```に追加されたものと一致することが重要です。 また、```<files>```の下にエントリを追加します。 
> 
> ```<file src="Node\**\*.*" target="Node" />```」をご覧ください。

``` xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="https://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
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

このパッケージを作成したら、そのフィードへのパスを追加します。 Windows 管理センターで、[設定] [> 拡張機能 > フィード] に移動し、パッケージが存在する場所へのパスを追加します。 拡張機能のインストールが完了すると、[```install```] ボタンをクリックすると、API が呼び出されます。  