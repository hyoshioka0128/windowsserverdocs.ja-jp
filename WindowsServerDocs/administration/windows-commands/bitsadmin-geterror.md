---
title: bitsadmin geterror
description: Bitsadmin geterror コマンドの参照記事。指定されたジョブの詳細なエラー情報を取得します。
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ae0b2391267ddc1508d8343b909b9739a0e01ffb
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894351"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror

指定されたジョブの詳細なエラー情報を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /geterror <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのエラー情報を取得するには、次のようにします。

```
bitsadmin /geterror myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
