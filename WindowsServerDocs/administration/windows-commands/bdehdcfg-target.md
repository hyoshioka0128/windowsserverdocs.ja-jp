---
title: bdehdcfg ターゲット
description: Bdehdcfg target の Windows コマンドトピックでは、BitLocker と Windows 回復によってシステムドライブとして使用するパーティションを準備します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f761d25d-8349-4ac7-ac46-6bb340a4348f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2fb0a1daa257ef2c9f1cd77b88e5ef14f84a0dfa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382181"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: ターゲット



BitLocker と Windows 回復によってシステムドライブとして使用するパーティションを準備します。 既定では、このパーティションはドライブ文字なしで作成されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|既定値 (default)|は、コマンドラインツールが BitLocker セットアップウィザードと同じプロセスに従うことを示します。|
|未|ディスク上の使用可能な未割り当て領域からシステムパーティションを作成します。|
|@no__t 0 のドライブ文字 > 圧縮|アクティブなシステムパーティションを作成するのに必要な量だけドライブを減らします。 このコマンドを使用するには、指定されたドライブに少なくとも 5% の空き領域が必要です。|
|\<DriveLetter merge|は、アクティブなシステムパーティションとして指定されたドライブを使用します。 オペレーティングシステムドライブをマージのターゲットにすることはできません。|

## <a name="BKMK_Examples"></a>例

次の例では、**ターゲット**コマンドを使用して、既存のドライブ (P) をシステムドライブとして指定しています。
```
bdehdcfg -target P: merge
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)