---
title: bitsadmin setminretrydelay
description: '**Bitsadmin setminretrydelay**の Windows コマンドに関するトピックでは、ファイルの転送を試行する前に、一時的なエラーが発生した後に BITS が待機する時間の最小値を秒単位で設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce8674ca-6cc5-4bb2-8dda-7dfbb1cd6830
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddae9a62a49ca07bb03649f131a0a1ebad8ee3fe
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122872"
---
# <a name="bitsadmin-setminretrydelay"></a>bitsadmin setminretrydelay

一時エラーが発生してからファイルの転送を試行するまでの待機時間の最小値を秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setminretrydelay <job> <retrydelay>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| retrydelay | 転送中にエラーが発生した後のビットの待機時間の最小値 (秒単位)。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの最小再試行間隔を35秒に設定しています。

```
C:\>bitsadmin /setminretrydelay myDownloadJob 35
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)