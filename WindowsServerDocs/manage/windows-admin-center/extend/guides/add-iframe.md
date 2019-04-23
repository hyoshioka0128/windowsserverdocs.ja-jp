---
title: ツール拡張機能に iFrame を追加する
description: 開発ツールの拡張機能 Windows Admin Center SDK (プロジェクト ホノルル) - ツールの拡張機能に iFrame を追加します。
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7cf1dcec1bc8e187b6db789c5402ca8119ca8b6c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850763"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>ツール拡張機能に iFrame を追加する

>適用先:Windows Admin Center、Windows Admin Center プレビュー

この記事では、Windows Admin Center CLI を使用して作成した新しい、空のツールの拡張機能に、iFrame を追加します。

## <a name="prepare-your-environment"></a>環境の準備 ##

まだインストールしていない場合の手順を実行[ツールの拡張機能を開発](..\develop-tool.md)環境の準備を新規作成は、ツールの拡張機能を空にします。

## <a name="add-a-module-to-your-project"></a>モジュール プロジェクトへの追加します。 ##

新しい追加[空モジュール](add-module.md)を次の手順で iFrame を追加しましたが、プロジェクトにします。  

## <a name="add-an-iframe-to-your-module"></a>IFrame をモジュールに追加します。 ##

先ほど作成したその新しい、空のモジュールに iFrame を追加します。

\Src\app で\,モジュール フォルダーに移動し、ファイルを開く```{!module-name}.component.html```、次の名前付け規則で検出されました。

| 値 | 説明 | ファイル名の例 |
| ----- | ----------- | ------- |
| ```{!module-name}``` | モジュール名 (小文字、スペースをダッシュに置換) | ```manage-foo-works-portal.component.html``` |
    
次の内容を html ファイルに追加します。

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

これで、拡張機能に iFrame を追加しました。  次に、実行できます[ビルドおよび負荷を側](..\develop-tool.md#build-and-side-load-your-extension)結果を表示する Windows Admin Center で、拡張機能。

> [!Note]
> コンテンツ セキュリティ ポリシー (CSP) の設定によっては、Windows Admin Center 内で iFrame で表示から一部のサイトができません。 これに関する詳細については、[ここ](https://content-security-policy.com/)します。 
