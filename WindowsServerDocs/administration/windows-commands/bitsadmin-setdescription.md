---
title: bitsadmin setdescription
description: Bitsadmin setdescription コマンドの参照記事。指定されたジョブの説明を設定します。
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d499b152f5cb3a846cc1de6ec65f07903421cf49
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893175"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription

指定されたジョブの説明を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| description | ジョブを説明するために使用されるテキストです。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの説明を取得するには、次のようにします。

```
bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
