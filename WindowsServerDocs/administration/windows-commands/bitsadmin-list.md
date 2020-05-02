---
title: bitsadmin list
description: Bitsadmin list コマンドのリファレンストピック。現在のユーザーが所有している転送ジョブの一覧を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 262589293a147cc1bae98da8fdca047c5f914094
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717430"
---
# <a name="bitsadmin-list"></a>bitsadmin list

現在のユーザーが所有している転送ジョブの一覧を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /list [/allusers][/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| /allusers | 任意。 すべてのユーザーのジョブを一覧表示します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /verbose | 任意。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a>例

現在のユーザーが所有しているジョブに関する情報を取得します。

```
bitsadmin /list
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
