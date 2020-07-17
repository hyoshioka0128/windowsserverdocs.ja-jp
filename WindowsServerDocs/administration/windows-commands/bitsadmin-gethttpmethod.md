---
title: bitsadmin gethttpmethod
description: ジョブで使用する HTTP 動詞を取得する bitsadmin gethttpmethod コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 3a963eb275c6e635849094906c52fedf90dccd0d
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927022"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

ジョブで使用する HTTP 動詞を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで使用する HTTP 動詞を取得するには、次のようにします。

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
