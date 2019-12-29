---
title: 'ksetup: ドメイン'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 0a4d9f09def32c7518046c25887f4154020c5d7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375116"
---
# <a name="ksetupdomain"></a>ksetup: ドメイン



すべての Kerberos 操作のドメイン名を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /domain <DomainName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DomainName >|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (contoso.com や contoso など) を使用します。|

## <a name="remarks"></a>コメント

[なし] :

## <a name="BKMK_Examples"></a>例

次のように、/mapuser サブコマンドを使用して、Microsoft などの有効なドメインへの接続を確立します。
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
接続に成功すると、新しい TGT が送信されるか、既存の TGT が更新されます。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)