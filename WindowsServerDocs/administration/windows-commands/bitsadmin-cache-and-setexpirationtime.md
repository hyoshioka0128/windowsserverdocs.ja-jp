---
title: bitsadmin キャッシュと setexpirationtime
description: Windows コマンド」のトピック**bitsadmin キャッシュと setexpirationtime** -キャッシュの有効期限を設定します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e896df0a88c0cfc4eec07aba4807f184e7abe32
ms.sourcegitcommit: b190fac4bfa5599751a60d3fc3b4c4a64dd9afd7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2019
ms.locfileid: "66008939"
---
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin キャッシュと setexpirationtime
キャッシュの有効期限を設定します。
## <a name="syntax"></a>構文
```
bitsadmin /Cache /SetExpirationtime secs
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|秒|キャッシュの有効期限が切れるまでの秒数です。|
## <a name="BKMK_examples"></a>例
次の例では、60 秒でキャッシュを期限が切れます。
```
C:\>bitsadmin /Cache / SetExpirationtime 60
```
## <a name="additional-references"></a>その他の参照
[コマンド ライン構文の記号](command-line-syntax-key.md)
