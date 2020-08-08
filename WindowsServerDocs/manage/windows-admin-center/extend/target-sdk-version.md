---
title: 別のバージョンの Windows 管理センター SDK をターゲットにする
description: 別のバージョンの Windows 管理センター SDK (プロジェクトホノルル) をターゲットにする
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 96e17326bc289b4ad018da59b01344956586a198
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964558"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>別のバージョンの Windows 管理センター SDK をターゲットにする

>適用先:Windows Admin Center、Windows Admin Center Preview

SDK の変更とプラットフォームの変更によって拡張機能を最新の状態に保つことは簡単です。  [Npm タグ](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk)を使用して、新機能のリリースを SDK バージョンに整理します。

次の3つの SDK バージョンを選択できます。

* ```latest```-この SDK パッケージは、Windows 管理センターの現在の GA リリースと整合しています
* ```insider```-この SDK パッケージは、Windows 管理センターの現在のプレビューリリース (Windows Server Insider Preview で利用可能) と整合しています。
* ```next```–この SDK パッケージには、最新の機能が含まれています

> [!NOTE]
> ダウンロードできる Windows 管理センターのさまざまな[バージョン](https://aka.ms/WACDownloadPage)については、こちらを参照してください。

## <a name="targeting-sdk-version-on-a-new-project"></a>新しいプロジェクトでの SDK バージョンのターゲット設定

新しい拡張機能を作成するときに、パラメーターを追加して、 ```--version``` 別のバージョンの SDK を対象にすることができます。

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| 値 | 説明 | 例 |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | 会社名 (スペースを含む) | ```Contoso Inc``` |
| ```{!Tool Name}``` | (スペースを含む) ツール名 | ```Manage Foo Works``` |
| ```{!version}``` | SDK バージョン | ```latest``` |

次に、新しい拡張機能をターゲットにする例を示し ```insider``` ます。

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>既存のプロジェクトでの SDK バージョンのターゲット設定

別の SDK バージョンを対象とするように既存のプロジェクトを変更するには、の次の行を変更し ```package.json``` ます。

```
"@microsoft/windows-admin-center-sdk": "latest",
```
この例では、を ```latest``` 必要な SDK のバージョン (つまり、) に置き換えます。 ```insider```

```
"@microsoft/windows-admin-center-sdk": "insider",
```

次に、を実行し ```npm install``` て、プロジェクト全体で参照を更新します。