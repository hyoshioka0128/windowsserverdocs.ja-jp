---
title: nslookup set recurse
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b7a93f-dfb0-4ccd-b230-e0953057fada
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68a5dc26387ddeb6541cc1c85005cd9dab4b433a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372886"
---
# <a name="nslookup-set-recurse"></a>nslookup set recurse



他のサーバーが情報を持っていない場合にクエリを実行するように、ドメインネームシステム (DNS) ネームサーバーに指示します。

## <a name="syntax"></a>構文

```
set [no]recurse
```

## <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                  説明                                                                  |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **norecurse** |                ドメインネームシステム (DNS) ネームサーバーに情報がない場合は、他のサーバーに対してクエリを実行しないようにします。                |
|  **recurse**  | 他のサーバーが情報を持っていない場合にクエリを実行するように、ドメインネームシステム (DNS) ネームサーバーに指示します。 既定の構文は、**再帰**です。 |
|     {ヘルプ     |                                                                      ?}                                                                       |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)