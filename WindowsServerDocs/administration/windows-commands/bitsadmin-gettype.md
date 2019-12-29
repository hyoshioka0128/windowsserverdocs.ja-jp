---
title: bitsadmin gettype
description: '**Bitsadmin gettype**の Windows コマンドトピックでは、指定されたジョブのジョブの種類を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca46cb813809621f4fa79b3265198206729a392c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381340"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype



指定されたジョブの種類を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetType <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

ダウンロード、アップロード、アップロード-応答、または不明の種類を使用できます。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのジョブの種類を取得します。
```
C:\>bitsadmin /GetType myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)