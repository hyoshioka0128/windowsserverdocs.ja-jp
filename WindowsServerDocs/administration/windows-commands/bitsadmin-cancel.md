---
title: bitsadmin cancel
description: Bitsadmin cancel コマンドの参照記事。転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 35173fe8b2e4f3888fa3a365ca25da35b8153eb4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928364"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cancel <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

転送キューから*Mydownloadjob*ジョブを削除するには、次のようにします。

```
bitsadmin /cancel myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
