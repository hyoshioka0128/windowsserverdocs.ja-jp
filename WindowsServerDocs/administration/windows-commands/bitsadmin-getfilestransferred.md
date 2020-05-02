---
title: bitsadmin getfilestransferred
description: 指定されたジョブで転送されたファイルの数を取得する bitsadmin getfilestransferred コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed11739029338ecce5fc4efbe1918873a7f37f62
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717914"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred

指定したジョブで転送されたファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getfilestransferred <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブで転送されたファイルの数を取得するには、次のようにします。

```
bitsadmin /getfilestransferred myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
