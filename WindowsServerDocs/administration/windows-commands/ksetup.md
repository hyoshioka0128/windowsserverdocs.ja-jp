---
title: ksetup
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3c61fd81691f9db44330eddbf40d4212d1786ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841255"
---
# <a name="ksetup"></a>ksetup



Kerberos プロトコルとキー配布センター (KDC) を設定して管理するタスクを実行して、Kerberos 領域をサポートします。これは、Windows ドメインでもありません。 このコマンドを使用する方法の例については、関連する各サブトピックの「例」を参照してください。

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

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Ksetup:setrealm](ksetup-setrealm.md)|このコンピューターを Kerberos 領域のメンバーにします。|
|[Ksetup:mapuser](ksetup-mapuser.md)|Kerberos プリンシパルをアカウントにマップします。|
|[Ksetup:addkdc](ksetup-addkdc.md)|指定された領域の KDC エントリを定義します。|
|[Ksetup:delkdc](ksetup-delkdc.md)|領域の KDC エントリを削除します。|
|[Ksetup:addkpasswd](ksetup-addkpasswd.md)|領域の Kpasswd サーバーアドレスを追加します。|
|[Ksetup:delkpasswd](ksetup-delkpasswd.md)|領域の Kpasswd サーバーアドレスを削除します。|
|[Ksetup:server](ksetup-server.md)|変更を適用する Windows コンピューターの名前を指定できます。|
|[Ksetup:setcomputerpassword](ksetup-setcomputerpassword.md)|コンピューターのドメインアカウント (またはホストプリンシパル) のパスワードを設定します。|
|[Ksetup:removerealm](ksetup-removerealm.md)|指定された領域のすべての情報をレジストリから削除します。|
|[Ksetup:domain](ksetup-domain.md)|ドメインを指定できます (\<DomainName > が **/domain**を使用して設定されていない場合)。|
|[Ksetup:changepassword](ksetup-changepassword.md)|Kpasswd を使用して、ログオンしているユーザーのパスワードを変更できます。|
|[Ksetup:listrealmflags](ksetup-listrealmflags.md)|**Ksetup**が検出できる領域フラグを一覧表示します。|
|[Ksetup:setrealmflags](ksetup-setrealmflags.md)|特定の領域の領域フラグを設定します。|
|[Ksetup:addrealmflags](ksetup-addrealmflags.md)|領域に領域フラグを追加します。|
|[Ksetup:delrealmflags](ksetup-delrealmflags.md)|領域から領域フラグを削除します。|
|[Ksetup:dumpstate](ksetup-dumpstate.md)|指定されたコンピューターの Kerberos 構成を分析します。 レジストリに対するレルムマッピングにホストを追加します。|
|[Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)|ホストを Kerberos 領域にマップするレジストリ値を追加します。|
|[Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)|ホストコンピューターを Kerberos 領域にマップしたレジストリ値を削除します。|
|[Ksetup:setenctypeattr](ksetup-setenctypeattr.md)|ドメインの1つ以上の暗号化の種類の信頼属性を設定します。|
|[Ksetup:getenctypeattr](ksetup-getenctypeattr.md)|ドメインの暗号化の種類の信頼属性を取得します。|
|[Ksetup:addenctypeattr](ksetup-addenctypeattr.md)|ドメインの暗号化の種類の信頼属性に暗号化の種類を追加します。|
|[Ksetup:delenctypeattr](ksetup-delenctypeattr.md)|ドメインの暗号化の種類の信頼属性を削除します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

**Ksetup**は、Kerberos 領域を検索するためにコンピューターの設定を変更するために使用されます。 Microsoft 以外の Kerberos ベースの実装では、通常、この情報は Krb5.conf ファイルに保存されます。 Windows Server オペレーティングシステムでは、レジストリに保持されます。 このツールを使用すると、これらの設定を変更できます。 これらの設定は、ワークステーションが Kerberos 領域を検索するために使用され、ドメインコントローラーによって、複数の領域にわたる信頼関係の Kerberos 領域を特定します。

**Ksetup**コンピューターが windows server 2003、windows server 2008、または windows Server 2008 R2 を実行していて、windows ドメインのメンバーではない場合、Kerberos セキュリティサポートプロバイダー (SSP) が kerberos 領域の KDC を見つけるために使用するレジストリキーを初期化します。 構成が完了すると、Windows オペレーティングシステムを実行しているクライアントコンピューターのユーザーが、Kerberos 領域内のアカウントにログオンできるようになります。

Kerberos version 5 プロトコルは、Windows XP Professional、Windows Vista、および Windows 7 を実行しているコンピューターでのネットワーク認証の既定値です。 Kerberos SSP は、レジストリ内でユーザーの領域のドメイン名を検索し、DNS サーバーを照会することによって、名前を IP アドレスに解決します。 Kerberos プロトコルでは、DNS を使用して、領域名のみを使用して Kdc を検索できますが、これを行うように特別に構成する必要があります。

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)