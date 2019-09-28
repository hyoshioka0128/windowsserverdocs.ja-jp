---
title: bitsadmin complete
description: '**Bitsadmin complete**の Windows コマンドトピックでは、ジョブを完了します。 ダウンロードしたファイルは、このスイッチを使用するまで使用できません。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5a1dc5dbbf2d5b3207b5423f338e0caf4412599
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381818"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

ジョブを完了します。 ダウンロードしたファイルは、このスイッチを使用するまで使用できません。 ジョブが転送済み状態に移行した後に、このスイッチを使用します。 それ以外の場合は、正常に転送されたファイルのみを使用できます。

## <a name="syntax"></a>構文

```
bitsadmin /complete <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

ジョブの状態が [転送済み] になると、そのジョブ内のすべてのファイルが BITS によって正常に転送されます。 ただし、 **[完了]** スイッチを使用するまで、ファイルは使用できません。 複数のジョブが*Mydownloadjob*を名前として使用する場合は、ジョブを一意に識別するために、 *mydownloadjob*をジョブの GUID に置き換える必要があります。
```
C:\>bitsadmin /complete myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)