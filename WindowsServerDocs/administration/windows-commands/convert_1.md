---
title: convert
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d78f7adbc26acf9787ad39019e1450542a6acda2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379028"
---
# <a name="convert"></a>convert



ディスクをディスクの種類別に変換します。

## <a name="syntax"></a>構文

```
convert basic
convert dynamic
convert gpt
convert mbr
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[基本の変換](convert-basic.md)|空のダイナミック ディスクをベーシック ディスクに変換します。|
|[動的変換](convert-dynamic.md)|ベーシックディスクをダイナミックディスクに変換します。|
|[Gpt の変換](convert-gpt.md)|マスターブートレコード (MBR) パーティションスタイルを持つ空のベーシックディスクを、GUID パーティションテーブル (GPT) パーティションスタイルを持つベーシックディスクに変換します。|
|[Mbr の変換](convert-mbr.md)|GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

