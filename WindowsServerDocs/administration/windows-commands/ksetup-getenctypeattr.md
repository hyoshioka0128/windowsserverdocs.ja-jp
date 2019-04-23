---
title: ksetup:getenctypeattr
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6c7ec002-355e-474d-bc27-27215049f1a8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 302f94616f98eb350332b08ad37a58305a0a0be1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841993"
---
# <a name="ksetupgetenctypeattr"></a>ksetup:getenctypeattr



ドメインの暗号化の種類属性を取得します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /getenctypeattr <DomainName> 
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドメイン名 >|接続を確立するドメインの名前です。 完全修飾ドメイン名または名前、corp.contoso.com または contoso などの単純なフォームを使用します。|

## <a name="remarks"></a>注釈

Kerberos チケット保証チケット (TGT) およびセッション キーの暗号化の種類を表示するには、実行、 **klist**コマンドし、出力を表示します。

コマンドの成功または失敗、成功または失敗の完了時に、ステータス メッセージが表示されます。

接続して使用するドメインを設定するには、実行、 **ksetup/domain \<DomainName >** コマンド。

## <a name="BKMK_Examples"></a>例

ドメインの暗号化の種類属性を確認します。
```
ksetup /getenctypeattr mit.contoso.com
```

#### <a name="additional-references"></a>その他の参照情報

-   [klist](klist.md)
-   [ksetup:domain](ksetup-domain.md)
-   [ksetup:addenctypeattr](ksetup-addenctypeattr.md)
-   [ksetup:setenctypeattr](ksetup-setenctypeattr.md)
-   [ksetup:delenctypeattr](ksetup-delenctypeattr.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)