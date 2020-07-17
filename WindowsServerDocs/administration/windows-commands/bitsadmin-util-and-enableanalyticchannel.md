---
title: bitsadmin util および enableanalyticchannel
description: BITS クライアント分析チャネルを有効または無効にする bitsadmin util および enableanalytics のチャネルコマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0d7645aa-b91b-4ed7-b630-a1e1be6f6ae9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 515402f42dee54baa662f37718841f70b1cd2882
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927416"
---
# <a name="bitsadmin-util-and-enableanalyticchannel"></a>bitsadmin util および enableanalyticchannel

BITS クライアント分析チャネルを有効または無効にします。

## <a name="syntax"></a>Syntax

```
bitsadmin /util /enableanalyticchannel TRUE|FALSE
```

| パラメーター | 説明 |
| --------- | ---------- |
| TRUE または FALSE | **TRUE**を指定すると、指定したファイルのコンテンツの検証が有効になり、 **FALSE**の場合は無効になります。 |

## <a name="examples"></a>例

BITS クライアントの分析チャネルをオンまたはオフにします。

```
bitsadmin /util / enableanalyticchannel TRUE
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin util コマンド](bitsadmin-util.md)

- [bitsadmin コマンド](bitsadmin.md)
