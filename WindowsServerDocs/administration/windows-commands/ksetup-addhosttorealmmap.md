---
title: 'ksetup: addhost almmap'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ee8f434482b0658194daed46b62f6f7f70abae1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841845"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup: addhost almmap



指定されたホストと領域の間に、サービスプリンシパル名 (SPN) マッピングを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ホスト名の \<>|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>コメント

このコマンドを使用すると、同じ DNS サフィックスを共有しているホストまたは複数のホストを領域にマップできます。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**のレジストリに記録されます。

## <a name="examples"></a><a name=BKMK_Examples></a>例

領域 CONTOSO の構成の一環として、ホストコンピューター IPops897 を領域にマップします。
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
レジストリで、マッピングが意図しているものであることを確認します。

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)