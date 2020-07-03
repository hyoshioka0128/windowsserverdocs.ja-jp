---
title: bitsadmin getfilestotal
description: Bitsadmin getfilestotal コマンドの参照記事。指定されたジョブ内のファイルの数を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c5de113e-f29c-4cd3-9392-0e300018d516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7592f783d17e31fe8a1e7fbf82cb41e20171c9fd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928284"
---
# <a name="bitsadmin-getfilestotal"></a>bitsadmin getfilestotal

指定されたジョブ内のファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getfilestotal <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに含まれるファイルの数を取得するには、次のようにします。

```
bitsadmin /getfilestotal myDownloadJob
```

## <a name="see-also"></a>関連項目

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
