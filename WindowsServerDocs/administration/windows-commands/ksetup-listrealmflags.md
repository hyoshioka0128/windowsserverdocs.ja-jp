---
title: ksetup:listrealmflags
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7db6caf4e63ea59fa40892679d3de0cfaca661e9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438018"
---
# <a name="ksetuplistrealmflags"></a>ksetup:listrealmflags



によって報告できる使用可能な領域のフラグを一覧表示**ksetup**します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /listrealmflags
```

### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>注釈

領域のフラグは、非 Windows ベースの Kerberos 領域の他の機能を指定します。 Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターでは、非 Windows ベースの Kerberos サーバーを使用して、Windows Server オペレーティング システムを実行しているドメインを使用する代わりに、認証の管理します。 これらのシステムは、Windows ドメインではなく Kerberos 領域に参加します。 このエントリは、領域の機能を確立します。 次の表では、それぞれについて説明します。

|Value|領域のフラグ|説明|
|-----|----------|-----------|
|0 xf です.|すべての|すべての領域フラグが設定されます。|
|0x00|なし|領域のフラグが設定されていないと、その他の機能が有効なことはありません。|
|0x01|SendAddress|IP アドレスは、チケット保証チケット内に含まれるになります。|
|0x02|TcpSupported|伝送制御プロトコル (TCP) とユーザー データグラム プロトコル (UDP) は、この領域でサポートされます。|
|0x04|委任|この領域のすべてのユーザーは、委任に対して信頼されています。|
|0x08|NcSupported|この領域は、名の正規化は、DNS と領域の名前付け標準をサポートします。|
|0x80|RC4|この領域は、TLS の使用できる領域間の信頼を有効にする RC4 暗号化をサポートします。|

領域のフラグがレジストリに格納されている**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\\** <em>領域名</em>します。 既定では、このエントリはレジストリに存在しません。 使用することができます、 [Ksetup:addrealmflags](ksetup-addrealmflags.md)レジストリの作成にコマンド。

## <a name="BKMK_Examples"></a>例

このコンピューターの既知領域のフラグを一覧表示します。
```
ksetup /listrealmflags
```
使用可能な領域のフラグを設定**Ksetup**コマンドラインで次のコマンドのいずれかを入力するかわかりません。
```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```
```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Ksetup](ksetup.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)