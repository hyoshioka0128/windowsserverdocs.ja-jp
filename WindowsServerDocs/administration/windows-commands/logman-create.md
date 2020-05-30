---
title: logman create
description: Logman create コマンドのリファレンストピックでは、カウンター、トレース、構成データコレクター、または API を作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 972f0126-7bc4-4b14-9265-062864f3ffd4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4a68be098f868cdd9cd48c1e7c68fc183fa1fab
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222953"
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
| [logman カウンターの作成](logman-create-counter.md) | カウンターデータコレクターを作成します。 |
| [logman 作成トレース](logman-create-trace.md) | トレースデータコレクターを作成します。 |
| [logman 作成アラート](logman-create-alert.md) | アラートデータコレクターを作成します。 |
| [logman 作成 cfg](logman-create-cfg.md) | 構成データコレクターを作成します。 |
| [logman api の作成](logman-create-api.md) | API トレースデータコレクターを作成します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman コマンド](logman.md)