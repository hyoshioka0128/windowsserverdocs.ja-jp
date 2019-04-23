---
title: bitsadmin getvalidationstate
description: 'Windows コマンド」のトピック**bitsadmin getvalidationstate** -ジョブ内の指定されたファイルのコンテンツの検証状態を報告します。 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6ada3f1f-9967-4262-9d22-ed641e23f516
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8abff3fc9fddb9cff1758739fdc540a9c945efe2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879163"
---
# <a name="bitsadmin-getvalidationstate"></a>bitsadmin getvalidationstate



ジョブ内の指定されたファイルのコンテンツの検証の状態を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /GetValidationState <Job> <file index> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ファイルのインデックス|0 から始まります|

## <a name="BKMK_examples"></a>例

次の例では、ファイル 2 という名前のジョブ内のコンテンツの検証の状態を取得します。 *myJob*します。
```
C:\>bitsadmin /GetValidationState myJob 1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)