---
title: 'ksetup: delrealmflags'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8e2e67d7af4fdd31b79ad633c9df844483bb1ea3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375104"
---
# <a name="ksetupdelrealmflags"></a>ksetup: delrealmflags



指定された領域から領域フラグを削除します。  このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /delrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **Ksetup**の実行時に既定の領域として表示されます。|

## <a name="remarks"></a>コメント

領域フラグは、Windows Server オペレーティングシステムに基づいていない Kerberos 領域の追加機能を指定します。 Windows server 2003、Windows Server 2008、または Windows Server 2008 R2 を実行しているコンピューターは、Windows Server オペレーティングシステムを実行しているドメインを使用するのではなく、Kerberos サーバーを使用して認証を管理できます。また、これらのシステムは、Kerberos 領域。 このエントリにより、領域の機能が確立されます。 次の表では、それぞれについて説明します。

|値|領域フラグ|説明|
|-----|----------|-----------|
|0Xf です|All|すべての領域フラグが設定されます。|
|0x00|なし|領域フラグが設定されておらず、追加の機能は有効になっていません。|
|0x01|SendAddress|この IP アドレスはチケット交付チケット内に含まれます。|
|0x02|TcpSupported|この領域では、伝送制御プロトコル (TCP) とユーザーデータグラムプロトコル (UDP) の両方がサポートされています。|
|0x04|委任|この領域のすべてのユーザーが委任に対して信頼されています。|
|0x08|NcSupported|この領域では、DNS と領域の名前付け標準を可能にする、名前の正規化がサポートされています。|
|0x80|RC4|この領域では、RC4 暗号化をサポートして、複数領域にわたる信頼を有効にします。これにより、TLS を使用できるようになります。|

領域フラグは、レジストリの**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains @ no__t-1**<em>realmname</em>に格納されます。 既定では、このエントリはレジストリに存在しません。 [Ksetup: addrealmflags](ksetup-addrealmflags.md)コマンドを使用して、レジストリにデータを設定できます。

**Ksetup**または**ksetup/dumpstate**の出力を表示することで、使用可能な領域フラグと設定されている領域フラグを確認できます。

## <a name="BKMK_Examples"></a>例

領域 CONTOSO の利用可能な領域フラグを一覧表示します。
```
Ksetup /listrealmflags
```
現在セット内にある2つのフラグを削除します。
```
ksetup /delrealmflags CONTOSO ncsupported delegate
```
**Ksetup**コマンドを実行して、領域フラグが設定されていることを確認します。これを行うには、出力を表示し、 **realm flags =** を探します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)