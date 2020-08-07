---
title: bitsadmin info
description: Bitsadmin info コマンドの参照記事。指定されたジョブに関する概要情報が表示されます。
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6cd93716b818b3f1981ceb54c0c049933f25a77
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893727"
---
# <a name="bitsadmin-info"></a>bitsadmin info

指定されたジョブに関する概要情報を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| /verbose | 省略可能。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに関する情報を取得するには、次のようにします。

```
bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)
