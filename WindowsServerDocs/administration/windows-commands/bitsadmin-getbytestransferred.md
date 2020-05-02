---
title: bitsadmin getbytestransferred
description: 指定されたジョブで転送されたバイト数を取得する bitsadmin getbytestransferred コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 47bbf184-e06f-4be0-b2ba-d32b10d82002
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7c333926ed46dd2e66e0e2507f838f721a73c192
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718142"
---
# <a name="bitsadmin-getbytestransferred"></a>bitsadmin getbytestransferred

指定したジョブに対して転送されたバイト数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getbytestransferred <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで転送されたバイト数を取得するには、次のようにします。

```
bitsadmin /getbytestransferred myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
