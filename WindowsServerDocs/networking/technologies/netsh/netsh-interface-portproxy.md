---
title: interface portproxy の netsh コマンド
description: IPv4 および IPv6 のネットワークとアプリケーション間でプロキシとして機能させるために、netsh interface portproxy コマンドを使用します。
ms.topic: article
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 08/30/2018
ms.openlocfilehash: 2b05db55ef914130a337b38ea92b41e0cef81dc9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964028"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh interface portproxy コマンド

IPv4 および IPv6 のネットワークとアプリケーション間でプロキシとして機能させるために、**netsh interface portproxy** コマンドを使用します。 これらのコマンドを使用して、次の方式でプロキシ サービスを確立できます。

-   IPv4 で構成されたコンピューターおよびアプリケーションのメッセージが、IPv4 で構成された他のコンピューターおよびアプリケーションに送信される。

-   IPv4 で構成されたコンピューターおよびアプリケーションのメッセージが、IPv6 で構成されたコンピューターおよびアプリケーションに送信される。

-   IPv6 で構成されたコンピューターおよびアプリケーションのメッセージが、IPv4 で構成されたコンピューターおよびアプリケーションに送信される。

-   IPv6 で構成されたコンピューターおよびアプリケーションのメッセージが、IPv6 で構成された他のコンピューターおよびアプリケーションに送信される。

これらのコマンドを使用してバッチ ファイルまたはスクリプトを作成する場合、各コマンドは **netsh interface portproxy** から開始される必要があります。 たとえば、**delete v4tov6** コマンドを使用して、ポートプロキシ サーバー上でサーバーがリッスンする IPv4 アドレスの一覧から IPv4 ポートとアドレスを削除する場合、バッチ ファイルまたはスクリプトでは次の構文を使用する必要があります。

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

利用可能な netsh interface portproxy コマンドを次に示します。

-   [add v4tov4](#add-v4tov4)

-   [add v4tov6](#add-v4tov6)

-   [add v6tov4](#add-v6tov4)

-   [add v6tov6](#add-v6tov6)

-   [delete v4tov4](#delete-v4tov4)

-   [delete v4tov6](#delete-v4tov6)

-   [delete v6tov6](#delete-v6tov6)

-   [reset](#reset)

-   [set v4tov4](#set-v4tov4)

-   [set v4tov6](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [set v6tov6](#set-v6tov6)

-   [show all](#show-all)

-   [show v4tov4](#show-v4tov4)

-   [show v4tov6](#show-v4tov6)

-   [show v6tov4](#show-v6tov4)

-   [show v6tov6](#show-v6tov6)


## <a name="add-v4tov4"></a>add v4tov4

ポートプロキシ サーバーでは、特定のポートと IPv4 アドレスに送信されるメッセージをリッスンして、別個の TCP 接続が確立された後に受信したメッセージを送信するためのポートと IPv4 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv4 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v4tov6"></a>add v4tov6

ポートプロキシ サーバーでは、特定のポートと IPv4 アドレスに送信されるメッセージをリッスンして、別個の TCP 接続が確立された後に受信したメッセージを送信するためのポートと IPv6 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv6 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov4"></a>add v6tov4

ポートプロキシ サーバーでは、特定のポートと IPv6 アドレスに送信されるメッセージをリッスンして、別個の TCP 接続が確立された後に受信したメッセージの送信先とするポートと IPv4 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv4 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov6"></a>add v6tov6

ポートプロキシ サーバーでは、特定のポートと IPv6 アドレスに送信されるメッセージをリッスンして、別個の TCP 接続が確立された後に受信したメッセージの送信先とするポートと IPv6 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv6 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="delete-v4tov4"></a>delete v4tov4

ポートプロキシ サーバーでは、サーバーがリッスンする IPv4 ポートとアドレスの一覧から、IPv4 アドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    削除する IPv4 ポートを指定します。                                    |
| **listenaddress** | 削除する IPv4 アドレスを指定します。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|   **protocol**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v4tov6"></a>delete v4tov6

ポートプロキシ サーバーでは、サーバーがリッスンする IPv4 アドレスの一覧から、IPv4 ポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    削除する IPv4 ポートを指定します。                                    |
| **listenaddress** | 削除する IPv4 アドレスを指定します。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|   **protocol**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov4"></a>delete v6tov4

ポートプロキシ サーバーでは、サーバーがリッスンする IPv6 アドレスの一覧から、IPv6 ポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    削除する IPv6 ポートを指定します。                                    |
| **listenaddress** | 削除する IPv6 アドレスを指定します。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|   **protocol**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov6"></a>delete v6tov6

ポートプロキシ サーバーでは、サーバーがリッスンする IPv6 アドレスの一覧から、IPv6 アドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    削除する IPv6 ポートを指定します。                                    |
| **listenaddress** | 削除する IPv6 アドレスを指定します。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|   **protocol**    |                                      使用するプロトコルを指定します。                                      |

## <a name="reset"></a>reset

IPv6 構成の状態をリセットします。

### <a name="syntax"></a>構文

`reset`

## <a name="set-v4tov4"></a>set v4tov4

**add v4tov4** コマンドを使用して作成されたポートプロキシ サーバー上での既存のエントリのパラメーター値を変更するか、またはポート/アドレスのペアをマップする新しいエントリを一覧に追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv4 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v4tov6"></a>set v4tov6

**add v4tov6** コマンドを使用して作成されたポートプロキシ サーバー上での既存のエントリのパラメーター値を変更するか、またはポート/アドレスのペアをマップする新しいエントリを一覧に追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv6 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov4"></a>set v6tov4

**add v6tov4** コマンドを使用して作成されたポートプロキシ サーバー上での既存のエントリのパラメーター値を変更するか、またはポート/アドレスのペアをマップする新しいエントリを一覧に追加します。

### <a name="syntax"></a>構文

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           ポート番号またはサービス名によって、リッスンする IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。 |
|  **connectport**   |       ポート番号またはサービス名によって、接続する IPv4 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|    **protocol**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov6"></a>set v6tov6

**add v6tov6** コマンドを使用して作成されたポートプロキシ サーバー上での既存のエントリのパラメーター値を変更するか、またはポート/アドレスのペアをマップする新しいエントリを一覧に追加します。

### <a name="syntax"></a>構文

```PowerShell
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

#### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                            ポート番号またはサービス名によって、リッスンする IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されない場合、既定値はローカル コンピューターです。  |
|  **connectport**   |        ポート番号またはサービス名によって、接続する IPv6 ポートを指定します。 **connectport** が指定されない場合、既定値はローカル コンピューター上の **listenport** の値です。        |
| **listenaddress**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスを指定しない場合、既定値はローカル コンピューターです。 |
|    **protocol**    |                                                                                   使用するプロトコルを指定します。                                                                                   |

## <a name="show-all"></a>すべての表示

v4tov4、v4tov6、v6tov4、および v6tov6 のポート/アドレスのペアを含め、すべてのポートプロキシ パラメータ―を表示します。

### <a name="syntax"></a>構文

`show all`


## <a name="show-v4tov4"></a>show v4tov4

v4tov4 ポートプロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov4`

## <a name="show-v4tov6"></a>show v4tov6

v4tov6 ポートプロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov6`

## <a name="show-v6tov4"></a>show v6tov4

v6tov4 ポートプロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov4`


## <a name="show-v6tov6"></a>show v6tov6

v6tov6 ポートプロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov6`

---
