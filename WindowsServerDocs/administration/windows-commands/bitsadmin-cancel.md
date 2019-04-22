---
title: bitsadmin cancel
description: Windows コマンド」のトピック**bitsadmin キャンセル**- 転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7374b544-6a16-4d3e-872c-dcf4c02ad89d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0a4d1e2d6e4fd66cb525316f236d070fcd72d73f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814073"
---
# <a name="bitsadmin-cancel"></a>bitsadmin cancel

転送キューからジョブを削除し、ジョブに関連付けられているすべての一時ファイルを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cancel <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、削除、 *myDownloadJob*転送キューからジョブ。
```
C:\>bitsadmin /cancel myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)