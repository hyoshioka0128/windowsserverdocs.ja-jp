---
title: bitsadmin list
description: '**Bitsadmin list**の Windows コマンドに関するトピックでは、現在のユーザーが所有している転送ジョブの一覧を示します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1416965e-e0e6-49cf-b1d4-b286d3cf8716
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1883da7bfa71a41952f6f67e25eca4dbbdd3353c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850325"
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
| /allusers | 省略可。 すべてのユーザーのジョブを一覧表示します。 このパラメーターを使用するには、管理者特権が必要です。 |
| /verbose | 省略可。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、現在のユーザーが所有しているジョブに関する情報を取得します。

```
C:\>bitsadmin /list
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)