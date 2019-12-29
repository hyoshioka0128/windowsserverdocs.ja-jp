---
title: bitsadmin setcustomheaders
description: '**Bitsadmin setcustomheaders**の Windows コマンドに関するトピック-GET 要求にカスタム HTTP ヘッダーを追加します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45e3a5178df69b84618966ca0fcd9cc1e6d0e449
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380640"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders



GET 要求にカスタム HTTP ヘッダーを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Header1 .Header2。 . .|ジョブのカスタムヘッダー|

## <a name="remarks"></a>コメント

-   このスイッチは、HTTP サーバーに送信される GET 要求にカスタム HTTP ヘッダーを追加するために使用されます。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのカスタム HTTP ヘッダーを追加します。
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)