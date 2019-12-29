---
title: serverweroptin
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7d5791e059d31e416f848f6e8df648c8f9bd27d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371020"
---
# <a name="serverweroptin"></a>serverweroptin

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

エラー報告を有効にできます。
## <a name="syntax"></a>構文
```
serverweroptin [/query] [/detailed] [/summary]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/query|現在の設定を検証します。|
|詳細な/|送信では、レポートが自動的に詳しく説明します。|
|概要/|概要レポートを自動的に送信します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_Examples"></a>例
現在の設定を確認するには、次のように入力します。
```
serverweroptin /query
```
詳細レポートを自動的に送信するには、次のように入力します。
```
serverweroptin /detailed
```
概要レポートを自動的に送信するには、次のように入力します。
```
serverweroptin /summary
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

