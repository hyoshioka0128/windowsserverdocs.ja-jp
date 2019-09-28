---
title: bitsadmin getreplyprogress
description: '**Bitsadmin getreplyprogress**の Windows コマンドトピックでは、サーバーの応答のサイズと進行状況を取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f7cb0b4-ad95-44fd-a35d-0ddf5fc0b0d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c791fe98271b497e5ecf48338ab3bbb0cc50de98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381243"
---
# <a name="bitsadmin-getreplyprogress"></a>bitsadmin getreplyprogress

サーバー応答のサイズと進行状況を取得します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /GetReplyProgress <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

アップロード/応答ジョブに対してのみ有効です。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの応答の進行状況を取得します。
```
C:\>bitsadmin /GetReplyProgress myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)