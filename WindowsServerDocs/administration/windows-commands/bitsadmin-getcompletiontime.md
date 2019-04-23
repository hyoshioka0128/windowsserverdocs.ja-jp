---
title: bitsadmin getcompletiontime
description: Windows コマンド」のトピック**bitsadmin getcompletiontime** -ジョブは、データの転送を完了する時間を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3790a91c4b347b982c0f0a023d5977a8d6cd1f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857383"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



データを転送する、ジョブの終了時刻を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、時間、ジョブの名前を*myDownloadJob*データの転送が終了しました。
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)