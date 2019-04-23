---
title: ksetup:setenctypeattr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a91539ec7a9e0ce4c75d5165da1b88ae36d3fe6c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879203"
---
# <a name="ksetupsetenctypeattr"></a>ksetup:setenctypeattr



ドメインの暗号化の種類属性を設定します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /setenctypeattr <Domain name> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドメイン名 >|接続を確立するドメインの名前です。 完全修飾ドメイン名または名前、corp.contoso.com または contoso などの単純なフォームを使用します。|
|［暗号化の種類］|次のサポートされている暗号化の種類のいずれかを指定する必要があります。</br>-DES-CBC-CRC</br>-   DES-CBC-MD5</br>-   RC4-HMAC-MD5</br>-AES128、CTS の HMAC-SHA1-96</br>-AES256-CTS の HMAC-SHA1-96|

## <a name="remarks"></a>注釈

Kerberos チケット保証チケット (TGT) およびセッション キーの暗号化の種類を表示するには、実行、 **klist**コマンドし、出力を表示します。

設定またはスペースでのコマンドは、暗号化の種類を分離することで複数の暗号化の種類を追加できます。 ただし、のみこれを行う 1 つのドメインを一度にします。

コマンドの成功または失敗、ステータス メッセージが表示されます。

接続して使用するドメインを設定するには、実行、 **ksetup/domain \<DomainName >** コマンド。

## <a name="BKMK_Examples"></a>例

このコンピューターに設定されている現在の暗号化の種類を決定します。
```
klist
```
Corp.contoso.com のドメインを設定します。
```
ksetup /domain corp.contoso.com
```
Corp.contoso.com というドメインの AES-256-CTS-HMAC-SHA1-96 に暗号化型の属性を設定します。
```
ksetup /setenctypeattr corp.contoso.com AES-256-CTS-HMAC-SHA1-96
```
ドメインの意図したとおりに暗号化型の属性が設定されたことを確認します。
```
ksetup /getenctypeattr corp.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [klist](klist.md)
-   [ksetup:domain](ksetup-domain.md)
-   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [ksetup:getenctypeattr](ksetup-getenctypeattr.md)
-   [ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)