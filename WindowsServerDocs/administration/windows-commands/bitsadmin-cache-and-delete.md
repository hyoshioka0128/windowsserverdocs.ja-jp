---
title: bitsadmin キャッシュおよび delete
description: Windows コマンド」のトピック**bitsadmin をキャッシュし、削除**-特定のキャッシュ エントリを削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 63b82cbbadebf2c4e36f2c76076b329787d7b1b5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852513"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin キャッシュおよび delete



特定のキャッシュ エントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /Delete RecordID 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|RecordID|キャッシュ エントリに関連付けられた GUID です。|

## <a name="BKMK_examples"></a>例

次の例では、{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を持つキャッシュ エントリを削除します。
```
C:\>bitsadmin /Cache /Delete {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)