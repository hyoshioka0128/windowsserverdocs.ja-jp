---
title: 'ksetup: setenctypeattr'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cb7380a5fc65734902c6eed0b4b941eda6f6f5a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724567"
---
# <a name="ksetupsetenctypeattr"></a>ksetup: setenctypeattr



ドメインの暗号化の種類の属性を設定します。

## <a name="syntax"></a>構文

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<DomainName>|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。|
|暗号化の種類|は、次のサポートされている暗号化の種類のいずれかである必要があります。</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128-96-96</br>-AES256-96-96|

## <a name="remarks"></a>Remarks

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。

コマンド内の暗号化の種類をスペースで区切って、複数の暗号化の種類を設定または追加できます。 ただし、一度に1つのドメインに対してのみ実行できます。

コマンドが成功するか失敗すると、ステータスメッセージが表示されます。

接続先として使用するドメインを設定するには、 **ksetup/Domain \<DomainName>** コマンドを実行します。

## <a name="examples"></a>例

このコンピューターに設定されている現在の暗号化の種類を確認します。
```
klist
```
ドメインを corp.contoso.com に設定します。
```
ksetup /domain corp.contoso.com
```
次のように、暗号化の種類の属性を、ドメイン corp.contoso.com の AES-256 に設定します。
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
暗号化の種類の属性がドメイン用に設定されていることを確認します。
```
ksetup /getenctypeattr corp.contoso.com
```

## <a name="additional-references"></a>その他のリファレンス

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)