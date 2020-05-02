---
title: bitsadmin cache および delete
description: 特定のキャッシュエントリを削除する bitsadmin cache と delete コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 22540273-55a5-46ea-869b-6df2aa6808a1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62c0c3d5b2cc188e8a8987c7ca502cdeaf932410
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718457"
---
# <a name="bitsadmin-cache-and-delete"></a>bitsadmin cache および delete

特定のキャッシュエントリを削除します。

## <a name="syntax"></a>構文

```
bitsadmin /cache /delete recordID
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a>例

{6511FB02-E195-40A2-B595-E8E2F8F47702} の RecordID を使用してキャッシュエントリを削除するには、次のように入力します。

```
bitsadmin /cache /delete {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
