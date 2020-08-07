---
title: bitsadmin getdisplayname
description: Bitsadmin getdisplayname コマンドの参照記事。指定されたジョブの表示名を取得します。
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8ddc6e2f73062abca7c711a02c9c3a4f9c725bde
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894390"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname

指定されたジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getdisplayname <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの表示名を取得するには、次のようにします。

```
bitsadmin /getdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
