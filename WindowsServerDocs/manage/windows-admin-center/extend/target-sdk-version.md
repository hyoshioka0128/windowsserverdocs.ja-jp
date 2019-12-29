---
title: 別のバージョンの Windows 管理センター SDK をターゲットにする
description: 別のバージョンの Windows 管理センター SDK (プロジェクトホノルル) をターゲットにする
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0d3b7af5229f7b8487aa9f04eaf0d1756d8c02f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356972"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョンの Windows 管理センター SDK をターゲットにする

>適用先:Windows Admin Center、Windows Admin Center Preview

SDK の変更とプラットフォームの変更によって拡張機能を最新の状態に保つことは簡単です。  [Npm タグ](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk)を使用して、新機能のリリースを SDK バージョンに整理します。

次の3つの SDK バージョンを選択できます。

* ```latest```-この SDK パッケージは、Windows 管理センターの現在の GA リリースと整合しています
* ```insider```-この SDK パッケージは、Windows 管理センターの現在のプレビューリリース (Windows Server Insider Preview で利用可能) と整合しています。
* ```next```-この SDK パッケージには最新の機能が含まれています

> [!NOTE]
> ダウンロードできる Windows 管理センターのさまざまな[バージョン](https://aka.ms/WACDownloadPage)については、こちらを参照してください。

## <a name="targeting-sdk-version-on-a-new-project"></a>新しいプロジェクトでの SDK バージョンのターゲット設定

新しい拡張機能を作成するときに、別のバージョンの SDK を対象とするように ```--version``` パラメーターを含めることができます。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```Manage Foo Works``` |
| ```{!version}``` | SDK のバージョン | ```latest``` |

次に示すのは、新しい拡張機能を作成して ```insider``` にする例です。

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>既存のプロジェクトでの SDK バージョンのターゲット設定

既存のプロジェクトを変更して別の SDK バージョンを対象にするには、```package.json``` の次の行を変更します。

```
"@microsoft/windows-admin-center-sdk": "latest",
```
この例では、```latest``` を目的の SDK バージョン (```insider```) に置き換えます。

```
"@microsoft/windows-admin-center-sdk": "insider",
```

次に、```npm install``` を実行して、プロジェクト全体の参照を更新します。