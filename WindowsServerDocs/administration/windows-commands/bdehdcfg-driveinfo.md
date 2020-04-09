---
title: bdehdcfg driveinfo
description: '**Bdehdcfg driveinfo**の Windows コマンドに関するトピックでは、ドライブ文字、合計サイズ、最大空き領域、およびパーティションの特性が表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c598ea2d1d140090d623b3b48dbcc1be51ee66c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851065"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライブ文字、合計サイズ、最大空き領域、およびパーティションの特性が表示されます。 有効なパーティションだけが一覧表示されます。 4つのプライマリパーティションまたは拡張パーティションが既に存在する場合、未割り当ての領域は表示されません。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -driveinfo <DriveLetter>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| <DriveLetter> | ドライブ文字の後にコロンを続けて指定します。 |

## <a name="remarks"></a>コメント

コマンドは情報提供のみを目的としており、ドライブに変更は加えられません。

## <a name="example"></a><a name=BKMK_Examples></a>よう

次の例では、ドライブ C のドライブ情報が表示されます。

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
