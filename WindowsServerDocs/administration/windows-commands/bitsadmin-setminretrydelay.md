---
title: bitsadmin setminretrydelay
description: Bitsadmin setminretrydelay の Windows コマンドに関するトピックでは、ファイルの転送を試行する前に、一時的なエラーが発生した後に BITS が待機する時間の最小値を秒単位で設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb2fe4c6d0e4f90c6ec49fa1da63404393d4f634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849365"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

一時エラーが発生してからファイルの転送を試行するまでの待機時間の最小値を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RetryDelay|秒単位で表された数値。|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの最小再試行間隔を35秒に設定しています。
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)