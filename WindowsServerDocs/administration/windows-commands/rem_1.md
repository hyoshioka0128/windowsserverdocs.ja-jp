---
title: rem
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7245aedb-ba6f-49bb-9f77-848c4853c68f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4bd3ec5166ee2d5d8a99f5b728dcce31600722ec
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933492"
---
# <a name="rem"></a>rem



スクリプトにコメントを追加できます。

## <a name="syntax"></a>構文

```
rem
```

## <a name="examples"></a>例

このサンプルスクリプトでは、 **rem**を使用して、スクリプトの内容に関するコメントを指定しています。
```
rem The commands in this script set up 3 drives.
rem The first drive is a primary partition and is
rem assigned the letter D. The second and third drives
rem are logical partitions, and are assigned letters
rem E and F.
create partition primary size=2048
assign d:
create partition extended
create partition logical size=2048
assign e:
create partition logical
assign f:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

