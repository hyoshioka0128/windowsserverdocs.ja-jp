---
title: bitsadmin getdisplayname
description: '**Bitsadmin getdisplayname**の Windows コマンドに関するトピックでは、指定されたジョブの表示名を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e5c0e76c-4cc6-42d8-ac30-30bf3dc11b9b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 229bd245f9e810fc6aeb856bbfba253b9ab8a9f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381629"
---
# <a name="bitsadmin-getdisplayname"></a>bitsadmin getdisplayname



指定されたジョブの表示名を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetDisplayName <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの表示名を取得します。
```
C:\>bitsadmin /GetDisplayName myDownloadJob
```
その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)