---
title: 選択
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c3723dd414adca68c22011ef3f6be02eb6531d5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889903"
---
# <a name="select"></a>選択



フォーカスを移動すると、ディスク、パーティション、ボリューム、またはバーチャル ハード_ディスク (VHD) します。

## <a name="syntax"></a>構文

```
select disk
select partition
select volume
select vdisk
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[ディスクを選択します。](select-disk.md)|ディスクにフォーカスを移動します。|
|[パーティションを選択します。](select-partition.md)|パーティションにフォーカスを移動します。|
|[ボリュームを選択します。](select-volume.md)|ボリュームにフォーカスを移動します。|
|[vdisk を選択します。](select-vdisk.md)|VHD にフォーカスを移動します。|

## <a name="remarks"></a>注釈

-   対応するパーティションを持つボリュームを選択したパーティションが自動的に選択します。
-   パーティションが対応するボリュームで選択されている場合、ボリュームを自動的に選択されます。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

