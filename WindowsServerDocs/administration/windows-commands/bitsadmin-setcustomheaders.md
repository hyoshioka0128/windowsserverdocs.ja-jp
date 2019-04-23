---
title: bitsadmin setcustomheaders
description: Windows コマンド」のトピック**bitsadmin setcustomheaders** -GET 要求にカスタム HTTP ヘッダーを追加します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6d90ac2d23b852ae0c2114e7cd5a9c9e6382ce8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853853"
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
|-ヘッダー 1-ヘッダー 2。 . .|ジョブのカスタム ヘッダー|

## <a name="remarks"></a>注釈

-   このスイッチを使用して、HTTP サーバーに送信された GET 要求にカスタム HTTP ヘッダーを追加します。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブのカスタム HTTP ヘッダー *myDownloadJob*します。
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob "Accept-encoding:deflate/gzip"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)