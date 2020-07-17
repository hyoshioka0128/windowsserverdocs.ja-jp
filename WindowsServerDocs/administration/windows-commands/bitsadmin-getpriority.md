---
title: bitsadmin getpriority
description: Bitsadmin getpriority コマンドの参照記事。指定されたジョブの優先順位を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 39ce769e2eb1dcf7a05d416dc2a66c6c082c9ae4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926851"
---
# <a name="bitsadmin-getpriority"></a>bitsadmin getpriority

指定されたジョブの優先順位を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

#### <a name="output"></a>出力

このコマンドで返される優先順位は次のとおりです。

- **フォア**

- **高い**

- **通常**

- **低画質**

- **UNKNOWN**

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの優先順位を取得するには、次のようにします。

```
bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
