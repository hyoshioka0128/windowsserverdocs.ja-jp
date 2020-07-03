---
title: logman create
description: Logman create コマンドのリファレンス記事。カウンター、トレース、構成データコレクター、または API を作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 695a101a0aa6a720b64ffee6617085d13b6e83d1
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922323"
---
# <a name="logman-create"></a>logman create

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カウンター、トレース、構成データコレクター、または API を作成します。

## <a name="syntax"></a>構文

```
logman create <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [logman create counter](logman-create-counter.md) | カウンターデータコレクターを作成します。 |
| [logman create trace](logman-create-trace.md) | トレースデータコレクターを作成します。 |
| [logman create alert](logman-create-alert.md) | アラートデータコレクターを作成します。 |
| [logman create cfg](logman-create-cfg.md) | 構成データコレクターを作成します。 |
| [logman create api](logman-create-api.md) | API トレースデータコレクターを作成します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman コマンド](logman.md)