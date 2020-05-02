---
title: 'ksetup: ドメイン'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f127eaf33e9ef6d597851c31a4167ceaa3516abb
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724684"
---
# <a name="ksetupdomain"></a>ksetup: ドメイン



すべての Kerberos 操作のドメイン名を設定します。

## <a name="syntax"></a>構文

```
ksetup /domain <DomainName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<DomainName>|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (contoso.com や contoso など) を使用します。|

## <a name="remarks"></a>Remarks

なし。

## <a name="examples"></a>例

次のように、/mapuser サブコマンドを使用して、Microsoft などの有効なドメインへの接続を確立します。
```
ksetup /mapuser principal@realm domain-user /domain domain-name
```
接続に成功すると、新しい TGT が送信されるか、既存の TGT が更新されます。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)