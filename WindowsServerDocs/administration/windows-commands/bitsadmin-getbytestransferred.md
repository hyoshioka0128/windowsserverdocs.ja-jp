---
title: bitsadmin getbytestransferred
description: Windows コマンド」のトピック**bitsadmin getbytestransferred** -指定したジョブの転送されたバイト数を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cce2c051af169385c43fdff4efdeff46d8422926
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814613"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred



指定したジョブの転送されたバイト数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetBytesTransferred <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの転送されたバイト数を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetBytesTransferred myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)