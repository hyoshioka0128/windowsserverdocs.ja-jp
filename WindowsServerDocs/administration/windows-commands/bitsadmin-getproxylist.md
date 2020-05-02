---
title: bitsadmin getproxylist-指定したジョブのプロキシの一覧を取得します。
description: 指定されたジョブのプロキシ一覧を取得する bitsadmin getproxylist コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eebfa727-d8f1-4ae3-9382-6d8ffe8c3df3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a92703d83cc872204d3dc488c15d703dfd50a780
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717655"
---
# <a name="bitsadmin-getproxylist"></a>bitsadmin getproxylist

指定したジョブに使用するプロキシサーバーのコンマ区切りの一覧を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxylist <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのプロキシ一覧を取得するには、次のようにします。

```
bitsadmin /getproxylist myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
