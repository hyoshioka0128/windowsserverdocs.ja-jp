---
title: serverweroptin
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3acba57aa012c57c5c6109ed948ce6bb5b28078
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721950"
---
# <a name="serverweroptin"></a>serverweroptin

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

エラー報告を有効にできます。
## <a name="syntax"></a>構文
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|/query|現在の設定を検証します。|
|詳細な/|送信では、レポートが自動的に詳しく説明します。|
|概要/|概要レポートを自動的に送信します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="examples"></a>例
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
## <a name="additional-references"></a>その他のリファレンス
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

