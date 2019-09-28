---
title: bitsadmin suspend
description: '**Bitsadmin suspend**の Windows コマンドトピックでは、指定されたジョブを中断します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7a3a484df2b50cdc8893512020b835f913793d2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380370"
---
# <a name="bitsadmin-suspend"></a>bitsadmin suspend

> 適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたジョブを中断します。

## <a name="syntax"></a>構文

```
bitsadmin /Suspend <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

ジョブを再開するには、 [bitsadmin resume](bitsadmin-resume.md)スイッチを使用します。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブを一時停止します。

```
C:\>bitsadmin /Suspend myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
