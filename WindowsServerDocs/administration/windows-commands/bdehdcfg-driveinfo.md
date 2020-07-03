---
title: bdehdcfg driveinfo
description: Bdehdcfg driveinfo コマンドの参照記事。ドライブ文字、合計サイズ、最大空き領域、およびパーティションの特性が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f2d065e7-eced-4509-a1a0-ee2521a7f02e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0063c73cd20aca8c8fe5cc21b245517475268c64
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923485"
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

| パラメーター | 説明 |
| --------- | ----------- |
| <drive_letter> | ドライブ文字の後にコロンを続けて指定します。 |

## <a name="example"></a>例

C: ドライブのドライブ情報を表示するには、次のようにします。

```
bdehdcfg  driveinfo C:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
