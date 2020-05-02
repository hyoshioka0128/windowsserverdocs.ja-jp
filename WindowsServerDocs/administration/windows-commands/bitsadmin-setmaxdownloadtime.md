---
title: bitsadmin setmaxdownloadtime
description: ダウンロードタイムアウトを秒単位で設定する bitsadmin setmaxdownloadtime コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 16b96cf1-5738-415c-9b9d-c4ea8d5e4fec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8192826570c9dae6aa9d286596336c3e589c9cbd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719686"
---
# <a name="bitsadmin-setmaxdownloadtime"></a>bitsadmin setmaxdownloadtime

ダウンロードタイムアウトを秒単位で設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setmaxdownloadtime <job> <timeout>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| timeout | ダウンロードタイムアウトの長さ (秒単位)。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのタイムアウトを10秒に設定します。

```
bitsadmin /setmaxdownloadtime myDownloadJob 10
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
