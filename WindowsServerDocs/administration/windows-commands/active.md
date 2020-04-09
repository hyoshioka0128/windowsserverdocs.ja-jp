---
title: アクティブ
description: '**[アクティブ]** の Windows コマンドトピック (ベーシックディスクの場合) は、パーティションをアクティブとしてマークします。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f25da2e-87fc-4392-a7ee-f38d09b7873c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42f2e0d367344355e8f9a570f37cfbdc5dfc4590
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851375"
---
# <a name="active"></a>アクティブ

ベーシック ディスクで、フォーカスのあるパーティションをアクティブとしてマークします。

> [!CAUTION]
> DiskPart では、パーティションがオペレーティングシステムのスタートアップファイルを含むことができるかどうかのみが検証されます。 DiskPart では、パーティションの内容を確認できません。 パーティションを誤ってアクティブとしてマークし、オペレーティングシステムのスタートアップファイルが含まれていない場合は、コンピューターが起動しないことがあります。

## <a name="syntax"></a>構文

```
active
```- 

## Remarks

-   This informs the basic input/output system (BIOS) or Extensible Firmware Interface (EFI) that the partition or volume is a valid system partition or system volume.

-   Only partitions can be marked as active.

-   A partition must be selected for this operation to succeed. Use the **select partition** command to select a partition and shift the focus to it.

## <a name=BKMK_examples></a>Examples

To mark the partition with focus as the active partition, type:

```
アクティブ
```
## Additional References

- [Command-Line Syntax Key](command-line-syntax-key.md)