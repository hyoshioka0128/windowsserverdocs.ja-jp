---
title: bitsadmin setdescription
description: '**Bitsadmin setdescription**の Windows コマンドトピック-指定したジョブの説明を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d140ee9d575828a1a4d536073e468c9b4e56799f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380932"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin setdescription



指定されたジョブの説明を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetDescription <Job> <Description>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|説明|ジョブを説明するために使用されるテキストです。|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの説明を取得します。
```
C:\>bitsadmin /SetDescription myDownloadJob "Music Downloads"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)