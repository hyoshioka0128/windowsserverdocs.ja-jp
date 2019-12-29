---
title: 'ksetup: setrealm'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1bbe5c000b7e84066c19511639fe3d92d7e4b558
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374901"
---
# <a name="ksetupsetrealm"></a>ksetup: setrealm



Kerberos 領域の名前を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setrealm <DNSDomainName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DNSDomainName >|DNS ドメイン名は、完全修飾ドメイン名または単純なドメイン名の形式で指定できます。|

## <a name="remarks"></a>コメント

DNS ドメイン名パラメーターは大文字で入力する必要があります。 それ以外の場合、 **ksetup**コマンドは検証を続行するように要求します。

ドメインコントローラーでの Kerberos 領域の設定はサポートされていません。 これを行おうとすると、警告とコマンドのエラーが発生します。

## <a name="BKMK_Examples"></a>例

このコンピューターの領域を特定のドメイン名に設定して、ドメインコントローラー以外のアクセスを CONTOSO Kerberos 領域のみに制限します。
```
ksetup /setrealm CONTOSO
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)