---
title: bitsadmin setcustomheaders
description: '**Bitsadmin setcustomheaders**の Windows コマンドに関するトピックでは、GET 要求にカスタム HTTP ヘッダーを追加します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed926410-80d0-46ed-9a90-f752c164bb9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b5b1a28f03815a22a3f8d10b2c3d1d4a3a2ae635
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123024"
---
# <a name="bitsadmin-setcustomheaders"></a>bitsadmin setcustomheaders

HTTP サーバーに送信される GET 要求にカスタム HTTP ヘッダーを追加します。

## <a name="syntax"></a>構文

```
bitsadmin /setcustomheaders <job> <header1> <header2> <...>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| `<header1> <header2>` | ジョブのカスタムヘッダー。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのカスタム HTTP ヘッダーを追加します。 GET 要求の詳細については、「[メソッドの定義](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html#sec9.3)」および「[ヘッダーフィールドの定義](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)」を参照してください。

```
C:\>bitsadmin /setcustomheaders myDownloadJob accept-encoding:deflate/gzip
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)