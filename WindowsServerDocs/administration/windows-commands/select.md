---
title: 選択
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7dc3bc8775f971968f096ba4344348e77c112cfa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384111"
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
|[ディスクの選択](select-disk.md)|ディスクにフォーカスを移動します。|
|[パーティションの選択](select-partition.md)|パーティションにフォーカスを移動します。|
|[ボリュームの選択](select-volume.md)|ボリュームにフォーカスを移動します。|
|[Vdisk の選択](select-vdisk.md)|VHD にフォーカスを移動します。|

## <a name="remarks"></a>コメント

-   対応するパーティションを持つボリュームを選択したパーティションが自動的に選択します。
-   パーティションが対応するボリュームで選択されている場合、ボリュームを自動的に選択されます。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

