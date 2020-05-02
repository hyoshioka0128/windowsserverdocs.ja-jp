---
title: perfmon
description: Perfmon のリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 5742b51ffd4fca16c1054e373636afbe39968c96
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723325"
---
# <a name="perfmon"></a>perfmon

特定のスタンドアロンモードで Windows 信頼性とパフォーマンスモニターを起動します。

## <a name="syntax"></a>構文

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|/res|リソースビューを開始します。|
|/report」|システム診断データコレクターセットを起動し、結果のレポートを表示します。|
|/rel|信頼性モニターを起動します。|
|/sys|パフォーマンス モニターを起動します。|

## <a name="additional-references"></a>その他のリファレンス

[Windows パフォーマンス モニタ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
