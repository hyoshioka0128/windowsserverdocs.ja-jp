---
title: オフラインボリューム
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b8f7192f-ea38-47d0-9d4e-58ef68336ae6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d17295f3367fed054a7f6a245bae44ea3494a4a8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723449"
---
# <a name="offline-volume"></a>オフラインボリューム



オフラインの状態に、オンラインのボリュームがフォーカスを移動します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
offline volume [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>Remarks

-   これが成功するには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。
```
offline volume
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

