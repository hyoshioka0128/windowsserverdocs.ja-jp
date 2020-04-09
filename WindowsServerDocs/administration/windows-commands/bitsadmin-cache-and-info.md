---
title: bitsadmin cache と info
description: 特定のキャッシュエントリをダンプする**bitsadmin cache および info**の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 15975cbf-dba6-49ca-a725-d15ce1952de5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9c6ce1eb972a76408483b8a27a3abca5500e56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850895"
---
# <a name="bitsadmin-cache-and-info"></a>bitsadmin cache と info

特定のキャッシュエントリをダンプします。

## <a name="syntax"></a>構文

```
bitsadmin /cache /info recordID [/verbose]
```

### <a name="parameters"></a>パラメーター

| Paramreter | 説明 |
| -------------- | -------------- |
| recordID | キャッシュエントリに関連付けられている GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、recordID の値が {6511FB02-E195-40A2-B595-E8E2F8F47702} であるキャッシュエントリをダンプします。

```
C:\>bitsadmin /cache /info {6511FB02-E195-40A2-B595-E8E2F8F47702}
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)