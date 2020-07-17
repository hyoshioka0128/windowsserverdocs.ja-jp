---
title: bitsadmin list
description: Bitsadmin list コマンドの参照記事。現在のユーザーが所有している転送ジョブの一覧が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d9a2c86536ff0910b4e0a8bea15ec43d9371087
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926552"
---
# <a name="bitsadmin-list"></a>bitsadmin list

現在のユーザーが所有している転送ジョブの一覧を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| /allusers | 任意。 すべてのユーザーのジョブを一覧表示します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /verbose | 任意。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a>例

現在のユーザーが所有しているジョブに関する情報を取得します。

```
bitsadmin /list
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
