---
title: 'ksetup: delhost almmap'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b6b14785f254a63f0e16fcd16f1cd464a2d69c8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724692"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup: delhost almmap



指定されたホストと領域間のサービスプリンシパル名 (SPN) マッピングを削除します。

## <a name="syntax"></a>構文

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ホスト名>|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>Remarks

ホストから領域への (または複数のホストから領域への) マッピングが存在する場合、このコマンドによってそのマッピングが削除されます。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**のレジストリに記録されます。 このコマンドを使用した後、レジストリでマッピングを確認する必要があります。

## <a name="examples"></a>例

領域 CONTOSO の構成を変更すると、ホストコンピューター IPops897 の領域へのマッピングが削除されます。
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
このコマンドを実行した後、マッピングが意図したとおりであることをレジストリで確認できます。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)