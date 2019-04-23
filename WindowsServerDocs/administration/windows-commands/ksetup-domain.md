---
title: ksetup:domain
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f53e807891b434709b1a8faed7aae8e8d444f6e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857453"
---
# <a name="ksetupdomain"></a>ksetup:domain



Kerberos のすべての操作のドメイン名を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /domain <DomainName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドメイン名 >|接続を確立するドメインの名前です。 完全修飾ドメイン名または contoso.com または contoso など、名前の単純なフォームを使用します。|

## <a name="remarks"></a>注釈

なし。

## <a name="BKMK_Examples"></a>例

/Mapuser サブコマンドを使用して、Microsoft などの有効なドメインへの接続を確立します。
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
接続が成功したら、新しい受け取ります TGT または既存の TGT は更新されます。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)