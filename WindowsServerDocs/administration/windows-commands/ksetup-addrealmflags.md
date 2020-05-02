---
title: 'ksetup: addrealmflags'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 26f06e23f40216fe31403280d8946c56825967d6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724716"
---
# <a name="ksetupaddrealmflags"></a>ksetup: addrealmflags



指定された領域に領域フラグを追加します。

## <a name="syntax"></a>構文

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|領域名|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>Remarks

領域フラグは、Windows Server オペレーティングシステムに基づいていない Kerberos 領域の追加機能を指定します。 Windows server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターは、Windows Server オペレーティングシステムを実行しているドメインを使用するのではなく、Kerberos サーバーを使用して認証を管理できます。また、これらのシステムは Kerberos 領域に参加します。 このエントリにより、領域の機能が確立されます。 次の表では、それぞれについて説明します。

|値|領域フラグ|[説明]|
|-----|----------|-----------|
|0xF|All|すべての領域フラグが設定されます。|
|0x00|なし|領域フラグが設定されておらず、追加の機能は有効になっていません。|
|0x01|SendAddress|この IP アドレスは、チケット保証チケット内に含まれます。|
|0x02|TcpSupported|この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) の両方がサポートされています。|
|0x04|委任|この領域のすべてのユーザーが委任に対して信頼されています。|
|0x08|NcSupported|この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。|
|0x80|RC4|この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。|

領域フラグは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**の下のレジストリに格納され<em>ます。</em> 既定では、このエントリはレジストリに存在しません。 [Ksetup: addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

Ksetup または ksetup/dumpstateの出力を表示することで、使用可能な領域フラグと設定されている領域フラグを確認できます。

## <a name="examples"></a>例

領域 CONTOSO の利用可能な領域フラグを一覧表示します。
```
Ksetup /listrealmflags
```
CONTOSO 領域に2つのフラグを設定します。
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
現在 set に含まれていないフラグをもう1つ追加します。
```
ksetup /addrealmflags CONTOSO SendAddress
```
**Ksetup**コマンドを実行して、領域フラグが設定されていることを確認します。これを行うには、出力を表示し、 **realm flags =** を探します。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)