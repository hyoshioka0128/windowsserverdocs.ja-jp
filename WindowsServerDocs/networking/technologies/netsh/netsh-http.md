---
title: ハイパーテキスト転送プロトコル (HTTP) 用の Netsh コマンド
description: Netsh http を使用して、http.sys の設定とパラメーターを照会および構成します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7b9032eb05128532c8bf90a0db2f685b4435e6eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401878"
---
# <a name="netsh-http-commands"></a>Netsh http コマンド


**Netsh http**を使用して、http.sys の設定とパラメーターを照会および構成します。  

>[!TIP]
>Windows Server 2016 または Windows 10 を実行しているコンピューターで Windows PowerShell を使用している場合は、「 **netsh** 」と入力し、enter キーを押します。 Netsh プロンプトで、「 **http** 」と入力し、enter キーを押して netsh http プロンプトを取得します。
>
>&nbsp; @ no__t @ no__t @ no__t @ no__t @ no__t @ no__t @-6netsh http @-7 のようになります。

使用できる netsh http コマンドは次のとおりです。

- [iplisten の追加](#add-iplisten)
- [sslcert の追加](#add-sslcert)
- [タイムアウトの追加](#add-timeout)
- [urlacl の追加](#add-urlacl)
- [キャッシュの削除](#delete-cache)
- [iplisten の削除](#delete-iplisten)
- [sslcert の削除](#delete-sslcert)
- [削除のタイムアウト](#delete-timeout)
- [urlacl の削除](#delete-urlacl)
- [ログバッファーのフラッシュ](#flush-logbuffer)
- [キャッシュ資産の表示](#show-cachestate)
- [iplisten の表示](#show-iplisten)
- [servicestate の表示](#show-servicestate)
- [sslcert の表示](#show-sslcert)
- [タイムアウトの表示](#show-timeout)
- [urlacl の表示](#show-urlacl)

## <a name="add-iplisten"></a>iplisten の追加

IP リッスン一覧に新しい IP アドレスを追加します (ポート番号は除く)。

**構文**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**パラメーター**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP リッスン一覧に追加する IPv4 または IPv6 アドレス。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。 | 必須 |

---

**例**

**Add iplisten**コマンドの4つの例を次に示します。

-   add iplisten ipaddress = fe80:: 1
-   add iplisten ipaddress = 1.1.1.1
-   add iplisten ipaddress = 0.0.0.0
-   add iplisten ipaddress =::

---

## <a name="add-sslcert"></a>sslcert の追加

新しい SSL サーバー証明書のバインドと、IP アドレスとポートに対応するクライアント証明書のポリシーを追加します。

**構文**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**パラメーター**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **ipport**                  |                       バインドの IP アドレスとポートを指定します。 コロン文字 (:)は、IP アドレスとポート番号の間の区切り記号として使用されます。                        | 必須 |
|                 **certhash**                 |                                     証明書の SHA ハッシュを指定します。 このハッシュは長さが20バイトで、16進数の文字列として指定されます。                                      | 必須 |
|                  **appid**                   |                                                                  所有しているアプリケーションを識別する GUID を指定します。                                                                  | 必須 |
|              **certstorename**               |                                  証明書のストア名を指定します。 既定値は MY です。 証明書はローカルコンピューターのコンテキストに格納されている必要があります。                                  | 省略可能 |
|        **verifyclientcertrevocation**        |                                                      クライアント証明書の失効の検証をオンまたはオフにすることを指定します。                                                       | 省略可能 |
| **verifyrevocationwithcachedclientcertonly** |                                      失効確認用にキャッシュされたクライアント証明書のみの使用を有効または無効にするかどうかを指定します。                                       | 省略可能 |
|                **usagecheck**                |                                                      使用状況の確認を有効にするか無効にするかを指定します。 既定値は有効です。                                                       | 省略可能 |
|         **revocationfreshnesstime**          | 更新された証明書失効リスト (CRL) を確認する時間間隔を秒単位で指定します。 この値が0の場合、新しい CRL は、前の CRL が期限切れになった場合にのみ更新されます。 | 省略可能 |
|           **urlretrievaltimeout**            |                            リモート URL の証明書失効リストを取得しようとした後のタイムアウト間隔をミリ秒単位で指定します。                            | 省略可能 |
|             **sslctlidentifier**             |                信頼できる証明書の発行者の一覧を指定します。 この一覧は、コンピューターによって信頼されている証明書発行者のサブセットにすることができます。                 | 省略可能 |
|             **sslctlstorename**              |                                                SslCtlIdentifier が格納されている LOCAL_MACHINE の証明書ストアの名前を指定します。                                                | 省略可能 |
|              **dsmapperusage**               |                                                        DS マッパーを有効にするか無効にするかを指定します。 既定では、無効になっています。                                                         | 省略可能 |
|          **clientcertnegotiation**           |                                              証明書のネゴシエーションを有効にするか無効にするかを指定します。 既定では、無効になっています。                                               | 省略可能 |

---

**例**

次に、 **[sslcert の追加]** コマンドの例を示します。

sslcert ipport = 1.1.1.1: 443 certhash = 0102030405060708090A0B0C0D0E0F1011121314 appid = {00112233-4455-6677} を追加します。

---

## <a name="add-timeout"></a>タイムアウトの追加

サービスにグローバルタイムアウトを追加します。

**構文** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**パラメーター**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    設定のタイムアウトの種類。                                     |
|    **value**    | タイムアウトの値 (秒単位)。 値が16進表記の場合は、プレフィックス0x を追加します。 |

---

**例**

次に、 **add timeout**コマンドの2つの例を示します。

-   add timeout timeouttype = idleconnectiontimeout value = 120
-   add timeout timeouttype = headerwaittimeout 値 = 0x40

---

## <a name="add-urlacl"></a>urlacl の追加

Uniform Resource Locator (URL) 予約エントリを追加します。 このコマンドは、管理者以外のユーザーとアカウントの URL を予約します。 DACL は、リッスンパラメーターとデリゲートパラメーターを使用するか、SDDL 文字列を使用して、NT アカウント名を使用して指定できます。

**構文**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**パラメーター**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **先**    |                                          完全修飾 Uniform Resource Locator (URL) を指定します。                                           | 必須 |
|   **user**   |                                                      ユーザーまたはユーザーグループの名前を指定します。                                                       | 必須 |
|  **意見**  | 次のいずれかの値を指定します。はい:ユーザーが Url を登録できるようにします。 これは既定値です。 違います：ユーザーによる Url の登録を拒否します。 | 省略可能 |
| **人** |  次のいずれかの値を指定します。はい:ユーザーが Url を委任できないようにする:ユーザーが Url を委任できないようにします。 これは既定値です。  | 省略可能 |
|   **sddl**   |                                                DACL を説明する SDDL 文字列を指定します。                                                 | 省略可能 |

---

**例**

**Urlacl の追加**コマンドの4つの例を次に示します。

- add urlacl url = https://+:80/MyUri user = DOMAIN @ no__t-1user
- add urlacl url = <https://www.contoso.com:80/MyUri> user = DOMAIN @ no__t-1user listen = yes
- add urlacl url = <https://www.contoso.com:80/MyUri> user = DOMAIN @ no__t-1user delegate = no
- add urlacl url = https://+:80/MyUri sddl =...

---

## <a name="delete-cache"></a>キャッシュの削除

HTTP サービスのカーネル URI キャッシュから、エントリまたは指定されたエントリをすべて削除します。

**構文**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**パラメーター**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **先**    |                    削除する完全修飾 Uniform Resource Locator (URL) を指定します。                     | 省略可能 |
| **繰り返し** | Url キャッシュ内のすべてのエントリが削除されるかどうかを指定します。 **はい**: すべてのエントリを削除**しません。すべて**のエントリを削除しないでください | 省略可能 |

---

**例**

次に、 **delete cache**コマンドの2つの例を示します。

- キャッシュ url の削除 = <https://www.contoso.com:80/myresource/> recursive = yes
- キャッシュの削除

---

## <a name="delete-iplisten"></a>iplisten の削除

Ip リッスン一覧から IP アドレスを削除します。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。

**構文**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**パラメーター**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | IP リッスン一覧から削除する IPv4 または IPv6 アドレス。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。 これには、ポート番号は含まれません。 | 必須 |

---


**例**

**Delete iplisten**コマンドの4つの例を次に示します。

-   delete iplisten ipaddress = fe80:: 1
-   delete iplisten ipaddress = 1.1.1.1
-   delete iplisten ipaddress = 0.0.0.0
-   delete iplisten ipaddress =::

---

## <a name="delete-sslcert"></a>sslcert の削除


SSL サーバー証明書のバインドおよび IP アドレスとポートに対応するクライアント証明書のポリシーを削除します。

**構文**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**パラメーター**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 証明書のバインドを削除する IPv4 または IPv6 のアドレスとポートを指定します。 コロン文字 (:)は、IP アドレスとポート番号の間の区切り記号として使用されます。 | 必須 |

---


**例**

次に、 **delete sslcert**コマンドの3つの例を示します。

- sslcert ipport = 1.1.1.1: 443 を削除します。
- sslcert ipport = 0.0.0.0: 443 を削除します。
- sslcert ipport = [::]: 443 を削除します。

---

## <a name="delete-timeout"></a>削除のタイムアウト

グローバルタイムアウトを削除し、サービスを既定値に戻します。

**構文**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**パラメーター**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | タイムアウト設定の種類を指定します。 | 必須 |

---


**例**

**Delete timeout**コマンドの2つの例を次に示します。

-   delete timeout timeouttype = idleconnectiontimeout
-   delete timeout timeouttype = headerwaittimeout

---

## <a name="delete-urlacl"></a>urlacl の削除

URL 予約を削除します。

**構文**

```powershell
delete urlacl [ url= ] URL
```

**パラメーター**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **先** | 削除する完全修飾 Uniform Resource Locator (URL) を指定します。 | 必須 |

---


**例**

次に、 **delete urlacl**コマンドの2つの例を示します。

- urlacl url の削除 = https://+:80/MyUri
- urlacl url の削除 = <https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>ログバッファーのフラッシュ

ログログの内部バッファーをフラッシュします。

**構文**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>キャッシュ資産の表示

キャッシュされた URI リソースとそれらに関連付けられているプロパティを一覧表示します。 このコマンドは、HTTP 応答キャッシュにキャッシュされているすべてのリソースとそれに関連付けられているプロパティを一覧表示します。また、1つのリソースとその関連プロパティを表示します。

**構文**

```powershell
show cachestate [ [url= ] URL]
```

**パラメーター**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **先** | 表示する完全修飾 URL を指定します。 指定しない場合は、すべての Url が表示されます。 URL は、登録された Url のプレフィックスにすることもできます。 | 省略可能 |

---


**例**

**Show cachestate**コマンドの2つの例を次に示します。

- cachestate url の表示 = <https://www.contoso.com:80/myresource>
- キャッシュ資産の表示

---

## <a name="show-iplisten"></a>iplisten の表示

IP リッスン一覧のすべての IP アドレスを表示します。 IP リッスン一覧は、HTTP サービスがバインドされるアドレスのリストのスコープを指定するために使用されます。 "0.0.0.0" は任意の IPv4 アドレスを意味し、"::" は任意の IPv6 アドレスを意味します。

**構文**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>servicestate の表示

HTTP サービスのスナップショットを表示します。

**構文**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**パラメーター**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **[表示]**   | サーバーセッションまたは要求キューに基づいて HTTP サービスの状態のスナップショットを表示するかどうかを指定します。 | 省略可能 |
| **な** |                プロパティ情報も表示する詳細情報を表示するかどうかを指定します。                | 省略可能 |

---

**例**

**Show servicestate**コマンドの2つの例を次に示します。

-   servicestate view = "session" を表示します
-   servicestate view = "requestq" を表示します

---

## <a name="show-sslcert"></a>sslcert の表示

Secure Sockets Layer (SSL) サーバー証明書のバインドと、IP アドレスとポートに対応するクライアント証明書のポリシーが表示されます。

**構文**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**パラメーター**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | SSL 証明書のバインドを表示する IPv4 または IPv6 のアドレスとポートを指定します。 コロン文字 (:)は、IP アドレスとポート番号の間の区切り記号として使用されます。 Ipport を指定しない場合は、すべてのバインドが表示されます。 | 必須 |

---


**例**

次に、 **[sslcert の表示]** コマンドの5つの例を示します。

-   表示 sslcert ipport = [fe80:: 1]: 443
-   sslcert ipport = 1.1.1.1: 443 の表示
-   sslcert ipport = 0.0.0.0: 443 の表示
-   sslcert ipport = [::]: 443 を表示します
-   sslcert の表示

---

## <a name="show-timeout"></a>タイムアウトの表示

HTTP サービスのタイムアウト値を秒単位で表示します。

**構文**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>urlacl の表示

指定された予約済み URL またはすべての予約済み url の随意アクセス制御リスト (Dacl) を表示します。

**構文**

```powershell
show urlacl [ [url= ] URL]
```

**パラメーター**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **先** | 表示する完全修飾 URL を指定します。 それ以外の場合は、すべての Url を表示します。 | 省略可能 |

---


**例**

**Show urlacl**コマンドの3つの例を次に示します。

- show urlacl url = https://+:80/MyUri
- show urlacl url = <https://www.contoso.com:80/MyUri>
- urlacl の表示

---