---
title: bitsadmin suspend
description: '**Bitsadmin suspend**の Windows コマンドに関するトピックでは、指定されたジョブを中断します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42ed83d4dbf8c3d982c5c186b440cf17997903c9
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123153"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたジョブを中断します。 誤ってジョブを中断した場合は、 [bitsadmin resume](bitsadmin-resume.md)スイッチを使用してジョブを再開できます。

## <a name="syntax"></a>構文

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| Job | ジョブの表示名または GUID。 |

## <a name="example"></a>例

次の例では、 *Mydownloadjob*という名前のジョブを一時停止します。


```
C:\>bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
