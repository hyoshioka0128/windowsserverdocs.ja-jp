---
title: nslookup set recurse
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdcdaecdfc6923584a53bc09f985a16ff9b76126
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838395"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse



他のサーバーが情報を持っていない場合にクエリを実行するように、ドメインネームシステム (DNS) ネームサーバーに指示します。

## <a name="syntax"></a>構文

```
set [no]recurse
```

### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                  説明                                                                  |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **norecurse** |                ドメインネームシステム (DNS) ネームサーバーに情報がない場合は、他のサーバーに対してクエリを実行しないようにします。                |
|  **recurse**  | 他のサーバーが情報を持っていない場合にクエリを実行するように、ドメインネームシステム (DNS) ネームサーバーに指示します。 既定の構文は、**再帰**です。 |
|     {ヘルプ     |                                                                      ?}                                                                       |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)