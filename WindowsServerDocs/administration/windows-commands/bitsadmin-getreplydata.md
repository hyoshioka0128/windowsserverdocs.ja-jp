---
title: bitsadmin getreplydata
description: '**Bitsadmin getreplydata**の Windows コマンドトピックでは、サーバーの応答データを16進形式で取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 819f97d5-b255-4b2d-9f63-0daa73915434
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ebd3ee77e5d442467f49bb209c560f089f2271b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381278"
---
# <a name="bitsadmin-getreplydata"></a>bitsadmin getreplydata

サーバーの応答データを16進形式で取得します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetReplyData <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

アップロード/応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの応答データを取得します。
```
C:\>bitsadmin /GetReplyData myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)