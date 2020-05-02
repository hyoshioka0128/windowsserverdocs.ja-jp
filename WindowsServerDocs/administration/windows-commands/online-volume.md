---
title: オンラインボリューム
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb2ee396e4fa8a2e61001df0d979d85dabe1aa32
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723421"
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

|パラメーター|[説明]|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>Remarks

-   このコマンドは、失敗したかが失敗している場合、または、冗長の失敗の状態にするボリュームでは動作します。
-   このコマンドを成功させるには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a>例

ボリュームをオンラインをダウンするには、次のように入力します。
```
online volume
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

