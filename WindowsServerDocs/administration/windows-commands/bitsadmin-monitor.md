---
title: bitsadmin monitor
description: Windows コマンド」のトピック**bitsadmin モニター** -現在のユーザーが所有する転送キュー内のジョブを監視します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2c4620d5c8e46cb8bfcb6b9c83261d57781abea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814593"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor



現在のユーザーが所有する転送キュー内のジョブを監視します。

## <a name="syntax"></a>構文

```
bitsadmin /Monitor [/allusers] [/refresh <Seconds>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Allusers|省略可能-すべてのユーザーのジョブを監視します。|
|Refresh|省略可能: で指定された間隔でデータを更新*秒*します。 既定の更新間隔は、5 秒です。|

## <a name="remarks"></a>注釈

使用する管理者特権が必要、 **Allusers**パラメーター。

CTRL + C を使用して、更新を停止します。

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーが所有するジョブの転送キューを監視し、60 秒ごとの情報を更新します。
```
C:\>bitsadmin /Monitor /refesh 60
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)