---
title: bitsadmin cache および info
description: 特定のキャッシュエントリをダンプする bitsadmin cache と info コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a50e6575a5496ff9f7bcd6a0dc429c7960c6933
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718344"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache および info

特定のキャッシュエントリをダンプします。

## <a name="syntax"></a>構文

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>パラメーター

| Paramreter | [説明] |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a>例

RecordID の値 {6511FB02-E195-40A2-B595-E8E2F8F47702} を使用してキャッシュエントリをダンプするには、次のように入力します。

```
bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
