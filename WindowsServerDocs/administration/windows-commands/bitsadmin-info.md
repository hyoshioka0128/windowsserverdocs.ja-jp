---
title: bitsadmin info
description: Windows コマンド」のトピック**指定したジョブに関する概要情報が表示されます。** -bitsadmin 情報
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ee96c69e311600a53f04b1b883983718adf0f69
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851523"
---
# <a name="bitsadmin-info"></a>bitsadmin info



指定したジョブに関する概要情報が表示されます。

## <a name="syntax"></a>構文

```
bitsadmin /Info <Job> [/verbose]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

使用して、/verbose、ジョブに関する詳細情報を提供するパラメーター。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブに関する情報を取得する*myDownloadJob*します。
```
C:\>bitsadmin /Info myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)