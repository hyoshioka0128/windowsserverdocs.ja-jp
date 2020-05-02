---
title: bitsadmin peercaching および getconfigurationflags
description: Bitsadmin ピアリングと getconfigurationflags コマンドのリファレンストピック。コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 124ddc15-3444-4bd5-96e5-c6bfabe4f9c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62b6848dec30a9a9fef401b1b2372605dbb9934a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717325"
---
# <a name="bitsadmin-peercaching-and-getconfigurationflags"></a>bitsadmin peercaching および getconfigurationflags

コンピューターがピアにコンテンツを提供するかどうか、およびピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /peercaching /getconfigurationflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの構成フラグを取得するには、次のようにします。

```
bitsadmin /peercaching /getconfigurationflags myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)

- [bitsadmin ピアキャッシュコマンド](bitsadmin-peercaching.md)
