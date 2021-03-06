---
title: bdehdcfg driveinfo
description: 'Windows コマンド」のトピック * * bdehdcfg: * * - driveinfo ドライブ文字、合計サイズ、最大の空き領域、およびパーティションの特性を表示します。'
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2dd62e34f8205e0b5d395ba759fff4b4937b0ad
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435043"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライブ文字、合計サイズ、最大の空き領域、およびパーティションの特性が表示されます。 有効なパーティションのみが一覧表示されます。 4 つのプライマリまたは拡張パーティションが既に存在する場合は、未割り当て領域は表示されません。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
bdehdcfg -driveinfo <DriveLetter>
```
### <a name="parameters"></a>パラメーター

|   パラメーター   |                  説明                  |
|---------------|-----------------------------------------------|
| <DriveLetter> | コロンの後にドライブ文字を指定します。 |

## <a name="remarks"></a>注釈
このコマンドは情報ですし、ドライブに変更は行われない。
## <a name="BKMK_Examples"></a>例
次の例では、C ドライブのドライブ情報が表示されます。
```
bdehdcfg  driveinfo C:
```
## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [bdehdcfg](bdehdcfg.md)
