---
title: ツール拡張機能を iFrame を追加します。
description: Windows Admin Center SDK (Project Honolulu) ツールの拡張機能の開発 - iFrame をツールの拡張機能を追加します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b4a7b688e4b2d9f52e44395c19211b91b964578
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080929"
---
# ツール拡張機能を iFrame を追加します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

この記事では、Windows Admin Center CLI を使用しましたが、新しい空のツールの拡張機能に、iFrame を追加します。

## 環境の準備 ##

まだの場合は、[ツールの拡張機能の開発](..\develop-tool.md)環境を準備して、新しい空のツールの拡張機能を作成するに指示に従います。

## モジュールをプロジェクトに追加します。 ##

これを次の手順で iFrame を追加しますが、プロジェクトに新しい[空のモジュール](add-module.md)を追加します。  

## IFrame をモジュールに追加します。 ##

先ほど作成したが、新しい空のモジュールを iFrame を追加します。

\Src\app\、モジュール フォルダーを参照し、ファイルを開く```{!module-name}.component.html```、次の命名規則で見つかった。

| 値 | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.component.html``` |
    
次の内容を html ファイルに追加します。

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

ですが、iFrame は拡張機能を追加しました。  次に、結果を表示する Windows Admin Center で拡張機能[と側のビルドの負荷](..\develop-tool.md#build-and-side-load-your-extension)をできます。
