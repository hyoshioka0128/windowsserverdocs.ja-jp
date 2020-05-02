---
title: bitsadmin suspend
description: 指定されたジョブを中断する bitsadmin suspend コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8117cf9f4286994847e53dca8065da6821d47c5d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720449"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたジョブを中断します。 誤ってジョブを中断した場合は、 [bitsadmin resume](bitsadmin-resume.md)スイッチを使用してジョブを再開できます。

## <a name="syntax"></a>構文

```
bitsadmin /suspend <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ---------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="example"></a>例

*Mydownloadjob*という名前のジョブを中断するには、次のようにします。


```
bitsadmin /suspend myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin resume コマンド](bitsadmin-resume.md)

- [bitsadmin コマンド](bitsadmin.md)
