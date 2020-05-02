---
title: bitsadmin cache と deleteURL
description: Bitsadmin cache および deleteURL コマンドのリファレンストピック。指定された URL のすべてのキャッシュエントリを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e108b76b-fae9-4c16-bf4c-d74c9f025953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 075c48e5c8c205cbbf3fe476260ec7909edcc3e6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718445"
---
# <a name="bitsadmin-cache-and-deleteurl"></a>bitsadmin cache と deleteURL

指定された URL のすべてのキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /deleteURL URL
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| URL | リモートファイルを識別する Uniform Resource Locator。 |

## <a name="examples"></a>例

次のすべての`https://www.contoso.com/en/us/default.aspx`キャッシュエントリを削除するには:

```
bitsadmin /deleteURL https://www.contoso.com/en/us/default.aspx 
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
