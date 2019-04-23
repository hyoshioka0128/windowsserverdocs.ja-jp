---
title: bitsadmin getowner
description: Windows コマンド」のトピック**bitsadmin getowner** -指定したジョブの所有者を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1381bc1268b2b81e2bde18d0d8e17bd760345e0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886713"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

表示名または指定したジョブの所有者の GUID が表示されます。

## <a name="syntax"></a>構文

```
bitsadmin /GetOwner <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブの所有者を表示します。 *myDownloadJob*します。
```
C:\>bitsadmin /GetOwner myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)