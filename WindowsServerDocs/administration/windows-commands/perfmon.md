---
title: perfmon
description: 特定のスタンドアロンモードで Windows 信頼性とパフォーマンスモニターを起動する perfmon コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 96d1589dcd75814c37c2ad295cf60887eb07739c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472478"
---
# <a name="perfmon"></a>perfmon

特定のスタンドアロンモードで Windows 信頼性とパフォーマンスモニターを起動します。

## <a name="syntax"></a>構文

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| /res | リソースビューを開始します。 |
| /report」 | システム診断データコレクターセットを開始し、結果のレポートを表示します。 |
| /rel | 信頼性モニターを起動します。 |
| /sys | パフォーマンスモニターを起動します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Windows パフォーマンス モニタ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
