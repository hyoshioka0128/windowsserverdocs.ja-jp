---
title: ツール拡張機能に iFrame を追加する
description: ツール拡張機能の開発 Windows 管理センター SDK (Project ホノルル)-ツール拡張に iFrame を追加する
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0833b2fd92f2bf4b512120783bb71295a3112745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406897"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>ツール拡張機能に iFrame を追加する

>適用対象: Windows Admin Center、Windows Admin Center Preview

この記事では、Windows 管理センター CLI で作成した新しい空のツール拡張機能に iFrame を追加します。

## <a name="prepare-your-environment"></a>環境の準備 ##

まだ行っていない場合は、「[ツール拡張機能の開発](../develop-tool.md)」の指示に従って、環境を準備し、新しい空のツール拡張を作成します。

## <a name="add-a-module-to-your-project"></a>モジュールをプロジェクトに追加する ##

新しい空の[モジュール](add-module.md)をプロジェクトに追加します。ここでは、次の手順で iFrame を追加します。  

## <a name="add-an-iframe-to-your-module"></a>モジュールに iFrame を追加する ##

ここで、作成した新しい空のモジュールに iFrame を追加します。

-Src\ アプリ\, モジュールフォルダーを参照し、次の名前付け規則で見つかったファイル ```{!module-name}.component.html```を開きます。

| Value | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.component.html``` |
    
次の内容を html ファイルに追加します。

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

これで、拡張機能に iFrame が追加されました。  次に、Windows 管理センターで拡張機能を[ビルドしてサイドロード](../develop-tool.md#build-and-side-load-your-extension)し、結果を確認することができます。

> [!Note]
> コンテンツセキュリティポリシー (CSP) の設定により、一部のサイトが Windows 管理センター内の iFrame で表示されない可能性があります。 詳細については、[こちら](https://content-security-policy.com/)を参照してください。 
