---
title: bitsadmin getminretrydelay
description: '**Bitsadmin getminretrydelay**の Windows コマンドトピックでは、ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a2bde6340034e48b97b4c86f48a3b2ef72560a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381550"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay



ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetMinRetryDelay <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの最小再試行間隔を取得します。
```
C:\>bitsadmin /GetMinRetryDelay myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)