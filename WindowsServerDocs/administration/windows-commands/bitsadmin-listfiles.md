---
title: bitsadmin listfiles
description: 指定されたジョブ内のファイルを一覧表示する bitsadmin listfiles コマンドの参照記事です。
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a5dcd9092f2d9a8d150496e4cf89595537885d62
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893690"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

指定されたジョブ内のファイルを一覧表示します。

## <a name="syntax"></a>構文

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのファイルの一覧を取得するには、次のようにします。

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
