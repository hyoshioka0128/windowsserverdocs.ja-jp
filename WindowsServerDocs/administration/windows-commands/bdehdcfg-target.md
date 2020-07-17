---
title: bdehdcfg target
description: BitLocker と Windows 回復によってシステムドライブとして使用するパーティションを準備する bdehdcfg target コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 509c659907878f7b0ddc0b0c601715fa996c5fe7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923364"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: ターゲット

BitLocker と Windows 回復によってシステムドライブとして使用するパーティションを準備します。 既定では、このパーティションはドライブ文字なしで作成されます。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<drive_letter> shrink|<drive_letter> merge}
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| default | は、コマンドラインツールが BitLocker セットアップウィザードと同じプロセスに従うことを示します。 |
| 未 | ディスク上の使用可能な未割り当て領域からシステムパーティションを作成します。 |
| `<drive_letter>`伸縮 | アクティブなシステムパーティションを作成するのに必要な量だけドライブを減らします。 このコマンドを使用するには、指定されたドライブに少なくとも5% の空き領域が必要です。 |
| `<drive_letter>`マージ | は、アクティブなシステムパーティションとして指定されたドライブを使用します。 オペレーティングシステムドライブをマージのターゲットにすることはできません。 |

## <a name="examples"></a>例

既存のドライブ (P) をシステムドライブとして指定するには、次のようにします。

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bdehdcfg](bdehdcfg.md)
