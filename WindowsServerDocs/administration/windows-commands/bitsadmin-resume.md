---
title: bitsadmin resume
description: '**Bitsadmin resume**の Windows コマンドトピックでは、転送キューで新規または中断されたジョブをアクティブ化します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c7540a9-a11a-4910-923a-2a2a61cbf11d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1393e959980b72de09c546ced763a506d334b56c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380771"
---
# <a name="bitsadmin-resume"></a>bitsadmin resume



転送キューで新規または中断されたジョブをアクティブにします。

## <a name="syntax"></a>構文

```
bitsadmin /Resume <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブを再開します。
```
C:\>bitsadmin /Resume myDownloadJob
```
その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)