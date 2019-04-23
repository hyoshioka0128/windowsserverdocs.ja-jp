---
title: ksetup:delenctypeattr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fc25ef3-e271-4229-a712-72c507df55aa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c2cc96e8156cafd3846422596abe62513e275b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838133"
---
# <a name="ksetupdelenctypeattr"></a>ksetup:delenctypeattr



ドメインの暗号化の種類属性を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delenctypeattr <DomainName> 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドメイン名 >|接続を確立するドメインの名前です。 完全修飾ドメイン名または名前、corp.contoso.com または contoso などの単純なフォームを使用します。|

## <a name="remarks"></a>注釈

Kerberos チケット保証チケット (TGT) およびセッション キーの暗号化の種類を表示するには、実行、 **klist**コマンドし、出力を表示します。

ステータス メッセージが成功または失敗の完了時に表示されます。

接続して使用するドメインを設定するには、実行、 **ksetup/domain \<DomainName >** コマンド。

## <a name="BKMK_Examples"></a>例

このコンピューターに設定されている現在の暗号化の種類を決定します。
```
klist
```
Mit.contoso.com にドメインを設定します。
```
ksetup /domain mit.contoso.com
```
ドメインの暗号化の種類の属性を確認します。
```
ksetup /getenctypeattr mit.contoso.com
```
ドメイン mit.contoso.com のセットの暗号化の種類属性を削除します。
```
ksetup /delenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [klist](klist.md)
-   [ksetup:domain](ksetup-domain.md)
-   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)