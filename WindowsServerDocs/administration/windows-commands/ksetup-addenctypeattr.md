---
title: ksetup addenctypeattr
description: Ksetup addenctypeattr コマンドの参照記事。このコマンドにより、暗号化の種類の属性がドメインの使用可能な種類の一覧に追加されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32cc87d7-b9e1-4d14-9eb7-3b439c55aa3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e52a3fc7303bcd3db3f289ff8155bcb13b145b04
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931403"
---
# <a name="ksetup-addenctypeattr"></a>ksetup addenctypeattr

ドメインの使用可能な種類の一覧に暗号化の種類の属性を追加します。 正常に完了したか、完了しなかったときに、ステータスメッセージが表示されます。

## <a name="syntax"></a>構文

```
ksetup /addenctypeattr <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<domainname>` | 接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。 |
| 暗号化の種類 | は、次のサポートされている暗号化の種類のいずれかである必要があります。<ul><li>DES-CBC-CRC</li><li>DES-CBC-MD5</li><li>RC4-HMAC-MD5</li><li>AES128---SHA1-96</li><li>AES256---SHA1-96</li></ul> |

#### <a name="remarks"></a>注釈

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

暗号化の種類として*AES-256-* *corp.contoso.com*-96-96 を追加するには、次のように入力します。

```
ksetup /addenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```

暗号化の種類の属性を*AES-256-corp.contoso.com-96-96*に設定するには、 *corp.contoso.com*次のように入力します。

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

- [ksetup setenctypeattr コマンド](ksetup-setenctypeattr.md)

- [ksetup getenctypeattr コマンド](ksetup-getenctypeattr.md)

- [ksetup delenctypeattr コマンド](ksetup-delenctypeattr.md)
