---
title: logman update
description: 既存のデータコレクターを更新する logman update コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c98af84f-64ba-40c3-826d-75b80dfb9b34
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0302607f3d2efd9c20f8629e73199567a459d7c8
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222749"
---
# <a name="logman-update"></a>logman update

既存のデータコレクターを更新します。

## <a name="syntax"></a>構文

```
logman update <counter | trace | alert | cfg | api> <[-n] <name>> [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ---------| ----------- |
| [logman 更新カウンター](logman-update-counter.md) | カウンターデータコレクターを更新します。 |
| [logman 更新アラート](logman-update-alert.md) | アラートデータコレクターを更新します。 |
| [logman 更新 cfg](logman-update-cfg.md) | 構成データコレクターを更新します。 |
| [logman 更新 api](logman-update-api.md) | API トレースデータコレクターを更新します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [logman コマンド](logman.md)
