---
title: bitsadmin getminretrydelay
description: Windows コマンド」のトピック**bitsadmin getminretrydelay** -ファイルの転送を試行する前に一時的なエラーが発生したとき、サービスが待機する秒単位の時間の長さを取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a6df9faab8340994ad9219a863ad8e50186ccd1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832203"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay



ファイルの転送を試行する前に一時的なエラーが発生したとき、サービスが待機する秒単位の時間の長さを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetMinRetryDelay <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの最小再試行間隔を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)