---
title: ksetup
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0194cf81d069d7a5c1223f0a514d593e4870d397
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868843"
---
# <a name="ksetup"></a>ksetup



設定して、Kerberos プロトコルと Windows ドメインではない Kerberos レルムをサポートするためにキー配布センター (KDC) の管理に関連するタスクを実行します。 このコマンドの使用方法の例については、関連するサブトピックの各例」セクションを参照してください。

## <a name="syntax"></a>構文

```
ksetup 
[/setrealm <DNSDomainName>] 
[/mapuser <Principal> <Account>] 
[/addkdc <RealmName> <KDCName>] 
[/delkdc <RealmName> <KDCName>]
[/addkpasswd <RealmName> <KDCPasswordName>] 
[/delkpasswd <RealmName> <KDCPasswordName>]
[/server <ServerName>] 
[/setcomputerpassword <Password>]
[/removerealm <RealmName>]  
[/domain <DomainName>] 
[/changepassword <OldPassword> <NewPassword>] 
[/listrealmflags] 
[/setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]] 
[/dumpstate]
[/addhosttorealmmap] <HostName> <RealmName>]  
[/delhosttorealmmap] <HostName> <RealmName>]  
[/setenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <DomainName>
[/addenctypeattr] <DomainName> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <DomainName>

```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[ksetup:setrealm](ksetup-setrealm.md)|このコンピューターを Kerberos 領域のメンバーになります。|
|[ksetup:mapuser](ksetup-mapuser.md)|Kerberos プリンシパルをアカウントにマップします。|
|[ksetup:addkdc](ksetup-addkdc.md)|特定の領域の KDC エントリを定義します。|
|[ksetup:delkdc](ksetup-delkdc.md)|領域の KDC エントリを削除します。|
|[ksetup:addkpasswd](ksetup-addkpasswd.md)|レルムの Kpasswd サーバー アドレスを追加します。|
|[ksetup:delkpasswd](ksetup-delkpasswd.md)|レルムの Kpasswd サーバー アドレスを削除します。|
|[ksetup:server](ksetup-server.md)|変更を適用する Windows コンピューターの名前を指定することができます。|
|[ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)|コンピューターのドメイン アカウント (またはホスト プリンシパル) のパスワードを設定します。|
|[ksetup:removerealm](ksetup-removerealm.md)|指定された領域のすべての情報をレジストリから削除します。|
|[ksetup:domain](ksetup-domain.md)|ドメインを指定することができます (場合\<DomainName > を使用して設定されていない **/domain**)。|
|[ksetup:changepassword](ksetup-changepassword.md)|ログオンしたユーザーのパスワードを変更する、Kpasswd を使用することができます。|
|[ksetup:listrealmflags](ksetup-listrealmflags.md)|使用可能なを一覧表示フラグを設定する領域**ksetup**を検出できます。|
|[ksetup:setrealmflags](ksetup-setrealmflags.md)|特定の領域の領域のフラグを設定します。|
|[ksetup:addrealmflags](ksetup-addrealmflags.md)|領域に追加の領域のフラグを追加します。|
|[ksetup:delrealmflags](ksetup-delrealmflags.md)|領域から領域のフラグを削除します。|
|[ksetup:dumpstate](ksetup-dumpstate.md)|指定したコンピューターに Kerberos の構成を分析します。 レジストリには、ホスト領域へのマッピングからを追加します。|
|[ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)|Kerberos 領域にホストをマップするレジストリ値を追加します。|
|[ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)|ホスト コンピューターを Kerberos 領域にマップされているレジストリ値を削除します。|
|[ksetup:setenctypeattr](ksetup-setenctypeattr.md)|ドメインの信頼の属性を 1 つまたは複数の暗号化の種類を設定します。|
|[ksetup:getenctypeattr](ksetup-getenctypeattr.md)|ドメインの暗号化の種類の信頼の属性を取得します。|
|[ksetup:addenctypeattr](ksetup-addenctypeattr.md)|ドメインの暗号化の種類の信頼属性には、暗号化の種類を追加します。|
|[ksetup:delenctypeattr](ksetup-delenctypeattr.md)|ドメインの暗号化の種類の信頼属性を削除します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>注釈

**Ksetup** Kerberos 領域を検索するためにコンピューターの設定を変更するために使用します。 Microsoft Kerberos ベースの実装でこの情報は通常 Krb5.conf ファイルで保持されます。 Windows Server オペレーティング システムで、レジストリ内に保持されます。 これらの設定を変更するのには、このツールを使用することができます。 これらの設定は、Kerberos 領域の領域間の信頼関係を検索するドメイン コント ローラーと Kerberos 領域を検索するワークステーションによって使用されます。

**Ksetup** Kerberos セキュリティ サポート プロバイダー (SSP) を使用して、コンピューターが Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 が実行されていると、Windows のメンバーでない場合、KDC Kerberos 領域を検索するレジストリ キーを初期化しますドメイン。 構成の後、オペレーティング システムにログオンに Windows を実行しているクライアント コンピューターのユーザー アカウントを Kerberos 領域にします。

Kerberos version 5 プロトコルは、Windows XP Professional、Windows Vista、および Windows 7 を実行するコンピューターでネットワーク認証の既定値です。 Kerberos SSP では、ユーザーの領域のドメイン名のレジストリを検索し、名前を DNS サーバーのクエリを実行して IP アドレスに解決します。 Kerberos プロトコルは、領域名のみを使用して Kdc を検索する DNS を使用できますが、そのためには特別に構成する必要があります。

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)