---
title: イメージ ファイルの get コマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c8136585e04caca02ab16c7b4ca11a825cf400d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392134"
---
# <a name="using-the-get-imagefile-command"></a>イメージ ファイルの get コマンドを使用してください。



Windows イメージ (.wim) ファイルに含まれるイメージに関する情報を取得します。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/ImageFile: \<WIM ファイルパス >|.Wim ファイルの完全パスとファイル名を指定します。|
|[/詳細]|各イメージからすべてのイメージのメタデータを返します。 このオプションを使用しない場合、既定の動作は、イメージの名前、説明、およびファイル名のみを返すには。|

## <a name="BKMK_examples"></a>例

イメージに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-ImageFile /ImageFile:"C:\temp\install.wim"
```
詳細な情報を表示するには、次のように入力します。
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:"\\Server\Share\My Folder \install.wim" /Detailed
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)