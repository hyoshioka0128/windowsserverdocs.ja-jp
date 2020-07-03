---
title: select
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9eeb40c0-4258-46e2-8dbc-94f63497e771
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6004d39e225b1ac4acd96b4108accff2ccfc485c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935937"
---
# <a name="select"></a>select



フォーカスを移動すると、ディスク、パーティション、ボリューム、またはバーチャル ハード_ディスク (VHD) します。

## <a name="syntax"></a>構文

```
select disk
select partition
select volume
select vdisk
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[ディスクの選択](select-disk.md)|ディスクにフォーカスを移動します。|
|[パーティションの選択](select-partition.md)|パーティションにフォーカスを移動します。|
|[ボリュームの選択](select-volume.md)|ボリュームにフォーカスを移動します。|
|[Vdisk の選択](select-vdisk.md)|VHD にフォーカスを移動します。|

## <a name="remarks"></a>注釈

-   対応するパーティションを持つボリュームを選択したパーティションが自動的に選択します。
-   パーティションが対応するボリュームで選択されている場合、ボリュームを自動的に選択されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

