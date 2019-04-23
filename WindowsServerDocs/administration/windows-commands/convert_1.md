---
title: convert
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6a77e1fca9605c7e5cc4ff059db08ffbfcc81f81
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859283"
---
# <a name="convert"></a>convert



ディスクを別の 1 つのディスクの種類に変換します。

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
|[基本的な変換します。](convert-basic.md)|空のダイナミック ディスクをベーシック ディスクに変換します。|
|[動的変換します。](convert-dynamic.md)|ベーシック ディスクをダイナミック ディスクに変換します。|
|[Gpt に変換します。](convert-gpt.md)|マスター ブート レコード (MBR) パーティション スタイルに空のベーシック ディスクを GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。|
|[mbr を変換します。](convert-mbr.md)|GUID パーティション テーブル (GPT) パーティション スタイルを持つ空のベーシック ディスクをマスター ブート レコード (MBR) パーティション スタイルを持つベーシック ディスクに変換します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

