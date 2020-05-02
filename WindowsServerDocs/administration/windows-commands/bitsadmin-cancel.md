---
title: bitsadmin cancel
description: Bitsadmin cancel コマンドのリファレンストピック。転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95fefbc4a9731c2ccbac22adc27f8231a7f36138
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718253"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

転送キューから*Mydownloadjob*ジョブを削除するには、次のようにします。

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
