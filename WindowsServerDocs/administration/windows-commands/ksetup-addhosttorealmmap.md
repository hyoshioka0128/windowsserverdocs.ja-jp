---
title: 'ksetup: addhost almmap'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 732dccc868ca85b108ba443d912788a14dd0e107
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724774"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup: addhost almmap



指定されたホストと領域の間に、サービスプリンシパル名 (SPN) マッピングを追加します。

## <a name="syntax"></a>構文

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ホスト名>|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>Remarks

このコマンドを使用すると、同じ DNS サフィックスを共有しているホストまたは複数のホストを領域にマップできます。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**のレジストリに記録されます。

## <a name="examples"></a>例

領域 CONTOSO の構成の一環として、ホストコンピューター IPops897 を領域にマップします。
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
レジストリで、マッピングが意図しているものであることを確認します。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)