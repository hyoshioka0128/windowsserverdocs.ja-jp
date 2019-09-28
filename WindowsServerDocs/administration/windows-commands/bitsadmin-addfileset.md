---
title: bitsadmin addfileset
description: '**Bitsadmin addfileset**の Windows コマンドトピックでは、指定したジョブに1つ以上のファイルを追加します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 464f2da151d5a7bfffde286e52d9158560d48dcc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381990"
---
# <a name="bitsadmin-addfileset"></a>bitsadmin addfileset

指定されたジョブに1つ以上のファイルを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /addfileset <Job> <TextFile>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|TextFile|テキストファイル。各行には、リモートファイル名とローカルファイル名が含まれています。</br>メモ:名前はスペースで区切られています。 # 文字で始まる行は、コメントとして扱われます。|

## <a name="BKMK_examples"></a>例

```
C:\>bitsadmin /addfileset files.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)