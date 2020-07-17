---
title: bitsadmin getbytestransferred
description: Bitsadmin getbytestransferred コマンドの参照記事。指定されたジョブで転送されたバイト数を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ca8561a0c5eb92bb4bd716f7b20bd9f7ceaf606
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85923117"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

指定したジョブに対して転送されたバイト数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで転送されたバイト数を取得するには、次のようにします。

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
