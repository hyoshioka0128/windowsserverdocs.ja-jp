---
title: bitsadmin geterrorcount
description: '**Bitsadmin geterrorcount**の Windows コマンドトピックでは、指定されたジョブが一時的なエラーを生成した回数のカウントを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e5aa64c0e080e946e84c0bf804527bb00cad70a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381622"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount



指定したジョブが一時的なエラーを生成した回数のカウントを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetErrorCount <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのエラー数情報を取得します。
```
C:\>bitsadmin /GetErrorCount myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)