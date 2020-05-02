---
title: 'ksetup: setrealmflags'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcb2824e-fba7-4ebe-be62-e62b4fae5b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a32ea03f4f0e76f03c7a0b505563e6bcf972b80
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724571"
---
# <a name="ksetupsetrealmflags"></a>ksetup: setrealmflags



指定された領域の領域フラグを設定します。

## <a name="syntax"></a>構文

```
ksetup /setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM。|
|領域フラグ|は、次のいずれかのフラグを示します。</br>-SendAddress</br>-TcpSupported</br>-Delegate</br>- NcSupported</br>-RC4|

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

領域フラグは**HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\**<em>realmname</em>の下のレジストリに格納されます。 既定では、このエントリはレジストリに存在しません。 [Ksetup: addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

**Ksetup**の出力を表示することによって、使用可能な領域フラグと設定されているものを確認できます。

## <a name="examples"></a>例

領域 CONTOSO の利用可能な領域フラグと設定領域フラグを一覧表示します。
```
ksetup
```
現在設定されていない2つのフラグを設定します。
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
**Ksetup**コマンドを実行して、領域フラグが設定されていることを確認します。これを行うには、出力を表示し、 **realm flags =** を探します。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)