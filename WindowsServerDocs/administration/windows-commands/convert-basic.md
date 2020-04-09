---
title: convert basic
description: Windows コマンドに関するトピック「ベーシックディスクに変換する」を参照してください。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e0f6f5f04373042956d83bc9136c884c268e591
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847315"
---
# <a name="convert-basic"></a>convert basic

空のダイナミックディスクをベーシックディスクに変換します。

このコマンドの使用方法については、「[ダイナミックディスクをベーシックディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207048)する方法」 (https://go.microsoft.com/fwlink/?LinkId=207048)を参照してください。

## <a name="syntax"></a>構文

```
convert basic [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換するためには、そのディスクが空である必要があります。 ディスクを変換する前に、データのバックアップをとり、パーティションまたはボリュームをすべて削除してください。

-   この操作を成功させるには、ダイナミックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してダイナミックディスクを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

選択したダイナミックディスクをベーシックに変換するには、次のように入力します。
```
convert basic
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

