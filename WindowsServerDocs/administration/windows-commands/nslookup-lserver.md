---
title: nslookup lserver
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aee5ea0b-bb17-4c14-bde7-2f7a91f2f22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d0d8619101d2e7b1f7fb6d6ed99d801c7c264f1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838635"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメインネームシステム (DNS) ドメインに既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
lserver <DNSDomain> 
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                      説明                      |
|-----------------|-------------------------------------------------------|
|   <DNSDomain>   | 既定のサーバーの新しい DNS ドメインを指定します。  |
| {ヘルプ&#124; ?} | **Nslookup**サブコマンドの簡単な概要を表示します。 |

## <a name="remarks"></a>コメント
- **Lserver**コマンドは、初期サーバーを使用して、指定された DNS ドメインに関する情報を検索します。 これは、現在の既定のサーバーを使用する**サーバー**コマンドとは対照的です。
  ## <a name="additional-references"></a>その他の参照情報
  - [Nslookup サーバー](nslookup-server.md)
  [コマンドライン構文のキー](command-line-syntax-key.md)
