---
title: bdehdcfg サイズ
description: '**Bdehdcfg size**の Windows コマンドに関するトピック。新しいシステムドライブを作成するときのシステムパーティションのサイズを指定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c72bdfd0b8bf4dfd0aa36885ceb7fd249a18c332
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851025"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: サイズ

新しいシステムドライブを作成するときのシステムパーティションのサイズを指定します。

このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<SizeinMB>` | 新しいパーティションに使用するメガバイト (MB) 数を示します。 |

## <a name="remarks"></a>コメント

サイズを指定しない場合、ツールでは既定値の 300 MB が使用されます。 システムドライブの最小サイズは 100 MB です。 システムの回復などのシステムツールをシステムパーティションに格納する場合は、それに応じてサイズを大きくする必要があります。

> [!NOTE]
> **Size**コマンドを**ターゲット**`<DriveLetter>` **merge**コマンドと組み合わせることはできません。

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例では、 **size**コマンドを使用して、既定のシステムドライブに 500 MB を割り当てる方法を示します。

```
bdehdcfg -target default -size 500
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)