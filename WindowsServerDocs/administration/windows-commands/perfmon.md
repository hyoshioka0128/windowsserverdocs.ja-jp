---
title: perfmon
description: 特定のスタンドアロンモードで Windows 信頼性とパフォーマンスモニターを起動する perfmon コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 5beaa1692f3fc4aa66eae81069f0ead5839d22e3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922840"
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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Windows パフォーマンス モニタ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
