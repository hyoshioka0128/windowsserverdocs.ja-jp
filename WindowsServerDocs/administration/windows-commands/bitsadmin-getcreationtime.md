---
title: bitsadmin getcreationtime
description: 指定されたジョブの作成時刻を取得する bitsadmin get time コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc6ca5ad23730e9f57d58e069e0a2daf961930e8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718103"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime

指定されたジョブの作成時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getcreationtime <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの作成時刻を取得するには、次のようにします。

```
bitsadmin /getcreationtime myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
