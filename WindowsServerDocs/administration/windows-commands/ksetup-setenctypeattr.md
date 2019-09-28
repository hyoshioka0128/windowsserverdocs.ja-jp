---
title: 'ksetup: setenctypeattr'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88fb913e-6b57-48d9-8c16-a035ab2977ac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bcc268ecb591e3008d7274f6c9f6d6017c86f99d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374935"
---
# <a name="ksetupsetenctypeattr"></a>ksetup: setenctypeattr



ドメインの暗号化の種類の属性を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<DomainName >|接続を確立するドメインの名前。 完全修飾ドメイン名、または名前の単純な形式 (corp.contoso.com や contoso など) を使用します。|
|［暗号化の種類］|は、次のサポートされている暗号化の種類のいずれかである必要があります。</br>-DES-CBC-CRC</br>-DES-CBC-MD5</br>-RC4-HMAC-MD5</br>-AES128-96-96</br>-AES256-96-96|

## <a name="remarks"></a>コメント

Kerberos チケット保証チケット (TGT) とセッションキーの暗号化の種類を表示するには、 **klist**コマンドを実行し、出力を表示します。

コマンド内の暗号化の種類をスペースで区切って、複数の暗号化の種類を設定または追加できます。 ただし、一度に1つのドメインに対してのみ実行できます。

コマンドが成功するか失敗すると、ステータスメッセージが表示されます。

接続先として使用するドメインを設定するには、 **ksetup/domain \< domainname >** コマンドを実行します。

## <a name="BKMK_Examples"></a>例

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

#### <a name="additional-references"></a>その他の参照情報

-   [Klist](klist.md)
-   [Ksetup:domain](ksetup-domain.md)
-   [Ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [Ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [Ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)