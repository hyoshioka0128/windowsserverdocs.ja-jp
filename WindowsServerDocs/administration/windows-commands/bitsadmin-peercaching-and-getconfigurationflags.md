---
title: bitsadmin peercaching および getconfigurationflags
description: Bitsadmin ピアリングと getconfigurationflags コマンドの参照記事。コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 383387b135f38663a84999e041a4f6864d40a01d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893627"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching および getconfigurationflags

コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの構成フラグを取得するには、次のようにします。

```
bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)

- [bitsadmin ピアキャッシュコマンド](bitsadmin-peercaching.md)
