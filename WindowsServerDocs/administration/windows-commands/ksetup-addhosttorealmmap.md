---
title: 'ksetup: addhost almmap'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e6a28c6001707fac245de7136b5fb5bd38495027
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375650"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup: addhost almmap



指定されたホストと領域の間に、サービスプリンシパル名 (SPN) マッピングを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<HostName >|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>コメント

このコマンドを使用すると、同じ DNS サフィックスを共有しているホストまたは複数のホストを領域にマップできます。

マッピングは**HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**のレジストリに記録されます。

## <a name="BKMK_Examples"></a>例

領域 CONTOSO の構成の一環として、ホストコンピューター IPops897 を領域にマップします。
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
レジストリで、マッピングが意図しているものであることを確認します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)