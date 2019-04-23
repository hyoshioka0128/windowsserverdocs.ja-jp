---
title: bitsadmin getcreationtime
description: Windows コマンド」のトピック**bitsadmin getcreationtime** -指定したジョブの作成時間を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: be409cb5-ce72-41d9-aafa-edd4e230fd14
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d8cc0f02933c6a890ae8bf40361d859ad508b319
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858473"
---
# <a name="bitsadmin-getcreationtime"></a>bitsadmin getcreationtime



指定したジョブの作成時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetCreationTime <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブの作成時刻を取得*myDownloadJob*します。
```
C:\>bitsadmin /GetCreationTime myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)