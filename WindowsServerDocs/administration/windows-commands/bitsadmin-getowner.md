---
title: bitsadmin getowner
description: Bitsadmin getowner コマンドの参照記事。指定されたジョブの所有者を取得します。
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91dd63dcba8b41fee01c17e87c817e32a9dbba39
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894049"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

指定したジョブの所有者の表示名または GUID が表示されます。

## <a name="syntax"></a>構文

```
bitsadmin /getowner <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの所有者を表示するには、次のようにします。

```
bitsadmin /getowner myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
