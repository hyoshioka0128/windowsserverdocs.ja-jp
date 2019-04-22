---
title: bitsadmin setminretrydelay
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 640492cf690a934e3e3b8d0ecf8ca7a0d6a7dc2f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813083"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

ファイルの転送を試行する前に一時的なエラーが発生したときに BITS が待機する秒単位で時間の最小の長さを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetMinRetryDelay <Job> <RetryDelay>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|RetryDelay|秒単位で表された数値。|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの最小再試行間隔を設定する*myDownloadJob* 35 秒にします。
```
C:\>bitsadmin /SetMinRetryDelay myDownloadJob 35
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)