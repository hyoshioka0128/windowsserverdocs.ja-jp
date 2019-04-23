---
title: bitsadmin addfileset
description: Windows コマンド」のトピック**bitsadmin addfileset** -指定されたジョブに 1 つまたは複数のファイルを追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75466994-262f-4724-b14d-f813c5397675
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8f6ff32dfa6042272c68647477d77183ce9cb76
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889443"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

指定したジョブを 1 つまたは複数のファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfileset <Job> <TextFile>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|TextFile|テキスト ファイル、対象の各の行には、リモートとローカルのファイル名が含まれています。</br>注:名前は、スペースで区切られました。 # 文字で始まる行はコメントとして扱われます。|

## <a name="BKMK_examples"></a>例

```
C:\>bitsadmin /addfileset files.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)