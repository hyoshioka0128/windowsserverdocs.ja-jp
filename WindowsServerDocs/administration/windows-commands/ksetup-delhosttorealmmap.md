---
title: ksetup:delhosttorealmmap
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: cf01edc4932fd5ec1cf98043de04286b3a100a34
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882343"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup:delhosttorealmmap



指定されたホストと領域の間のサービス プリンシパル名 (SPN) マッピングを削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ホスト名 >|ホスト名は、コンピューター名とコンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM です。|

## <a name="remarks"></a>注釈

ホスト マッピング領域 (または領域を複数のホスト) に存在する場合、このコマンドは、そのマッピングを削除します。

マッピングがレジストリに記録された**HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**します。 このコマンドを使用した後、レジストリのマッピングを確認する必要があります。

## <a name="BKMK_Examples"></a>例

CONTOSO 領域の構成を変更するには、領域には、ホスト コンピューターの IPops897 のマッピングを削除します。
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
このコマンドを実行した後で確認できます、レジストリのマッピングが意図したとおりであります。

#### <a name="additional-references"></a>その他の参照情報

-   [ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)