---
title: bdehdcfg restart
description: Bdehdcfg restart の Windows コマンドのトピック-ドライブの準備が完了した後にコンピューターを再起動する必要があることを bdehdcfg に指示します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a98b76bb-36f1-4790-b337-7dc35f606bc6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6c4e48b051f567c98ea679feaa22f995982a899
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382214"
---
# <a name="bdehdcfg-restart"></a>bdehdcfg: 再起動



ドライブの準備が完了した後にコンピューターを再起動する必要があることを Bdehdcfg コマンドラインツールに通知します。 このコマンドを使用する方法の例については、「[例](#BKMK_Examples)」を参照してください。

## <a name="syntax"></a>構文

```
bdehdcfg -target {default|unallocated|<DriveLetter> shrink|<DriveLetter> merge} -restart
```

### <a name="parameters"></a>パラメーター

このコマンドは、追加のパラメーターを受け取りません。

## <a name="remarks"></a>コメント

他のユーザーがコンピューターにログオンしていて、 **quiet**コマンドが指定されていない場合は、コンピューターを再起動するかどうかを確認するプロンプトが表示されます。

## <a name="BKMK_Examples"></a>例

次の例は、 **restart**コマンドの使用方法を示しています。
```
bdehdcfg -target default -restart
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Bdehdcfg](bdehdcfg.md)