---
title: bitsadmin cache と delete
description: '**Bitsadmin cache と delete**の Windows コマンドに関するトピックでは、特定のキャッシュエントリが削除されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fd7f1db83a62dd9c1085d6afdcf509c1c3ac8cf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850945"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache と delete

特定のキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を使用して、キャッシュエントリを削除します。

```
C:\>bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)