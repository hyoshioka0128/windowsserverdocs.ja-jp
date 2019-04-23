---
title: オンラインのボリューム
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6bacba1e204f1eee2e3d4772ff9024aedbfc4fed
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882003"
---
# <a name="online-volume"></a>オンラインのボリューム



ボリュームをオンライン状態には現在オフラインになっています。

> [!IMPORTANT]
> このコマンドでは、Windows Vista のエディションでは使用できません。

> [!IMPORTANT]
> 読み取り専用ボリュームで使用されている場合、このコマンドは失敗します。

## <a name="syntax"></a>構文

```
online volume [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   このコマンドは、失敗したかが失敗している場合、または、冗長の失敗の状態にするボリュームでは動作します。
-   このコマンドを成功させるには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ボリュームをオンラインをダウンするには、次のように入力します。
```
online volume
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

