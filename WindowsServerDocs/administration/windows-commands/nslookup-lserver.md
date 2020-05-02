---
title: nslookup lserver
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2054c0fd427b41e7d6076258b29ab78d0fb7892
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723673"
---
# <a name="nslookup-lserver"></a>nslookup lserver

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメインネームシステム (DNS) ドメインに既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
lserver <DNSDomain> 
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                      [説明]                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | 既定のサーバーの新しい DNS ドメインを指定します。  |
| {help &#124;?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>Remarks
- **Lserver**コマンドは、初期サーバーを使用して、指定された DNS ドメインに関する情報を検索します。 これは、現在の既定のサーバーを使用する**サーバー**コマンドとは対照的です。
  ## <a name="additional-references"></a>その他のリファレンス
  - [コマンドライン構文のキー](command-line-syntax-key.md)
  [nslookup サーバー](nslookup-server.md)
