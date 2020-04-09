---
title: bitsadmin setcustomheaders
description: Bitsadmin setcustomheaders の Windows コマンドに関するトピックでは、GET 要求にカスタム HTTP ヘッダーを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e5d97fae5f84637c80c3d1ef00aa36f09049bb17
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849615"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

GET 要求にカスタム HTTP ヘッダーを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /SetCustomHeaders <Job> <Header1> <Header2> <. . .>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Header1 .Header2。 。 。|ジョブのカスタムヘッダー|

## <a name="remarks"></a>コメント

-   このスイッチは、HTTP サーバーに送信される GET 要求にカスタム HTTP ヘッダーを追加するために使用されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのカスタム HTTP ヘッダーを追加します。
```
C:\>bitsadmin / SetCustomHeaders myDownloadJob Accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)