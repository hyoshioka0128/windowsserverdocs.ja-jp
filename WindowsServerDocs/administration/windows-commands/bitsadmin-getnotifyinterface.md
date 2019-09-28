---
title: bitsadmin getnotifyinterface
description: '**Bitsadmin getnotifyinterface**の Windows コマンドトピック-別のプログラムによって、指定されたジョブの COM コールバックインターフェイスが登録されているかどうかを判断します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 826e13cf8a3e54935ceb5a72ff82647cacfc3be5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381467"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

別のプログラムによって、指定されたジョブの COM コールバックインターフェイス (notify インターフェイス) が登録されているかどうかを判断します。

## <a name="syntax"></a>構文

```
bitsadmin /GetNotifyInterface <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

登録または登録解除されたを表示します。

> [!NOTE]
> コールバックインターフェイスを登録したプログラムを特定することはできません。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの notify インターフェイスを取得します。
```
C:\>bitsadmin /GetNotifyInterface myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)