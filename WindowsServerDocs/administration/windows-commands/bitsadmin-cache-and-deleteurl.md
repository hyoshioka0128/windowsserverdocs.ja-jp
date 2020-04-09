---
title: bitsadmin cache と deleteurl
description: '**Bitsadmin cache および deleteurl**の Windows コマンドに関するトピックでは、指定された url のすべてのキャッシュエントリを削除します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70099e795d0f05d0fcf75fbf6b82f5466d1c0c55
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850935"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin cache と deleteurl

指定された URL のすべてのキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /deleteURL url
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| url | リモートファイルを識別する Uniform Resource Locator。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、のすべてのキャッシュエントリを削除し `https://www.contoso.com/en/us/default.aspx`

```
C:\>bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)