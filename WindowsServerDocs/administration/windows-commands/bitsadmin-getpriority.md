---
title: bitsadmin getpriority
description: 指定されたジョブの優先度を取得する bitsadmin getpriority コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 38f92e83ccf5b048d168ce6a21c6026f490b18bf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717676"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

指定されたジョブの優先順位を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

#### <a name="output"></a>出力

このコマンドで返される優先順位は次のとおりです。

- **フォア**

- **高い**

- **通常**

- **低画質**

- **知ら**

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの優先順位を取得するには、次のようにします。

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
