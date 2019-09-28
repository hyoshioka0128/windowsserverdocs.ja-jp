---
title: nslookup lserver
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 347ad6e380f8d8163c4954771c9e985271b2d549
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373077"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメインネームシステム (DNS) ドメインに既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                      説明                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | 既定のサーバーの新しい DNS ドメインを指定します。  |
| {ヘルプ&#124; ?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>コメント
- **Lserver**コマンドは、初期サーバーを使用して、指定された DNS ドメインに関する情報を検索します。 これは、現在の既定のサーバーを使用する**サーバー**コマンドとは対照的です。
  ## <a name="additional-references"></a>その他の参照情報
  [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup サーバー](nslookup-server.md)
