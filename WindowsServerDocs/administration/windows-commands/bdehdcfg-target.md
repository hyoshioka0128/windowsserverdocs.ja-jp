---
title: bdehdcfg ターゲット
description: '**Bdehdcfg target**の Windows コマンドに関するトピックでは、BitLocker および Windows 回復によってシステムドライブとして使用するパーティションを準備します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0f3e90fbb8725360cf8db335e79721e2328ab3a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851015"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: ターゲット

BitLocker と Windows 回復によってシステムドライブとして使用するパーティションを準備します。 既定では、このパーティションはドライブ文字なしで作成されます。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| default | は、コマンドラインツールが BitLocker セットアップウィザードと同じプロセスに従うことを示します。 |
| 未 | ディスク上の使用可能な未割り当て領域からシステムパーティションを作成します。 |
| `<DriveLetter>` 圧縮 | アクティブなシステムパーティションを作成するのに必要な量だけドライブを減らします。 このコマンドを使用するには、指定されたドライブに少なくとも5% の空き領域が必要です。 |
| `<DriveLetter>` マージ | は、アクティブなシステムパーティションとして指定されたドライブを使用します。 オペレーティングシステムドライブをマージのターゲットにすることはできません。 |

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例では、**ターゲット**コマンドを使用して、既存のドライブ (P) をシステムドライブとして指定しています。

```
bdehdcfg -target P: merge
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)