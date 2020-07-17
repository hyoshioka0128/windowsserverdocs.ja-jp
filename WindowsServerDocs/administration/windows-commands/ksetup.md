---
title: ksetup
description: Kerberos プロトコルとキー配布センター (KDC) を設定および管理して Kerberos 領域をサポートするためのタスクを実行する、ksetup コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e046f8a-811b-48dc-9a69-18d8e097f353
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a0398d53516f81de68a7de5854ed2c996a78d1e5
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922632"
---
# <a name="ksetup"></a>ksetup

Kerberos プロトコルの設定と管理、および Kerberos 領域をサポートするためのキー配布センター (KDC) に関連するタスクを実行します。 具体的には、このコマンドは次の目的で使用されます。

- Kerberos 領域を検索するためのコンピューター設定を変更します。 Microsoft 以外の Kerberos ベースの実装では、通常、この情報は Krb5.conf ファイルに保存されます。 Windows Server オペレーティングシステムでは、レジストリに保持されます。 このツールを使用すると、これらの設定を変更できます。 これらの設定は、ワークステーションが Kerberos 領域を検索するために使用され、ドメインコントローラーによって、複数の領域にわたる信頼関係の Kerberos 領域を特定します。

- Kerberos セキュリティサポートプロバイダー (SSP) が Kerberos 領域の KDC を検索するために使用するレジストリキーを初期化します (コンピューターが Windows ドメインのメンバーでない場合)。 構成が完了すると、Windows オペレーティングシステムを実行しているクライアントコンピューターのユーザーが、Kerberos 領域内のアカウントにログオンできるようになります。

- レジストリでユーザーの領域のドメイン名を検索し、DNS サーバーを照会することによって、名前を IP アドレスに解決します。 Kerberos プロトコルでは、DNS を使用して、領域名のみを使用して Kdc を検索できますが、これを行うように特別に構成する必要があります。

## <a name="syntax"></a>構文

```
ksetup
[/setrealm <DNSdomainname>]
[/mapuser <principal> <account>]
[/addkdc <realmname> <KDCname>]
[/delkdc <realmname> <KDCname>]
[/addkpasswd <realmname> <KDCPasswordName>]
[/delkpasswd <realmname> <KDCPasswordName>]
[/server <servername>]
[/setcomputerpassword <password>]
[/removerealm <realmname>]
[/domain <domainname>]
[/changepassword <oldpassword> <newpassword>]
[/listrealmflags]
[/setrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/delrealmflags [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]]
[/dumpstate]
[/addhosttorealmmap] <hostname> <realmname>]
[/delhosttorealmmap] <hostname> <realmname>]
[/setenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/getenctypeattr] <domainname>
[/addenctypeattr] <domainname> {DES-CBC-CRC | DES-CBC-MD5 | RC4-HMAC-MD5 | AES128-CTS-HMAC-SHA1-96 | AES256-CTS-HMAC-SHA1-96}
[/delenctypeattr] <domainname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [ksetup setrealm](ksetup-setrealm.md) | このコンピューターを Kerberos 領域のメンバーにします。 |
| [ksetup addkdc](ksetup-addkdc.md) | 指定された領域の KDC エントリを定義します。 |
| [ksetup delkdc](ksetup-delkdc.md) | 領域の KDC エントリを削除します。 |
| [ksetup addkpasswd](ksetup-addkpasswd.md) | 領域の kpasswd サーバーアドレスを追加します。 |
| [ksetup delkpasswd](ksetup-delkpasswd.md) | 領域の kpasswd サーバーアドレスを削除します。 |
| [ksetup server](ksetup-server.md) | 変更を適用する Windows コンピューターの名前を指定できます。 |
| [ksetup setcomputerpassword](ksetup-setcomputerpassword.md) | コンピューターのドメインアカウント (またはホストプリンシパル) のパスワードを設定します。 |
| [ksetup removerealm](ksetup-removerealm.md) | 指定された領域のすべての情報をレジストリから削除します。 |
| [ksetup domain](ksetup-domain.md) | ドメインを指定できます (が `<domainname>` **/domain**パラメーターによってまだ設定されていない場合)。 |
| [ksetup changepassword](ksetup-changepassword.md) | Kpasswd を使用して、ログオンしているユーザーのパスワードを変更できます。 |
| [ksetup listrealmflags](ksetup-listrealmflags.md) | **Ksetup**が検出できる領域フラグを一覧表示します。 |
| [ksetup setrealmflags](ksetup-setrealmflags.md) | 特定の領域の領域フラグを設定します。 |
| [ksetup addrealmflags](ksetup-addrealmflags.md) | 領域に領域フラグを追加します。 |
| [ksetup delrealmflags](ksetup-delrealmflags.md) | 領域から領域フラグを削除します。 |
| [ksetup dumpstate](ksetup-dumpstate.md) | 指定されたコンピューターの Kerberos 構成を分析します。 レジストリに対するレルムマッピングにホストを追加します。 |
| [ksetup addhosttorealmmap](ksetup-addhosttorealmmap.md) | ホストを Kerberos 領域にマップするレジストリ値を追加します。 |
| [ksetup delhosttorealmmap](ksetup-delhosttorealmmap.md) | ホストコンピューターを Kerberos 領域にマップしたレジストリ値を削除します。 |
| [ksetup setenctypeattr](ksetup-setenctypeattr.md) | ドメインの1つ以上の暗号化の種類の信頼属性を設定します。 |
| [ksetup getenctypeattr](ksetup-getenctypeattr.md) | ドメインの暗号化の種類の信頼属性を取得します。 |
| [ksetup addenctypeattr](ksetup-addenctypeattr.md) | ドメインの暗号化の種類の信頼属性に暗号化の種類を追加します。 |
| [ksetup delenctypeattr](ksetup-delenctypeattr.md) | ドメインの暗号化の種類の信頼属性を削除します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)