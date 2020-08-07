---
title: ksetup domain
description: Ksetup domain コマンドの参照記事。すべての Kerberos 操作のドメイン名を設定します。
ms.topic: article
ms.assetid: 2ef766e3-6071-44f2-946b-22ea5b61a508
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81135ed668da901c55e891cec4c8749687359818
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887934"
---
# <a name="ksetup-domain"></a>ksetup domain

すべての Kerberos 操作のドメイン名を設定します。

## <a name="syntax"></a>構文

```
ksetup /domain <domainname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<domainname>` | 接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (contoso.com や contoso など) を使用します。|

### <a name="examples"></a>例

サブコマンドを使用して、Microsoft などの有効なドメインへの接続を確立するには、次のように `ksetup /mapuser` 入力します。

```
ksetup /mapuser principal@realm domain-user /domain domain-name
```

接続に成功すると、新しい TGT が送信されるか、既存の TGT が更新されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup mapuser コマンド](ksetup-mapuser.md)