---
title: 'ksetup: delhost almmap'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85e9f6b4a9f1c9050ed843f3837a2bd87aaf6eae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841735"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup: delhost almmap



指定されたホストと領域間のサービスプリンシパル名 (SPN) マッピングを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ホスト名の \<>|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>コメント

ホストから領域への (または複数のホストから領域への) マッピングが存在する場合、このコマンドによってそのマッピングが削除されます。

マッピングは**HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**のレジストリに記録されます。 このコマンドを使用した後、レジストリでマッピングを確認する必要があります。

## <a name="examples"></a><a name=BKMK_Examples></a>例

領域 CONTOSO の構成を変更すると、ホストコンピューター IPops897 の領域へのマッピングが削除されます。
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
このコマンドを実行した後、マッピングが意図したとおりであることをレジストリで確認できます。

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)