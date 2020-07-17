---
title: bitsadmin getfilestransferred
description: Bitsadmin getfilestransferred コマンドの参照記事。指定されたジョブで転送されたファイルの数を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43257dcb8350974bfb258a9970c1a6fec787a226
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928256"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

指定したジョブで転送されたファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで転送されたファイルの数を取得するには、次のようにします。

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
