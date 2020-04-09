---
title: serverweroptin
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 18b4a56888b3f23bf3bac4a12b2dba7079b50923
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834635"
---
# <a name="serverweroptin"></a>serverweroptin

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

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
|/?|コマンド プロンプトでヘルプを表示します。|
## <a name="examples"></a><a name=BKMK_Examples></a>例
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
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

