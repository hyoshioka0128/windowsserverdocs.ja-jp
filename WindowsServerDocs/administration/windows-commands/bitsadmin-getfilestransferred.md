---
title: bitsadmin getfilestransferred
description: Windows コマンド」のトピック**bitsadmin getfilestransferred** -指定したジョブの転送されたファイルの数を取得します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e282815c-938b-4ac0-a09d-9baafb656dcb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5df7f2abfdad6780878b1f00da44c772eecf9fba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822263"
---
# <a name="bitsadmin-getfilestransferred"></a>bitsadmin getfilestransferred



指定したジョブの転送ファイルの数を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetFilesTransferred <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブで転送されるファイルの数を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetFilesTransferred myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)