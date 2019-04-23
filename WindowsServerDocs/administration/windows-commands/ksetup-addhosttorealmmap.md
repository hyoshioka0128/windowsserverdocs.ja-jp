---
title: ksetup:addhosttorealmmap
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 25cf258309c94f0efde980018dd5dcf3c7df4d60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837503"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup:addhosttorealmmap



指定されたホストと領域の間のサービス プリンシパル名 (SPN) マッピングを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ホスト名 >|ホスト名は、コンピューター名とコンピューターの完全修飾ドメイン名として指定できます。|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM です。|

## <a name="remarks"></a>注釈

このコマンドでは、ホストまたはを領域に同じ DNS サフィックスを共有している複数のホストにマップできます。

マッピングがレジストリに記録された**HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**します。

## <a name="BKMK_Examples"></a>例

CONTOSO の領域の構成の一環として、ホスト コンピューター IPops897 を領域にマップします。
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
マッピングは、意図したとおり、レジストリで確認します。

#### <a name="additional-references"></a>その他の参照情報

-   [ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)