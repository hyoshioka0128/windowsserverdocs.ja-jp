---
title: nslookup server
description: 'Windows コマンド」のトピック * * *- '
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
ms.openlocfilehash: ba58e223d0aa35b4157b813b10bf1d274313a1c1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436970"
---
# <a name="nslookup-server"></a>nslookup server

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン ネーム システム (DNS) ドメインには、既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
server <DNSDomain>
```
## <a name="parameters"></a>パラメーター

|    パラメーター    |                          説明                           |
|-----------------|----------------------------------------------------------------|
|   <DNSDomain>   | 必須。 新しい DNS ドメインは、既定のサーバーを指定します。 |
| {help &#124; ?} |     簡単な概要を表示します。 **nslookup**サブコマンドします。      |

## <a name="remarks"></a>注釈
- **Server**コマンドは現在の既定のサーバーを使用して、指定した DNS ドメインについての情報を確認します。 これとは対照的に、 **lserver**コマンドで、初期のサーバーを使用します。
  ## <a name="additional-references"></a>その他の参照
  [コマンドライン構文のポイント](command-line-syntax-key.md)
  [nslookup lserver](nslookup-lserver.md)
