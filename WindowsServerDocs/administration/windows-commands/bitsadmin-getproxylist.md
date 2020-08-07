---
title: bitsadmin getproxylist-指定したジョブのプロキシの一覧を取得します。
description: 指定されたジョブのプロキシ一覧を取得する bitsadmin getproxylist コマンドの参照記事です。
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bcd94c65a11006a795f071224397d8b3081b7548
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893972"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

指定したジョブに使用するプロキシサーバーのコンマ区切りの一覧を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのプロキシ一覧を取得するには、次のようにします。

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
