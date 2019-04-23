---
title: nslookup lserver
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0c4e1ed4697666062bb90f4a9c65054a3dd73661
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848053"
---
# <a name="nslookup-lserver"></a>nslookup lserver

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたドメイン ネーム システム (DNS) ドメインには、既定のサーバーを変更します。
## <a name="syntax"></a>構文
```
lserver <DNSDomain> 
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<DNSDomain>|新しい DNS ドメインは、既定のサーバーを指定します。|
|{help &#124; ?}|簡単な概要を表示します。 **nslookup**サブコマンドします。|
## <a name="remarks"></a>注釈
-   **Lserver**コマンドは最初のサーバーを使用して、指定した DNS ドメインについての情報を確認します。 これとは対照的に、 **server**コマンドで、現在の既定のサーバーを使用します。
## <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[nslookup サーバー](nslookup-server.md)
