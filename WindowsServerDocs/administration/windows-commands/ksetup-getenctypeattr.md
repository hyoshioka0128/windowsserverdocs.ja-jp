---
title: ksetup getenctypeattr
description: Ksetup getenctypeattr コマンドの参照記事。ドメインの暗号化の種類の属性を取得します。
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27dfd66e5108aa4704b999671397cb90049d1a15
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887918"
---
# <a name="ksetup-getenctypeattr"></a>ksetup getenctypeattr

ドメインの暗号化の種類の属性を取得します。 正常に完了したか、完了しなかったときに、ステータスメッセージが表示されます。

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。 コマンドを実行して、に接続してを使用するようにドメインを設定でき `ksetup /domain <domainname>` ます。

## <a name="syntax"></a>構文

```
ksetup /getenctypeattr <domainname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<domainname>` | 接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。 |

### <a name="examples"></a>例

ドメインの暗号化の種類の属性を確認するには、次のように入力します。

```
ksetup /getenctypeattr mit.contoso.com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [klist コマンド](klist.md)

- [ksetup コマンド](ksetup.md)

- [ksetup domain コマンド](ksetup-domain.md)

- [ksetup addenctypeattr コマンド](ksetup-addenctypeattr.md)

- [ksetup setenctypeattr コマンド](ksetup-setenctypeattr.md)

- [ksetup delenctypeattr コマンド](ksetup-delenctypeattr.md)
