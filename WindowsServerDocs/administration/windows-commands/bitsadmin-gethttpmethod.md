---
title: bitsadmin gethttpmethod
description: ジョブで使用する HTTP 動詞を取得する bitsadmin gethttpmethod コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a458322a5ace69df74df054a537a7365da9e7329
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717891"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

ジョブで使用する HTTP 動詞を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで使用する HTTP 動詞を取得するには、次のようにします。

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
