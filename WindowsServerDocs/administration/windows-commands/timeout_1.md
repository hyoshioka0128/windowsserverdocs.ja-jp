---
title: タイムアウト
description: Windows コマンドに関するトピック (タイムアウト)。指定された秒数のコマンドプロセッサを一時停止します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e26b4a84-0e30-46e1-aa10-0667b7d3cb4c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd0a43e49e8a7567ac975333b04a9e6f549a0fd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832815"
---
# <a name="timeout"></a>タイムアウト

指定した秒数のコマンド プロセッサを一時停止します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
timeout /t <TimeoutInSeconds> [/nobreak] 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/t \<TimeoutInSeconds >|コマンド プロセッサが処理を続行する前に待機するには、10 進数 (-1 ~ 99999) 秒数を指定します。 値-1 は、キーストロークを無期限に待機するコンピューターです。|
|/nobreak|ユーザー キー ストロークを無視するように指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **タイムアウト** コマンドは、通常、バッチ ファイルで使用します。
-   ユーザーのキー入力は、タイムアウト期間の有効期限が切れていない場合でも、すぐに、コマンド プロセッサの実行を再開します。
-   組み合わせて使用すると、 **スリープ** コマンド、 **タイムアウト** に似ていますが、 **を一時停止** コマンドです。

## <a name="examples"></a><a name=BKMK_examples></a>例

コマンド プロセッサを一時停止、10 秒間に、次のように入力します。
```
timeout /t 10
```
100 秒のコマンド プロセッサを一時停止し、キー ストロークを無視する、次のように入力します。
```
timeout /t 100 /nobreak
```
コマンド プロセッサを一時停止、キーが押されるまで、次のように入力します。
```
timeout /t -1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
