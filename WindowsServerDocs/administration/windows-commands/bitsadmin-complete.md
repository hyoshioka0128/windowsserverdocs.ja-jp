---
title: bitsadmin complete
description: Windows コマンド」のトピック**bitsadmin 完了**-ジョブが完了するとします。 このスイッチを使用するまでは、ダウンロードしたファイルを使用できません。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 561585da370f7e69aa3b83b3ddd7579bfc658a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817323"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

ジョブを完了します。 このスイッチを使用するまでは、ダウンロードしたファイルを使用できません。 ジョブが転送の状態に移動した後は、このスイッチを使用します。 それ以外の場合、正常に転送されたファイルのみ利用できます。

## <a name="syntax"></a>構文

```
bitsadmin /complete <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

ジョブの状態を転送すると、BITS はジョブのすべてのファイルを正常に転送が。 ただし、ファイルは使用できませんを使用するまで、**完了/** スイッチします。 複数のジョブを使用して場合*myDownloadJob*という名前で置き換える必要がある*myDownloadJob*ジョブを一意に識別するために、ジョブの GUID を持つ。
```
C:\>bitsadmin /complete myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)