---
title: bitsadmin getbytestotal
description: 指定されたジョブのサイズを取得する bitsadmin getbytestotal コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 784e0bfa-7b09-4262-9104-adbc9beb479b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f844e1d3689c42a2c533921797d15dbb946b551e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718160"
---
# <a name="bitsadmin-getbytestotal"></a>bitsadmin getbytestotal

指定されたジョブのサイズを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getbytestotal <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのサイズを取得するには、次のようにします。

```
bitsadmin /getbytestotal myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
