---
title: 'ksetup: setrealm'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 453977ac39dd3a52b4f5a3104995f944e4a48392
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724557"
---
# <a name="ksetupsetrealm"></a>ksetup: setrealm



Kerberos 領域の名前を設定します。

## <a name="syntax"></a>構文

```
ksetup /setrealm <DNSDomainName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<DNSDomainName>|DNS ドメイン名は、完全修飾ドメイン名または単純なドメイン名の形式で指定できます。|

## <a name="remarks"></a>Remarks

DNS ドメイン名パラメーターは大文字で入力する必要があります。 それ以外の場合、 **ksetup**コマンドは検証を続行するように要求します。

ドメインコントローラーでの Kerberos 領域の設定はサポートされていません。 これを行おうとすると、警告とコマンドのエラーが発生します。

## <a name="examples"></a>例

このコンピューターの領域を特定のドメイン名に設定して、ドメインコントローラー以外のアクセスを CONTOSO Kerberos 領域のみに制限します。
```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)