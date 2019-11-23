---
title: bdehdcfg サイズ
description: Windows コマンドトピック-新しいシステムドライブを作成するときのシステムパーティションのサイズを指定します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80f55b1d-a28d-4edf-9997-1fb918b7b5a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ec42cdb5716c63c7210ea6cfde8ce8884833b45
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382196"
---
# <a name="bdehdcfg-size"></a>bdehdcfg: サイズ



新しいシステムドライブを作成するときのシステムパーティションのサイズを指定します。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink} -size <SizeinMB>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<SizeinMB >|新しいパーティションに使用するメガバイト (MB) 数を示します。|

## <a name="remarks"></a>注釈

サイズを指定しない場合、ツールでは既定値の 300 MB が使用されます。 システムドライブの最小サイズは 100 MB です。 システムの回復などのシステムツールをシステムパーティションに格納する場合は、それに応じてサイズを大きくする必要があります。

> [!NOTE]
> **Size**コマンドは、 **merge**コマンド >**ターゲット**\<ドライブ文字と組み合わせることはできません。

## <a name="BKMK_Examples"></a>例

次の例では、 **size**コマンドを使用して、既定のシステムドライブに 500 MB を割り当てる方法を示します。
```
bdehdcfg -target default -size 500
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)