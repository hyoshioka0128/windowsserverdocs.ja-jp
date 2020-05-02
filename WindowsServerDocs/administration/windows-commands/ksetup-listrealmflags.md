---
title: 'ksetup: listrealmflags'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f0646be8daaad4bc3303389cfca1f3a09136fe1a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724628"
---
# <a name="ksetuplistrealmflags"></a>ksetup: listrealmflags



**Ksetup**によって報告される可能性のある領域フラグを一覧表示します。

## <a name="syntax"></a>構文

```
ksetup /listrealmflags
```

#### <a name="parameters"></a>パラメーター

なし

## <a name="remarks"></a>Remarks

領域フラグは、Windows ベース以外の Kerberos 領域の追加機能を指定します。 Windows server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターでは、windows Server オペレーティングシステムを実行しているドメインを使用する代わりに、windows ベース以外の Kerberos サーバーを使用して認証を管理できます。 これらのシステムは、Windows ドメインではなく、Kerberos 領域に参加します。 このエントリにより、領域の機能が確立されます。 次の表では、それぞれについて説明します。

|値|領域フラグ|[説明]|
|-----|----------|-----------|
|0xF|All|すべての領域フラグが設定されます。|
|0x00|なし|領域フラグが設定されておらず、追加の機能は有効になっていません。|
|0x01|SendAddress|この IP アドレスは、チケット保証チケット内に含まれます。|
|0x02|TcpSupported|この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) がサポートされています。|
|0x04|委任|この領域のすべてのユーザーが委任に対して信頼されています。|
|0x08|NcSupported|この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。|
|0x80|RC4|この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。|

領域フラグは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**<em>領域名</em>のレジストリに格納されます。 既定では、このエントリはレジストリに存在しません。 [Ksetup: addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

## <a name="examples"></a>例

このコンピューターの既知の領域フラグを一覧表示します:
```
ksetup /listrealmflags
```
コマンドラインで次のコマンドのいずれかを入力して、 **Ksetup**で認識されない使用可能な領域フラグを設定します。
```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```
```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Ksetup](ksetup.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)