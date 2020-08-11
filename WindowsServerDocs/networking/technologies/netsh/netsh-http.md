---
title: ハイパーテキスト転送プロトコル (HTTP) 用の Netsh コマンド
description: netsh http を使用して、HTTP.sys の設定とパラメーターを照会および構成します。
ms.topic: article
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a2bf580dff85463306767b6a129819b82f4fc85c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946986"
---
# <a name="netsh-http-commands"></a>Netsh http コマンド


**netsh http** を使用して、HTTP.sys の設定とパラメーターを照会および構成します。

>[!TIP]
>Windows Server 2016 または Windows 10 を実行しているコンピューターで Windows PowerShell を使用している場合は、**netsh** と入力して Enter キーを押します。 netsh プロンプトで、「**http**」と入力し、Enter キーを押して netsh http プロンプトを取得します。
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

使用できる netsh http コマンドは次のとおりです。

- [add iplisten](#add-iplisten)
- [add sslcert](#add-sslcert)
- [add timeout](#add-timeout)
- [add urlacl](#add-urlacl)
- [delete cache](#delete-cache)
- [delete iplisten](#delete-iplisten)
- [delete sslcert](#delete-sslcert)
- [delete timeout](#delete-timeout)
- [delete urlacl](#delete-urlacl)
- [flush logbuffer](#flush-logbuffer)
- [show cachestate](#show-cachestate)
- [show iplisten](#show-iplisten)
- [show servicestate](#show-servicestate)
- [show sslcert](#show-sslcert)
- [show timeout](#show-timeout)
- [show urlacl](#show-urlacl)

## <a name="add-iplisten"></a>add iplisten

IP リッスン一覧に新しい IP アドレスを追加します (ポート番号は除く)。

**構文**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP リッスン一覧に追加する IPv4 または IPv6 アドレス。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。 | 必須 |

---

**例**

**add iplisten** コマンドの 4 つの例を次に示します。

-   add iplisten ipaddress=fe80::1
-   add iplisten ipaddress=1.1.1.1
-   add iplisten ipaddress=0.0.0.0
-   add iplisten ipaddress=::

---

## <a name="add-sslcert"></a>add sslcert

IP アドレスとポートについての新しい SSL サーバー証明書のバインドと、対応するクライアント証明書ポリシーを追加します。

**構文**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**Parameters**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **ipport**                  |                       バインド用の IP アドレスとポートを指定します。 IP アドレスとポート番号の間の区切り記号としてコロン文字 (:) が使用されます。                        | 必須 |
|                 **certhash**                 |                                     証明書の SHA ハッシュを指定します。 このハッシュは長さが 20 バイトで、16 進数の文字列として指定されます。                                      | 必須 |
|                  **appid**                   |                                                                  所有しているアプリケーションを識別する GUID を指定します。                                                                  | 必須 |
|              **certstorename**               |                                  証明書のストア名を指定します。 既定では MY に設定されます。 証明書はローカル コンピューターのコンテキストに格納される必要があります。                                  | オプション |
|        **verifyclientcertrevocation**        |                                                      クライアント証明書の失効の検証をオンまたはオフにすることを指定します。                                                       | オプション |
| **verifyrevocationwithcachedclientcertonly** |                                      キャッシュされたクライアント証明書のみを失効確認用に使用することを有効にするか無効にするかを指定します。                                       | オプション |
|                **usagecheck**                |                                                      使用状況チェックを有効にするか無効にするかを指定します。 既定では有効になっています。                                                       | オプション |
|         **revocationfreshnesstime**          | 更新された証明書失効リスト (CRL) を確認する時間間隔を秒単位で指定します。 この値が 0 の場合、新しい CRL は前の CRL が期限切れになった場合にのみ更新されます。 | オプション |
|           **urlretrievaltimeout**            |                            リモート URL の証明書失効リストを取得しようとした後のタイムアウト間隔をミリ秒単位で指定します。                            | オプション |
|             **sslctlidentifier**             |                信頼できる証明書の発行者の一覧を指定します。 この一覧は、コンピューターによって信頼されている証明書の発行者のサブセットにすることができます。                 | オプション |
|             **sslctlstorename**              |                                                SslCtlIdentifier が格納される LOCAL_MACHINE の証明書ストアの名前を指定します。                                                | オプション |
|              **dsmapperusage**               |                                                        DS マッパーが有効であるか、無効であるかを指定します。 既定では、無効になっています。                                                         | オプション |
|          **clientcertnegotiation**           |                                              証明書のネゴシエーションを有効にするか無効にするかを指定します。 既定では、無効になっています。                                               | オプション |

---

**例**

**add sslcert** コマンドの例を次に示します。

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>add timeout

サービスにグローバル タイムアウトを追加します。

**構文**

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**Parameters**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    設定のタイムアウトの種類。                                     |
|    **value**    | タイムアウトの値 (秒)。 値が 16 進表記の場合は、プレフィックス 0x を追加します。 |

---

**例**

**add timeout** コマンドの 2 つの例を次に示します。

-   add timeout timeouttype=idleconnectiontimeout value=120
-   add timeout timeouttype=headerwaittimeout value=0x40

---

## <a name="add-urlacl"></a>add urlacl

URL (Uniform Resource Locator) 予約エントリを追加します。 このコマンドは、管理者以外のユーザーとアカウント用に URL を予約します。 DACL は、listen パラメーターと delegate パラメーターとともに NT アカウント名を使用するか、SDDL 文字列を使用して指定できます。

**構文**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**Parameters**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **url**    |                                          完全修飾 URL (Uniform Resource Locator) を指定します。                                           | 必須 |
|   **user**   |                                                      ユーザーまたはユーザー グループの名前を指定します                                                       | 必須 |
|  **listen**  | 次のいずれかの値を指定します。yes:ユーザーが URL を登録できるようにします。 これは、既定値です。 no:ユーザーによる URI の登録を拒否します。 | オプション |
| **delegate** |  次のいずれかの値を指定します。yes:ユーザーが URL を委任できるようにします。no:ユーザーが URL を委任できないようにします。 これは、既定値です。  | オプション |
|   **sddl**   |                                                DACL を説明する SDDL 文字列を指定します。                                                 | オプション |

---

**例**

**add urlacl** コマンドの 4 つの例を次に示します。

- add urlacl url=https://+:80/MyUri user=DOMAIN\\ user
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user listen=yes
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user delegate=no
- add urlacl url=https://+:80/MyUri sddl=...

---

## <a name="delete-cache"></a>delete cache

HTTP サービス カーネル URI キャッシュから、すべてのエントリまたは指定されたエントリを削除します。

**構文**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**Parameters**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **url**    |                    削除する完全修飾 URL (Uniform Resource Locator) を指定します。                     | オプション |
| **recursive** | URI キャッシュ内のすべてのエントリが削除されるかどうかを指定します。 **yes**: すべてのエントリを削除します **no**: すべてのエントリを削除しません | オプション |

---

**例**

**delete cache** コマンドの 2 つの例を次に示します。

- delete cache url=<https://www.contoso.com:80/myresource/> recursive=yes
- delete cache

---

## <a name="delete-iplisten"></a>delete iplisten

IP リッスン一覧から IP アドレスを削除します。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。

**構文**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP リッスン一覧から削除する IPv4 または IPv6 アドレス。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。 これにはポート番号は含まれません。 | 必須 |

---


**例**

**delete iplisten** コマンドの 4 つの例を次に示します。

-   delete iplisten ipaddress=fe80::1
-   delete iplisten ipaddress=1.1.1.1
-   delete iplisten ipaddress=0.0.0.0
-   delete iplisten ipaddress=::

---

## <a name="delete-sslcert"></a>delete sslcert


IP アドレスとポートについての SSL サーバー証明書のバインドと、対応するクライアント証明書ポリシーを削除します。

**構文**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 証明書のバインドを削除する IPv4 アドレスまたは IPv6 アドレスとポートを指定します。 IP アドレスとポート番号の間の区切り記号としてコロン文字 (:) が使用されます。 | 必須 |

---


**例**

**delete sslcert** コマンドの 3 つの例を次に示します。

- delete sslcert ipport=1.1.1.1:443
- delete sslcert ipport=0.0.0.0:443
- delete sslcert ipport=[::]:443

---

## <a name="delete-timeout"></a>delete timeout

グローバル タイムアウトを削除し、サービスを既定値に戻します。

**構文**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**Parameters**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | タイムアウト設定の種類を指定します。 | 必須 |

---


**例**

**delete timeout** コマンドの 2 つの例を次に示します。

-   delete timeout timeouttype=idleconnectiontimeout
-   delete timeout timeouttype=headerwaittimeout

---

## <a name="delete-urlacl"></a>delete urlacl

URL 予約を削除します。

**構文**

```powershell
delete urlacl [ url= ] URL
```

**Parameters**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **url** | 削除する完全修飾 URL (Uniform Resource Locator) を指定します。 | 必須 |

---


**例**

**delete urlacl** コマンドの 2 つの例を次に示します。

- delete urlacl url=https://+:80/MyUri
- delete urlacl url=<https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>flush logbuffer

ログファイルの内部バッファーをフラッシュします。

**構文**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>show cachestate

キャッシュされた URI リソースとそれらに関連付けられているプロパティを一覧表示します。 このコマンドは、HTTP 応答キャッシュにキャッシュされているすべてのリソースとその関連プロパティを一覧表示するか、1 つのリソースとその関連プロパティを表示します。

**構文**

```powershell
show cachestate [ [url= ] URL]
```

**Parameters**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **url** | 表示する完全修飾 URL を指定します。 指定しない場合は、すべての URL が表示されます。 URL は、登録された URL のプレフィックスにすることもできます。 | オプション |

---


**例**

**show cachestate** コマンドの 2 つの例を次に示します。

- show cachestate url=<https://www.contoso.com:80/myresource>
- show cachestate

---

## <a name="show-iplisten"></a>show iplisten

IP リッスン一覧内のすべての IP アドレスを表示します。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。

**構文**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>show servicestate

HTTP サービスのスナップショットを表示します。

**構文**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**Parameters**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **表示**   | サーバー セッションまたは要求キューに基づいて、HTTP サービス状態のスナップショットを表示するかどうかを指定します。 | オプション |
| **Verbose** |                プロパティ情報も表示する詳細情報を表示するかどうかを指定します。                | オプション |

---

**例**

**show servicestate** コマンドの 2 つの例を次に示します。

-   show servicestate view="session"
-   show servicestate view="requestq"

---

## <a name="show-sslcert"></a>show sslcert

IP アドレスとポートについての Secure Sockets Layer (SSL) サーバー証明書のバインドと、対応するクライアント証明書ポリシーを表示します。

**構文**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 証明書のバインドを表示する IPv4 アドレスまたは IPv6 アドレスとポートを指定します。 IP アドレスとポート番号の間の区切り記号としてコロン文字 (:) が使用されます。 ipport を指定しない場合は、すべてのバインドが表示されます。 | 必須 |

---


**例**

**show sslcert** コマンドの 5 つの例を次に示します。

-   show sslcert ipport=[fe80::1]:443
-   show sslcert ipport=1.1.1.1:443
-   show sslcert ipport=0.0.0.0:443
-   show sslcert ipport=[::]:443
-   show sslcert

---

## <a name="show-timeout"></a>show timeout

HTTP サービスのタイムアウト値を秒単位で表示します。

**構文**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>show urlacl

指定された予約済み URL またはすべての予約済み URL の随意アクセス制御リスト (DACL) を表示します。

**構文**

```powershell
show urlacl [ [url= ] URL]
```

**Parameters**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **url** | 表示する完全修飾 URL を指定します。 指定しない場合は、すべての URL が表示されます。 | オプション |

---


**例**

**show urlacl** コマンドの 3 つの例を次に示します。

- show urlacl url=https://+:80/MyUri
- show urlacl url=<https://www.contoso.com:80/MyUri>
- show urlacl

---