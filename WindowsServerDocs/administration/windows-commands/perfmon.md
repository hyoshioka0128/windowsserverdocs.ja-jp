---
title: perfmon
description: Perfmon の Windows コマンドに関するトピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8d5eca-8473-463e-a6e0-7bbd590b18e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/25/2018
ms.openlocfilehash: 7a832416b5b00292a6249f3824644db1b727cfb2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837605"
---
# <a name="perfmon"></a>perfmon

特定のスタンドアロンモードで Windows 信頼性とパフォーマンスモニターを起動します。

## <a name="syntax"></a>構文

```
perfmon </res|report|rel|sys>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/res|リソースビューを開始します。|
|/report」|システム診断データコレクターセットを起動し、結果のレポートを表示します。|
|/rel|信頼性モニターを起動します。|
|/sys|パフォーマンス モニターを起動します。|

## <a name="additional-references"></a>その他の参照情報

[Windows パフォーマンスモニター](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749154(v%3dws.11))
