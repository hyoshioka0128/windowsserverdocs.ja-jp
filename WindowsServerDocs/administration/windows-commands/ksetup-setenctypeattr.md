---
title: ksetup setenctypeattr
description: Ksetup setenctypeattr コマンドの参照記事。ドメインの暗号化の種類の属性を設定します。
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50d5c5be2382cc1d811066d577f8f092b676853a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887765"
---
# <a name="ksetup-setenctypeattr"></a>ksetup setenctypeattr

ドメインの暗号化の種類の属性を設定します。 正常に完了したか、完了しなかったときに、ステータスメッセージが表示されます。

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。 コマンドを実行して、に接続してを使用するようにドメインを設定でき `ksetup /domain <domainname>` ます。

## <a name="syntax"></a>構文

```
ksetup /setenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<domainname>` | 接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。 |
| 暗号化の種類 | は、次のサポートされている暗号化の種類のいずれかである必要があります。<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128---SHA1-96</li><li>AES256---SHA1-96</li></ul> |

#### <a name="remarks"></a>Remarks

- コマンド内の暗号化の種類をスペースで区切って、複数の暗号化の種類を設定または追加できます。 ただし、一度に1つのドメインに対してのみ実行できます。

### <a name="examples"></a>例

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、次のように入力します。

```
klist
```

ドメインを corp.contoso.com に設定するには、次のように入力します。

```
ksetup /domain corp.contoso.com
```

暗号化の種類の属性を AES-256-corp.contoso.com-96-96 に設定するには、次のように入力します。

```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

暗号化の種類の属性がドメインに適したものとして設定されていることを確認するには、次のように入力します。

```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [klist コマンド](klist.md)

- [ksetup コマンド](ksetup.md)

- [ksetup domain コマンド](ksetup-domain.md)

- [ksetup addenctypeattr コマンド](ksetup-addenctypeattr.md)

- [ksetup getenctypeattr コマンド](ksetup-getenctypeattr.md)

- [ksetup delenctypeattr コマンド](ksetup-delenctypeattr.md)
