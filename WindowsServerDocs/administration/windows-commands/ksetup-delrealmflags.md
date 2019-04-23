---
title: ksetup:delrealmflags
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22053041-1eb4-47f5-bed9-3d5681bcde7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9522d384c4f6996534b47e98dc8d8003bda504cd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877143"
---
# <a name="ksetupdelrealmflags"></a>ksetup:delrealmflags



指定された領域から領域のフラグを削除します。  このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM では、既定の領域として表示時に**Ksetup**を実行します。|

## <a name="remarks"></a>注釈

領域のフラグは、Windows Server オペレーティング システムに基づいていないいる Kerberos 領域の他の機能を指定します。 Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターが、Windows Server オペレーティング システムを実行しているドメインを使用する代わりに認証を管理するサーバーを Kerberos を使用し、これらのシステムに参加します。Kerberos 領域。 このエントリは、領域の機能を確立します。 次の表では、それぞれについて説明します。

|値|領域のフラグ|説明|
|-----|----------|-----------|
|0 xf です.|すべての|すべての領域フラグが設定されます。|
|0x00|なし|領域のフラグが設定されていないと、その他の機能が有効なことはありません。|
|0x01|SendAddress|IP アドレスにが、チケットの付与のチケットに含まれます。|
|0x02|TcpSupported|この領域では、伝送制御プロトコル (TCP) とユーザー データグラム プロトコル (UDP) の両方がサポートされています。|
|0x04|委任|この領域のすべてのユーザーは、委任に対して信頼されています。|
|0x08|NcSupported|この領域は、名の正規化は、DNS と領域の名前付け標準をサポートします。|
|0x80|RC4|この領域は、TLS の使用できる領域間の信頼を有効にする RC4 暗号化をサポートします。|

領域のフラグがレジストリに格納されている**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\*** RealmName *。 既定では、このエントリはレジストリに存在しません。 使用することができます、 [Ksetup:addrealmflags](ksetup-addrealmflags.md)レジストリの作成にコマンド。

どのような領域のフラグが使用可能で設定を確認できますの出力を表示して**ksetup**または**ksetup/dumpstate**します。

## <a name="BKMK_Examples"></a>例

CONTOSO の領域の使用可能な領域のフラグを一覧表示します。
```
Ksetup /listrealmflags
```
現在、セット内にある 2 つのフラグを削除します。
```
ksetup /delrealmflags CONTOSO ncsupported delegate
```
実行、 **ksetup**コマンド出力を表示し、領域のフラグが設定されていることを確認する**領域フラグ =** します。

#### <a name="additional-references"></a>その他の参照情報

-   [ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)