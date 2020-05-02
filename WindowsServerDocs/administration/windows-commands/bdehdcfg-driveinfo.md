---
title: bdehdcfg driveinfo
description: Bdehdcfg driveinfo コマンドのリファレンストピックでは、ドライブ文字、合計サイズ、最大空き領域、およびパーティションの特性が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b18b4c3e128cd17353d369b418a049d0208cb654
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718689"
---
# <a name="bdehdcfg-driveinfo"></a>bdehdcfg: driveinfo

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライブ文字、合計サイズ、最大空き領域、およびパーティションの特性が表示されます。 有効なパーティションだけが一覧表示されます。 4つのプライマリパーティションまたは拡張パーティションが既に存在する場合、未割り当ての領域は表示されません。

>[!NOTE]
> このコマンドは情報提供のみを目的としており、ドライブに変更を加えません。

## <a name="syntax"></a>構文

```
bdehdcfg -driveinfo <drive_letter>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| <drive_letter> | ドライブ文字の後にコロンを続けて指定します。 |

## <a name="example"></a>例

C: ドライブのドライブ情報を表示するには、次のようにします。

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
