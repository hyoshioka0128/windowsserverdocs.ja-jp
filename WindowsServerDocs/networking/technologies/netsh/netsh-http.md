---
title: ハイパー テキスト用の Netsh コマンドは転送プロトコル (HTTP)
description: クエリを実行して、HTTP.sys の設定とパラメーターを構成するには、netsh http を使用します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daecc6a385d7aa2c02d1bea02eb0a585a9b33185
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881793"
---
# <a name="netsh-http-commands"></a>Netsh http コマンド


使用**netsh http**クエリを実行して、HTTP.sys の設定とパラメーターを構成します。  

>[!TIP]
>Windows Server 2016 または Windows 10 を実行するコンピューターを Windows PowerShell を使用している場合は、入力**netsh** Enter キーを押します。 Netsh プロンプトから次のように入力します。 **http** netsh http のプロンプトを取得するには Enter キーを押します。
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

Http の使用の netsh コマンドは次のとおりです。

- [iplisten を追加します。](#add-iplisten)
- [sslcert を追加します。](#add-sslcert)
- [タイムアウトを追加します。](#add-timeout)
- [urlacl を追加します。](#add-urlacl)
- [キャッシュを削除します。](#delete-cache)
- [iplisten を削除します。](#delete-iplisten)
- [sslcert を削除します。](#delete-sslcert)
- [タイムアウトを削除します。](#delete-timeout)
- [urlacl を削除します。](#delete-urlacl)
- [logbuffer をフラッシュします。](#flush-logbuffer)
- [show cachestate](#show-cachestate)
- [show iplisten](#show-iplisten)
- [servicestate を表示します。](#show-servicestate)
- [show sslcert](#show-sslcert)
- [タイムアウトを表示します。](#show-timeout)
- [urlacl を表示します。](#show-urlacl)

## <a name="add-iplisten"></a>iplisten を追加します。

ポート番号を除く、IP リッスン一覧に新しい IP アドレスを追加します。

**構文**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**Parameters**
| | | |
|---|---|---|
| **ip アドレス** | Ip アドレスに追加する IPv4 または IPv6 アドレスは、リストをリッスンします。 IP リッスン一覧は、HTTP サービスがバインド アドレスの一覧の範囲に使用されます。 任意の IPv4 アドレスを意味する「0.0.0.0」と"::"任意の IPv6 アドレスのことを意味します。 | 必須 |
---

**使用例**

4 つの例を次に、**追加 iplisten**コマンド。

-   追加 iplisten ipaddress fe80::1 を =
-   追加 iplisten ipaddress 1.1.1.1 を =
-   追加 iplisten ip アドレス 0.0.0.0 を =
-   add iplisten ipaddress=::

---

## <a name="add-sslcert"></a>sslcert を追加します。

新しい SSL サーバー証明書バインドと、対応する IP アドレスとポートのクライアント証明書ポリシーを追加します。

**構文**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**Parameters**

| | | |
|---|---|---|
| **ipport**                                   | IP アドレスとバインディングのポートを指定します。 コロン (:)IP アドレスとポート番号の間の区切り記号として使用されます。                                              | 必須 |
| **certhash**                                 | 証明書の SHA ハッシュを指定します。 このハッシュは、20 バイト長で 16 進数の文字列として指定されます。                                                                          | 必須 |
| **appid**                                    | 所有しているアプリケーションを識別する GUID を指定します。                                                                                                                                   | 必須 |
| **certstorename**                            | 証明書のストアの名前を指定します。 既定値は MY です。 証明書は、ローカル コンピューターのコンテキストを格納する必要があります。                                                                   | 省略可能 |
| **verifyclientcertrevocation**               | クライアント証明書の失効の検証のオン/オフに指定します。                                                                                                            | 省略可能 |
| **verifyrevocationwithcachedclientcertonly** | 失効確認のキャッシュされたクライアント証明書のみの使用法が有効になっているかどうかを指定します。                                                                            | 省略可能 |
| **usagecheck**                               | 使用状況のチェックを有効または無効になっているかどうかを指定します。 既定で有効になっています。                                                                                                            | 省略可能 |
| **revocationfreshnesstime**                  | 更新された証明書失効リスト (CRL) をチェックする秒単位の時間間隔を指定します。 この値が 0 の場合は、1 つ前の有効期限が切れる場合にのみ、新しい CRL は更新されます。 | 省略可能 |
| **urlretrievaltimeout**                      | 証明書失効リストをリモート URL の取得を試みると、タイムアウト間隔 (ミリ秒単位) を指定します。                                                       | 省略可能 |
| **sslctlidentifier**                         | 信頼できる証明書の発行者の一覧を指定します。 この一覧は、コンピューターによって信頼されている証明書発行者のサブセットであることができます。                                | 省略可能 |
| **sslctlstorename**                          | LOCAL_MACHINE SslCtlIdentifier が格納されている、証明書ストア名を指定します。                                                                                               | 省略可能 |
| **dsmapperusage**                            | DS マッパーを有効または無効になっているかどうかを指定します。 既定では、無効になっています。                                                                                                                | 省略可能 |
| **clientcertnegotiation**                    | 証明書のネゴシエーションを有効または無効になっているかどうかを指定します。 既定では、無効になっています。                                                                                            | 省略可能 |
---

**使用例**

例を次に、**追加 sslcert**コマンド。

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>タイムアウトを追加します。

サービスには、グローバル タイムアウトを追加します。

**構文** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**Parameters**
| | |
|---|---|
| **timeouttype** | 設定のタイムアウト値の型。                                                                        |
| **value**       | タイムアウト (秒) の値。 値は、16 進数表記では場合、は、0 のプレフィックスを追加し、x。 |
---

**使用例**

2 つの例を次に、**タイムアウトを追加**コマンド。

-   add timeout timeouttype=idleconnectiontimeout value=120
-   add timeout timeouttype=headerwaittimeout value=0x40

---

## <a name="add-urlacl"></a>urlacl を追加します。

Uniform Resource Locator (URL) の予約のエントリを追加します。 このコマンドは、管理者以外のユーザーとアカウントの URL を予約します。 DACL をリッスンし、デリゲートのパラメーターを使用して NT アカウント名を使用して、または SDDL 文字列を使用して指定できます。

**構文**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**Parameters**
| | | |
|---|---|---|
| **url**       | 完全修飾 Uniform Resource Locator (URL) を指定します。                                                                                    | 必須 |
| **user**      | ユーザーまたはユーザー グループ名を指定します                                                                                                            | 必須 |
| **listen**    | 次の値のいずれかを指定します。 [はい]。Url を登録するユーザーを許可します。 これが既定値です。 違います：Url の登録からユーザーを拒否します。 | 省略可能 |
| **デリゲート**  | 次の値のいずれかを指定します。 [はい]。いいえ、Url を委任するユーザーを許可します。ユーザーが Url の委任を拒否します。 これが既定値です。   | 省略可能 |
| **sddl**      | DACL を記述する SDDL 文字列を指定します。                                                                                                | 省略可能 |
---

**使用例**

4 つの例を次に、**追加 urlacl**コマンド。

-   追加 urlacl url =https://+:80/MyUriユーザー ドメインを =\\ユーザー
-   add urlacl url=https://www.contoso.com:80/MyUri user=DOMAIN\\user listen=yes
-   追加 urlacl url =https://www.contoso.com:80/MyUriユーザー ドメインを =\\ユーザー デリゲート = いいえ
-   追加 urlacl url =https://+:80/MyUri sddl = しています.

---

## <a name="delete-cache"></a>キャッシュを削除します。

HTTP サービス、カーネル URI キャッシュからすべてのエントリ、または指定したエントリを削除します。

**構文**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**Parameters**
| | | |
|---|---|---|
| **url**       | 完全修飾 Locator (URL) を削除するを指定します。                                        | 省略可能 |
| **recursive** | Url のキャッシュの下のすべてのエントリが削除を取得するかどうかを指定します。 **[はい]**: すべてのエントリを削除する**ありません**: すべてのエントリを削除しないでください | 省略可能 |
---

**使用例**

2 つの例を次に、**キャッシュを削除して**コマンド。

-   キャッシュの url を削除 =https://www.contoso.com:80/myresource/再帰 = [はい]
-   キャッシュを削除します。

---

## <a name="delete-iplisten"></a>iplisten を削除します。

IP リッスン一覧から IP アドレスを削除します。 IP リッスン一覧は、HTTP サービスがバインド アドレスの一覧の範囲に使用されます。

**構文**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**Parameters**
| | | |
|---|---|---|
| **ip アドレス** | Ip アドレスから削除する IPv4 または IPv6 アドレスは、リストをリッスンします。 IP リッスン一覧は、HTTP サービスがバインド アドレスの一覧の範囲に使用されます。 任意の IPv4 アドレスを意味する「0.0.0.0」と"::"任意の IPv6 アドレスのことを意味します。 これは、ポート番号には含まれません。 | 必須 |
---


**使用例**

4 つの例を次に、**削除 iplisten**コマンド。

-   削除 iplisten ipaddress fe80::1 を =
-   削除 iplisten ipaddress 1.1.1.1 を =
-   削除 iplisten ip アドレス 0.0.0.0 を =
-   delete iplisten ipaddress=::

---

## <a name="delete-sslcert"></a>sslcert を削除します。


SSL サーバー証明書のバインドと、IP アドレスとポートの対応するクライアント証明書ポリシーを削除します。

**構文**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**Parameters**
| | | |
|---|---|---|
| **ipport** | IPv4 または IPv6 アドレスと SSL 証明書のバインドを削除するポートを指定します。 コロン (:)IP アドレスとポート番号の間の区切り記号として使用されます。 | 必須 |
---


**使用例**

次の 3 つの例を次に、**削除 sslcert**コマンド。

- delete sslcert ipport=1.1.1.1:443
- delete sslcert ipport=0.0.0.0:443
- sslcert ipport の削除 [::] =: 443

---

## <a name="delete-timeout"></a>タイムアウトを削除します。

グローバル タイムアウトを削除し、サービスの既定値に戻すには、します。

**構文**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**Parameters**
| | | |
|---|---|---|
| **timeouttype** | タイムアウト設定の種類を指定します。 | 必須 |
---


**使用例**

2 つの例を次に、**削除タイムアウト**コマンド。

-   削除タイムアウト timeouttype idleconnectiontimeout を =
-   削除タイムアウト timeouttype headerwaittimeout を =

---

## <a name="delete-urlacl"></a>urlacl を削除します。

URL 予約を削除します。

**構文**

```powershell
delete urlacl [ url= ] URL
```

**Parameters**
| | | |
|---|---|---|
| **url** | 完全修飾 Locator (URL) を削除するを指定します。 | 必須 |
---


**使用例**

2 つの例を次に、**削除 urlacl**コマンド。

-   削除 urlacl url =https://+:80/MyUri
-   削除 urlacl url =https://www.contoso.com:80/MyUri

---

## <a name="flush-logbuffer"></a>logbuffer をフラッシュします。

ログ ファイルの内部バッファーをフラッシュします。

**構文**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>cachestate を表示します。

リストは、URI のリソースとその関連プロパティをキャッシュします。 このコマンドは、すべてのリソースとその関連プロパティは HTTP 応答のキャッシュにキャッシュまたは 1 つのリソースと関連付けられたプロパティを表示する一覧表示します。

**構文**

```powershell
show cachestate [ [url= ] URL]
```

**Parameters**
| | | |
|---|---|---|
| **url** | 表示する完全修飾 URL を指定します。 指定しない場合は、すべての Url を表示します。 URL は、登録された Url のプレフィックスを場合もあります。 | 省略可能 |
---


**使用例**

2 つの例を次に、**表示 cachestate**コマンド。

-   cachestate url の表示 =https://www.contoso.com:80/myresource
-   cachestate を表示します。

---

## <a name="show-iplisten"></a>iplisten を表示します。

IP リッスン一覧で、すべての IP アドレスを表示します。 IP リッスン一覧は、HTTP サービスがバインド アドレスの一覧の範囲に使用されます。 任意の IPv4 アドレスを意味する「0.0.0.0」と"::"任意の IPv6 アドレスのことを意味します。

**構文**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>servicestate を表示します。

HTTP サービスのスナップショットを表示します。

**構文**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**Parameters**
| | | |
|---|---|---|
| **[表示]**    | サーバーのセッションや要求キューに基づいて HTTP サービスの状態のスナップショットを表示するかどうかを指定します。 | 省略可能 |
| **詳細** | プロパティ情報を表示する詳細な情報を表示するかどうかを指定します。                               | 省略可能 |
---

**使用例**

2 つの例を次に、**表示 servicestate**コマンド。

-   servicestate ビューを表示する「セッション」を =
-   show servicestate view="requestq"

---

## <a name="show-sslcert"></a>sslcert を表示します。

Secure Sockets Layer (SSL) サーバー証明書のバインドと、IP アドレスとポートの対応するクライアント証明書ポリシーを表示します。

**構文**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**Parameters**
| | | |
|---|---|---|
| **ipport** | IPv4 または IPv6 アドレスとポート、SSL がバインド表示証明書を指定します。 コロン (:)IP アドレスとポート番号の間の区切り記号として使用されます。 Ipport を指定しない場合は、すべてのバインドが表示されます。 | 必須 |
---


**使用例**

5 つ例を次に、**表示 sslcert**コマンド。

-   sslcert ipport の表示 [fe80::1] =: 443
-   表示 sslcert ipport 1.1.1.1:443 を =
-   show sslcert ipport=0.0.0.0:443
-   sslcert ipport の表示 [::] =: 443
-   sslcert を表示します。

---

## <a name="show-timeout"></a>タイムアウトを表示します。

HTTP サービスのタイムアウト値を秒単位で表示します。

**構文**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>urlacl を表示します。

指定された予約済みの URL または予約済みのすべての Url のリスト (Dacl) を随意アクセス制御を表示します。

**構文**

```powershell
show urlacl [ [url= ] URL]
```

**Parameters**
| | | |
|---|---|---|
| **url** | 表示する完全修飾 URL を指定します。 いない指定した場合は、すべての Url を表示します。 | 省略可能 |
---


**使用例**

次の 3 つの例を次に、 **urlacl を表示する**コマンド。

-   表示 urlacl url =https://+:80/MyUri
-   表示 urlacl url =https://www.contoso.com:80/MyUri
-   urlacl を表示します。

---