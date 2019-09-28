---
title: bitsadmin monitor
description: '**Bitsadmin monitor**の Windows コマンドトピックでは、現在のユーザーが所有している転送キュー内のジョブを監視します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fe4963349c7e17fc77500b5adfceafc48a20ac5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381222"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor



現在のユーザーが所有している転送キュー内のジョブを監視します。

## <a name="syntax"></a>構文

```
bitsadmin /Monitor [/allusers] [/refresh <Seconds>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Allusers|省略可能-すべてのユーザーのジョブを監視します。|
|Refresh|省略可能:*秒*単位で指定された間隔でデータを更新します。 既定の更新間隔は5秒です。|

## <a name="remarks"></a>コメント

**Allusers**パラメーターを使用するには、管理者特権が必要です。

更新を停止するには、CTRL + C キーを使用します。

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーが所有しているジョブの転送キューを監視し、60秒ごとに情報を更新します。
```
C:\>bitsadmin /Monitor /refesh 60
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)