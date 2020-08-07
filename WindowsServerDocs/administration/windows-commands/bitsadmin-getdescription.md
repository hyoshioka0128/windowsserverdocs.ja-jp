---
title: bitsadmin getdescription
description: Bitsadmin getdescription コマンドの参照記事。指定されたジョブの説明を取得します。
ms.topic: article
ms.assetid: f3974603-ebbe-4d31-8217-040fe2d90c85
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5023a0a4114796fa3a492de4fddaa0d5ddb0187
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894402"
---
# <a name="bitsadmin-getdescription"></a>bitsadmin getdescription

指定されたジョブの説明を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdescription <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの説明を取得するには、次のようにします。

```
bitsadmin /getdescription myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
