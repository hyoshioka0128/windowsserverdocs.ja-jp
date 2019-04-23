---
title: 別のバージョン、Windows Admin Center SDK の対象します。
description: ターゲット別のバージョンの Windows Admin Center SDK (プロジェクト ホノルル)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833623"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョン、Windows Admin Center SDK の対象します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

拡張機能の最新の SDK の変更点とプラットフォームの変更を維持することは簡単です。  使用して[NPM タグ](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk)SDK のバージョンの新機能のリリースに編成します。

選択できる 3 つの SDK バージョンがあります。

* ```latest``` – Windows Admin Center の現在の GA リリースではこの SDK パッケージの配置
* ```insider``` – Windows Admin Center (Windows Server Insider プレビューで利用可能) の現在のプレビュー リリースではこの SDK パッケージの配置
* ```next``` -この SDK パッケージには、最新の機能が含まれています。

> [!NOTE]
> さまざまな詳細は[バージョン](https://aka.ms/WACDownloadPage)のダウンロードに使用できる Windows Admin Center。

## <a name="targeting-sdk-version-on-a-new-project"></a>新しいプロジェクトに SDK のバージョンを対象とします。

新しい拡張機能を作成するときに含めることができます、```--version```さまざまなバージョンの SDK を対象とするパラメーター。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Value | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | (スペース) を会社名 | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペース) を含む、ツール名 | ```Manage Foo Works``` |
| ```{!version}``` | SDK のバージョン | ```latest``` |

対象と新しい拡張機能を作成する例を次に示します```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>既存のプロジェクトの SDK バージョンを対象とします。

別の SDK バージョンを対象とする既存のプロジェクトを変更するには、次の行を変更```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
この例では、置き換える```latest```、目的の SDK バージョン、つまり```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

実行して```npm install```プロジェクト全体での参照を更新します。