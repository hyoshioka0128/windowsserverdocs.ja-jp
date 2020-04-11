---
title: bitsadmin setpriority
description: '**Bitsadmin setpriority**の Windows コマンドに関するトピックでは、指定されたジョブの優先順位を設定します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90788363-01a2-4d7c-a560-a3eba45b5e9e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9348680a61649b938267b3277de9aa5aa521361f
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122766"
---
# <a name="bitsadmin-setpriority"></a>bitsadmin setpriority

指定されたジョブの優先順位を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setpriority <job> <priority>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| priority | ジョブの優先順位を設定します。次に例を示します。<ul><li>FOREGROUND</li><li>HIGH</li><li>NORMAL</li><li>LOW</li></ul> |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの優先順位を normal に設定します。

```
C:\>bitsadmin /setpriority myDownloadJob NORMAL
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)