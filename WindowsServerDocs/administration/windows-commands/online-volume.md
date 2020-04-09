---
title: オンラインボリューム
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 476dd893e7899a2bd58336546a7881934f415f92
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837845"
---
# <a name="online-volume"></a>オンラインボリューム



ボリュームをオンライン状態には現在オフラインになっています。

> [!IMPORTANT]
> このコマンドは、Windows Vista のどのエディションでも使用できません。

> [!IMPORTANT]
> 読み取り専用ボリュームで使用されている場合、このコマンドは失敗します。

## <a name="syntax"></a>構文

```
online volume [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   このコマンドは、失敗したかが失敗している場合、または、冗長の失敗の状態にするボリュームでは動作します。
-   このコマンドを成功させるには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例

ボリュームをオンラインをダウンするには、次のように入力します。
```
online volume
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

