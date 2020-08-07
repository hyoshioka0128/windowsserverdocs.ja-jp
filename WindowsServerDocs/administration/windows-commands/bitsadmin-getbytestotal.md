---
title: bitsadmin getbytestotal
description: 指定されたジョブのサイズを取得する bitsadmin getbytestotal コマンドの参照記事です。
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8b26773578d4c9a24f969df1506828c202e12b41
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894564"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

指定されたジョブのサイズを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのサイズを取得するには、次のようにします。

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
