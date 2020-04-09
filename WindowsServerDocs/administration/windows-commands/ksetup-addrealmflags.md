---
title: 'ksetup: addrealmflags'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 21ab18620f0ed25cfb0d50bb1ab1a5d92caa9c54
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841816"
---
# <a name="ksetupaddrealmflags"></a>ksetup: addrealmflags



指定された領域に領域フラグを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|領域名|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|

## <a name="remarks"></a>コメント

領域フラグは、Windows Server オペレーティングシステムに基づいていない Kerberos 領域の追加機能を指定します。 Windows server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターは、Windows Server オペレーティングシステムを実行しているドメインを使用するのではなく、Kerberos サーバーを使用して認証を管理できます。また、これらのシステムは Kerberos 領域に参加します。 このエントリにより、領域の機能が確立されます。 次の表では、それぞれについて説明します。

|値|領域フラグ|説明|
|-----|----------|-----------|
|0xF|[すべて]|すべての領域フラグが設定されます。|
|0x00|なし|領域フラグが設定されておらず、追加の機能は有効になっていません。|
|0x01|SendAddress|この IP アドレスは、チケット保証チケット内に含まれます。|
|0x02|TcpSupported|この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) の両方がサポートされています。|
|0x04|デリゲート|この領域のすべてのユーザーが委任に対して信頼されています。|
|0x08|NcSupported|この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。|
|0x80|RC4|この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。|

領域フラグは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\** <em>領域名</em>の下のレジストリに格納されます。 既定では、このエントリはレジストリに存在しません。 [Ksetup: addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

Ksetup または ksetup/dumpstateの出力を表示することで、使用可能な領域フラグと設定されている領域フラグを確認できます。

## <a name="examples"></a><a name=BKMK_Examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)