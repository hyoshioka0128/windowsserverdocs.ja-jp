---
title: bitsadmin cache と setexpirationtime
description: '**Bitsadmin cache と setexpirationtime**の Windows コマンドに関するトピックでは、キャッシュの有効期限が設定されています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf283a0a8b94fd55c591609e3dcd1d127a2be81a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850885"
---
>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache と setexpirationtime

キャッシュの有効期限を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /setexpirationtime secs
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 秒数 | キャッシュの有効期限が切れるまでの秒数。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、キャッシュを60秒で期限切れにします。

```
C:\>bitsadmin /cache / setexpirationtime 60
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
