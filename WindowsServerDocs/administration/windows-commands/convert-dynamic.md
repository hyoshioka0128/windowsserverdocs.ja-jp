---
title: convert dynamic
description: ベーシックディスクをダイナミックディスクに変換する、[動的変換] の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7b8fa4b1-850f-4e48-b05f-871c883ea33c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ad84cf2ecb6808b68110187b52f3fc13590b491
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847325"
---
# <a name="convert-dynamic"></a>convert dynamic

ベーシック ディスクをダイナミック ディスクに変換します。

このコマンドの使用方法については、「[ベーシックディスクをダイナミックディスクに変更](https://go.microsoft.com/fwlink/?LinkId=207047)する方法」 (https://go.microsoft.com/fwlink/?LinkId=207047)を参照してください。

## <a name="syntax"></a>構文

```
convert dynamic [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   ベーシックディスク上の既存のパーティションは、単純ボリュームになります。
-   この操作を成功させるには、ベーシックディスクを選択する必要があります。 **[ディスクの選択**] コマンドを使用してベーシックディスクを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

ベーシックディスクをダイナミックディスクに変換するには、次のように入力します。
```
convert dynamic
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

