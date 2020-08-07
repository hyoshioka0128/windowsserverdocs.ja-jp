---
title: serverweroptin
description: 参照記事 * * * *-
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9bcedf0d855980b193f466e719483ec268afd40c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87882719"
---
# <a name="serverweroptin"></a>serverweroptin

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

エラー報告を有効にできます。
## <a name="syntax"></a>構文
```
serverweroptin [/query] [/detailed] [/summary]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
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
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

