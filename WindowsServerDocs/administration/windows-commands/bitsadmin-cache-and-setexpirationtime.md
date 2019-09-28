---
title: bitsadmin cache と setexpirationtime
description: '**Bitsadmin cache と setexpirationtime**の Windows コマンドに関するトピックでは、キャッシュの有効期限を設定します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 386c6659e4410b41669ade39d8af97829d81a1cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381921"
---
>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin cache と setexpirationtime
キャッシュの有効期限を設定します。
## <a name="syntax"></a>構文
```
bitsadmin /Cache /SetExpirationtime secs
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|秒|キャッシュの有効期限が切れるまでの秒数。|
## <a name="BKMK_examples"></a>例
次の例では、キャッシュを60秒で期限切れにします。
```
C:\>bitsadmin /Cache / SetExpirationtime 60
```
## <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
