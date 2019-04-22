---
title: bitsadmin suspend
description: Windows コマンド」のトピック**bitsadmin 中断**-指定したジョブを中断します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f9d42500-7bea-4aa8-a9f0-c22f6ed3e73b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87e1bbd1b068d68fb60655043735c6c1aeb07707
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825923"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したジョブを中断します。

## <a name="syntax"></a>構文

```
bitsadmin /Suspend <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

ジョブを再開するには、使用、 [bitsadmin 再開](bitsadmin-resume.md)スイッチします。

## <a name="BKMK_examples"></a>例

次の例は、という名前のジョブを中断します。 *myDownloadJob*します。

```
C:\>bitsadmin /Suspend myDownloadJob
```

#### <a name="additional-references"></a>その他の参照

[コマンドライン構文キー](command-line-syntax-key.md)
