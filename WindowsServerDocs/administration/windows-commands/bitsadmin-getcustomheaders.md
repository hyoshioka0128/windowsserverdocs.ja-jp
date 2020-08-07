---
title: bitsadmin getcustomheaders
description: Bitsadmin getcustomheaders コマンドの参照記事で、ジョブからカスタム HTTP ヘッダーを取得します。
ms.topic: article
ms.assetid: 1f0d38d3-e865-4474-81e8-773d65c3d1cc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3cc970a7aeee1be678a3c77d852af91ae0ab98c8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894413"
---
# <a name="bitsadmin-getcustomheaders"></a>bitsadmin getcustomheaders

ジョブからカスタム HTTP ヘッダーを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcustomheaders <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのカスタムヘッダーを取得するには、次のようにします。

```
bitsadmin /getcustomheaders myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
