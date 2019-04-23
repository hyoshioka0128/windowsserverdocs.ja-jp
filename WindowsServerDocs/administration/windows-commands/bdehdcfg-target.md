---
title: bdehdcfg ターゲット
description: Bdehdcfg ターゲットに Windows コマンド」のトピックでは、BitLocker と Windows recovery によってシステム ドライブとして使用するため、パーティションを準備します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f8d180974f480b4c40532dab529ad49dcc33540d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881533"
---
# <a name="bdehdcfg-target"></a>bdehdcfg: target



BitLocker と Windows 回復してシステムのドライブとして使用するためには、パーティションを準備します。 既定では、ドライブ文字がないこのパーティションが作成されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|既定値 (default)|コマンド ライン ツールで、BitLocker セットアップ ウィザードと同じプロセスに従うことを示します。|
|未割り当て|ディスクの使用可能な未割り当ての領域外のシステム パーティションを作成します。|
|\<ドライブ文字 > 圧縮|アクティブなシステム パーティションを作成するために必要な量で指定されたドライブが減少します。 このコマンドを使用して、指定されたドライブに空き領域が 5% 以上する必要があります。|
|\<ドライブ文字 > マージ|アクティブなシステム パーティションとして指定されたドライブを使用します。 オペレーティング システムのドライブは、マージの対象にすることはできません。|

## <a name="BKMK_Examples"></a>例

使用して次の例を示しています、**ターゲット**システム ドライブとして既存のドライブ (P) を指定するコマンド。
```
bdehdcfg -target P: merge
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)