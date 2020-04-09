---
title: bitsadmin cache と setlimit
description: '**Bitsadmin cache と setlimit**に関する Windows コマンドのトピックでは、キャッシュサイズの制限を設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46578835-d5ce-423b-be4d-62ddb9e1908d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 746ee0b69da8f5bd22fec2ccbd432126cc25d94d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850875"
---
# <a name="bitsadmin-cache-and-setlimit"></a>bitsadmin cache と setlimit

キャッシュサイズの制限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /setlimit percent
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| percent | ハードディスクの合計領域に対する割合として定義されているキャッシュの制限。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、キャッシュサイズを50% に制限しています。

```
C:\>bitsadmin /cache /setlimit 50
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)