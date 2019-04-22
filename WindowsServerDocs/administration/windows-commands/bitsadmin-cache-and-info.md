---
title: bitsadmin キャッシュおよび情報
description: Windows コマンド」のトピック**bitsadmin キャッシュおよび情報**-特定のキャッシュ エントリをダンプします。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 61ff57b33e575921f2032d4e13a2d9b74accae60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813323"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin キャッシュおよび情報



特定のキャッシュ エントリをダンプします。

## <a name="syntax"></a>構文

```
bitsadmin /Cache /Info RecordID [/Verbose] 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|RecordID|キャッシュ エントリに関連付けられた GUID です。|

## <a name="BKMK_examples"></a>例

次の例では、{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を持つキャッシュ エントリをダンプします。
```
C:\>bitsadmin /Cache /Info {6511FB02-E195-40A2-B595-E8E2F8F47702} 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)