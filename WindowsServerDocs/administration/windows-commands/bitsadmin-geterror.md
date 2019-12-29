---
title: bitsadmin geterror
description: '**Bitsadmin geterror**の Windows コマンドトピックでは、指定されたジョブの詳細なエラー情報を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cbe5bca1-d2dd-4ce6-903f-f85de4a2ec6a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f9bd607886d00ede4e1da91ed73eff2794db6ce
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381644"
---
# <a name="bitsadmin-geterror"></a>bitsadmin geterror



指定されたジョブの詳細なエラー情報を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetError <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのエラー情報を取得します。
```
C:\>bitsadmin /GetError myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)