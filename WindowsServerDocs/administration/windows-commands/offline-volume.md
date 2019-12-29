---
title: オフラインボリューム
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71e507bde827233ce1f15aacd5e13523236a080e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372570"
---
# <a name="offline-volume"></a>オフラインボリューム



オフラインの状態に、オンラインのボリュームがフォーカスを移動します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
offline volume [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   これが成功するには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。
```
offline volume
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

