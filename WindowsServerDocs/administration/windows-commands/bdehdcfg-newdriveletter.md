---
title: bdehdcfg newdriveletter
description: '**Bdehdcfg newdriveletter**の Windows コマンドに関するトピックでは、システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f1f200a0-6850-4f0d-9047-f9f982a590f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a8757e7d0684912525817708fbe34953b049582
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851055"
---
# <a name="bdehdcfg-newdriveletter"></a>bdehdcfg: newdriveletter

システムドライブとして使用されるドライブの部分に新しいドライブ文字を割り当てます。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -newdriveletter <DriveLetter>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------| ----------- |
|`<DriveLetter>`|指定されたターゲットドライブに割り当てられるドライブ文字を定義します。|

## <a name="remarks"></a>コメント

ベストプラクティスとして、システムドライブにドライブ文字を割り当てないことをお勧めします。

## <a name="examples"></a><a name="BKMK_Examples"></a>例

次の例は、ドライブ文字 P が割り当てられている既定のドライブを示しています。

```
bdehdcfg -target default -newdriveletter P:
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Bdehdcfg](bdehdcfg.md)