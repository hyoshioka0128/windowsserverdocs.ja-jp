---
title: bitsadmin cache および info
description: 特定のキャッシュエントリをダンプする bitsadmin cache と info コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 537c6173718d8c7deb421915b2ef9697472600a2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894792"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache および info

特定のキャッシュエントリをダンプします。

## <a name="syntax"></a>構文

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>パラメーター

| Paramreter | 説明 |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a>例

RecordID の値 {6511FB02-E195-40A2-B595-E8E2F8F47702} を使用してキャッシュエントリをダンプするには、次のように入力します。

```
bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin cache コマンド](bitsadmin-cache.md)
