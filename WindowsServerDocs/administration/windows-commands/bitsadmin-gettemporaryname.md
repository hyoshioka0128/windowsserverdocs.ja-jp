---
title: bitsadmin gettemporaryname
description: Windows コマンド」のトピック**bitsadmin gettemporaryname** -ジョブ内の指定されたファイルの一時ファイル名を報告します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68925edc-a801-4292-a812-7471c4f60fdd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 762a2a5943202b38e94a245b74745e6631e0792d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876713"
---
# <a name="bitsadmin-gettemporaryname"></a>bitsadmin gettemporaryname



ジョブ内の指定されたファイルの一時ファイル名を報告します。

## <a name="syntax"></a>構文

```
bitsadmin /GetTemporaryName <Job> <file index> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|ファイルのインデックス|0 から始まります|

## <a name="BKMK_examples"></a>例

次の例では、ファイル 2 という名前のジョブの一時ファイル名をレポートする*myJob*します。
```
C:\>bitsadmin /GetTemporaryName myJob 1 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)