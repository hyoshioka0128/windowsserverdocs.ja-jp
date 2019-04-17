---
title: Windows Admin Center SDK のさまざまなバージョンをターゲットします。
description: Windows Admin Center SDK (Project Honolulu) のさまざまなバージョンをターゲットします。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081039"
---
# Windows Admin Center SDK のさまざまなバージョンをターゲットします。

>適用対象: Windows Admin Center、Windows Admin Center Preview

拡張機能を SDK の変更とプラットフォームの変更を最新の状態に保つことは簡単です。  SDK のバージョンの新機能のリリースに整理[NPM タグ](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk)を使用します。

選択できる 3 つの SDK バージョンがあります。

* ```latest``` -この SDK パッケージが Windows Admin Center の現在の GA リリースと合わせるため
* ```insider``` -この SDK パッケージが Windows Admin Center (Windows Server Insider Preview で利用可能) の現在のプレビュー リリースと合わせるため
* ```next``` -この SDK パッケージには、最新の機能が含まれています。

> [!NOTE]
> 異なる[バージョン](https://aka.ms/WACDownloadPage)をダウンロードで利用できる Windows Admin Center の詳細について説明します。

## 新しいプロジェクトのターゲット SDK バージョン

新しい拡張機能を作成する場合は、含める、```--version```さまざまなバージョンの SDK を対象とするパラメーター。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペース) を | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペース) をツール名 | ```Manage Foo Works``` |
| ```{!version}``` | SDK バージョン | ```latest``` |

新しい拡張ターゲットを作成する例を示します```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## 既存のプロジェクトで SDK バージョンをターゲットと

さまざまな SDK バージョンをターゲットに既存のプロジェクトを変更するには、次の行を変更```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
この例では置換```latest```、目的の SDK バージョンとつまり```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

実行し、```npm install```プロジェクト全体の参照を更新します。