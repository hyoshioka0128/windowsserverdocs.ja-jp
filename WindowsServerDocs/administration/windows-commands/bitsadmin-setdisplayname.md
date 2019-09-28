---
title: bitsadmin setdisplayname
description: '**Bitsadmin setdisplayname**の Windows コマンドトピックでは、指定されたジョブの表示名を設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10a5607eb26f8199ec415a4cec17d03015a26bcd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380635"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



指定されたジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|DisplayName|指定されたジョブの表示名に使用されるテキスト。|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの表示名を*myDownloadJob2*に設定します。
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)