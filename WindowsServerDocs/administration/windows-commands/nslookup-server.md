---
title: nslookup server
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 608267f8-f7b4-412a-8dcd-e08b5ffc2085
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e24e55026d12a0d8afc5b6f1bef926ece9087bd0
ms.sourcegitcommit: 6423dfa9cecb3b06bdd563cae113c3e80a4ec330
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71105014"
---
# <a name="nslookup-server"></a>nslookup server

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメインネームシステム (DNS) ドメインに既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
server <DNSDomain>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                          説明                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | 必須。 既定のサーバーの新しい DNS ドメインを指定します。 |
| {ヘルプ&#124; ?} |     **Nslookup**サブコマンドの簡単な概要を表示します。      |

## <a name="remarks"></a>コメント
- **サーバー**コマンドは、現在の既定のサーバーを使用して、指定された DNS ドメインに関する情報を検索します。 これは、最初のサーバーを使用する**lserver**コマンドとは対照的です。
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
