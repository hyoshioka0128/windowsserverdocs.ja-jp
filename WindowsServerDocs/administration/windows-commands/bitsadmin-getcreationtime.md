---
title: bitsadmin getcreationtime
description: Bitsadmin get time コマンドの参照記事。指定されたジョブの作成時刻を取得します。
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 42cd6de0769d4a741e76a1f6b03c32123ea8cf6a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894452"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

指定されたジョブの作成時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの作成時刻を取得するには、次のようにします。

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
