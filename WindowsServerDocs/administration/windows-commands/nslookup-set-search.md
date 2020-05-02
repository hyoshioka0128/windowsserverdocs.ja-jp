---
title: nslookup set search
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 064ac660-8b04-4af9-8b2c-e4e0549771b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e3f5bce42d3614b535b2dfb00c4c9ea9cac2346
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723564"
---
# <a name="nslookup-set-search"></a>nslookup set search



DNS ドメイン検索リスト内のドメインネームシステム (DNS) ドメイン名を、応答が受信されるまで要求に追加します。 これは、セットと参照要求に少なくとも1つのピリオドが含まれている場合に適用されますが、末尾にピリオドは付きません。

## <a name="syntax"></a>構文

```
set [no]search
```

### <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                          [説明]                                                                          |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **nosearch** |                            DNS ドメイン検索リスト内のドメインネームシステム (DNS) ドメイン名を要求に追加しないようにします。                            |
|  **search**  | DNS ドメイン検索リスト内のドメインネームシステム (DNS) ドメイン名を、応答が受信されるまで要求に追加します。 既定の構文は**search**です。 |
|    {ヘルプ     |                                                                              ?}                                                                               |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)