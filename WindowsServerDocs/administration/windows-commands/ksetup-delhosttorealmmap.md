---
title: 'ksetup: delhost almmap'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 70b54aaebc0b7b46c34c6f52e45f6583afd6c477
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375149"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup: delhost almmap



指定されたホストと領域間のサービスプリンシパル名 (SPN) マッピングを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<HostName >|ホスト名はコンピューター名であり、コンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>コメント

ホストから領域への (または複数のホストから領域への) マッピングが存在する場合、このコマンドによってそのマッピングが削除されます。

マッピングは**HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**のレジストリに記録されます。 このコマンドを使用した後、レジストリでマッピングを確認する必要があります。

## <a name="BKMK_Examples"></a>例

領域 CONTOSO の構成を変更すると、ホストコンピューター IPops897 の領域へのマッピングが削除されます。
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
このコマンドを実行した後、マッピングが意図したとおりであることをレジストリで確認できます。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)