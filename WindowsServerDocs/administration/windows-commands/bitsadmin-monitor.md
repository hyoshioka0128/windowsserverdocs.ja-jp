---
title: bitsadmin monitor
description: Bitsadmin monitor コマンドのリファレンストピックでは、現在のユーザーが所有している転送キュー内のジョブを監視します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2c424d27-e011-49c2-b579-a2c235467c39
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c8fa52f9fcf30a66b41c9cdbf7b7e1fab69f06e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717377"
---
# <a name="bitsadmin-monitor"></a>bitsadmin monitor

現在のユーザーが所有している転送キュー内のジョブを監視します。

## <a name="syntax"></a>構文

```
bitsadmin /monitor [/allusers] [/refresh <seconds>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| /allusers | 任意。 すべてのユーザーのジョブを監視します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /更新 | 任意。 によって`<seconds>`指定された間隔でデータを更新します。 既定の更新間隔は5秒です。 更新を停止するには、CTRL + C キーを押します。 |

## <a name="examples"></a>例

現在のユーザーが所有しているジョブの転送キューを監視し、60秒ごとに情報を更新すること。

```
bitsadmin /monitor /refresh 60
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
