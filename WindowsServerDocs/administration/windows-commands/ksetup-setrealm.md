---
title: 'ksetup: setrealm'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ab268c40-276b-46ef-ab16-d5ce7667fbed
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: acdbfaabe341c8efb19c6e9d183022375f679de7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841315"
---
# <a name="ksetupsetrealm"></a>ksetup: setrealm



Kerberos 領域の名前を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setrealm <DNSDomainName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DNSDomainName >|DNS ドメイン名は、完全修飾ドメイン名または単純なドメイン名の形式で指定できます。|

## <a name="remarks"></a>コメント

DNS ドメイン名パラメーターは大文字で入力する必要があります。 それ以外の場合、 **ksetup**コマンドは検証を続行するように要求します。

ドメインコントローラーでの Kerberos 領域の設定はサポートされていません。 これを行おうとすると、警告とコマンドのエラーが発生します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

このコンピューターの領域を特定のドメイン名に設定して、ドメインコントローラー以外のアクセスを CONTOSO Kerberos 領域のみに制限します。
```
ksetup /setrealm CONTOSO
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Ksetup](ksetup.md)
-   [Ksetup:removerealm](ksetup-removerealm.md)