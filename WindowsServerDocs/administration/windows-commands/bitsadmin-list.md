---
title: bitsadmin list
description: Windows コマンド」のトピック**bitsadmin 一覧**-現在のユーザーによって所有されている転送ジョブを一覧表示します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0b88001b9c4ae01b57006ffeef66dec0348ca77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873863"
---
# <a name="bitsadmin-list"></a>bitsadmin list



現在のユーザーによって所有されている転送ジョブを一覧表示します。

## <a name="syntax"></a>構文

```
bitsadmin /List [/allusers][/verbose]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/Allusers|省略可能-すべてのユーザーのジョブを一覧表示|
|/Verbose|省略可能: 各ジョブの詳細情報を提供します。|

## <a name="remarks"></a>注釈

/Allusers パラメーターを使用する管理者特権が必要

## <a name="BKMK_examples"></a>例

次の例では、現在のユーザーが所有するジョブに関する情報を取得します。
```
C:\>bitsadmin /List 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)