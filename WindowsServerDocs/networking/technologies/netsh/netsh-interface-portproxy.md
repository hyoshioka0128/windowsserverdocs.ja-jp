---
title: インターフェイスポートプロキシ用の Netsh コマンド
description: Netsh interface のポートプロキシコマンドを使用して、IPv4 と IPv6 のネットワークとアプリケーションの間のプロキシとして機能します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 6244213ea689f07230ce53288e52959972112037
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405507"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh interface portproxy コマンド

**Netsh interface のポートプロキシ**コマンドを使用して、IPv4 と IPv6 のネットワークとアプリケーションの間のプロキシとして機能します。 これらのコマンドを使用して、次の方法でプロキシサービスを確立できます。

-   IPv4 で構成されたコンピューターおよびアプリケーションメッセージを、IPv4 で構成された他のコンピューターおよびアプリケーションに送信します。

-   IPv6 で構成されたコンピューターおよびアプリケーションに送信される、IPv4 で構成されたコンピューターおよびアプリケーションのメッセージ。

-   IPv4 で構成されたコンピューターおよびアプリケーションに送信される、IPv6 で構成されたコンピューターおよびアプリケーションのメッセージ。

-   IPv6 で構成されたコンピューターおよびアプリケーションメッセージは、IPv6 で構成された他のコンピューターおよびアプリケーションに送信されます。

これらのコマンドを使用してバッチファイルまたはスクリプトを作成する場合、各コマンドは**netsh interface のポートプロキシ**を使用して開始する必要があります。 たとえば、 **delete v4tov6**コマンドを使用して、サーバーがリッスンする ipv4 アドレスの一覧から ipv4 ポートとアドレスを削除するように指定する場合は、バッチファイルまたはスクリプトで次の構文を使用する必要があります。

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

使用可能な netsh interface プロキシコマンドは次のとおりです。

-   [v4tov4 の追加](#add-v4tov4)

-   [v4tov6 の追加](#add-v4tov6)

-   [v6tov4 の追加](#add-v6tov4)

-   [v6tov6 の追加](#add-v6tov6)

-   [v4tov4 の削除](#delete-v4tov4)

-   [v4tov6 の削除](#delete-v4tov6)

-   [v6tov6 の削除](#delete-v6tov6)

-   [解除](#reset)

-   [v4tov4 の設定](#set-v4tov4)

-   [v4tov6 の設定](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [v6tov6 の設定](#set-v6tov6)

-   [すべて表示](#show-all)

-   [v4tov4 の表示](#show-v4tov4)

-   [v4tov6 の表示](#show-v4tov6)

-   [v6tov4 の表示](#show-v6tov4)

-   [v6tov6 の表示](#show-v6tov6)


## <a name="add-v4tov4"></a>v4tov4 の追加

プロキシサーバーは、特定のポートおよび IPv4 アドレスに送信されたメッセージをリッスンし、ポートと IPv4 アドレスをマップして、別の TCP 接続を確立した後に受信したメッセージを送信します。

### <a name="syntax"></a>構文

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv4 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v4tov6"></a>v4tov6 の追加

プロキシサーバーは、特定のポートおよび IPv4 アドレスに送信されたメッセージをリッスンし、ポートと IPv6 アドレスをマップして、別の TCP 接続を確立した後に受信したメッセージを送信します。

### <a name="syntax"></a>構文

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv6 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov4"></a>v6tov4 の追加

プロキシサーバーは、特定のポートおよび IPv6 アドレスに送信されたメッセージをリッスンし、別の TCP 接続を確立した後に受信したメッセージを送信するポートと IPv4 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv4 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov6"></a>v6tov6 の追加

プロキシサーバーは、特定のポートおよび IPv6 アドレスに送信されたメッセージをリッスンし、別の TCP 接続を確立した後に受信したメッセージを送信するポートと IPv6 アドレスをマップします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv6 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="delete-v4tov4"></a>v4tov4 の削除

プロキシサーバーは、サーバーがリッスンする IPv4 ポートとアドレスの一覧から IPv4 アドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv4 ポートを指定します。                                    |
| **リッスンアドレス** | 削除する IPv4 アドレスを指定します。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|   **プロトコール**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v4tov6"></a>v4tov6 の削除

プロキシサーバーは、サーバーがリッスンする IPv4 アドレスの一覧から IPv4 ポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv4 ポートを指定します。                                    |
| **リッスンアドレス** | 削除する IPv4 アドレスを指定します。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|   **プロトコール**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov4"></a>v6tov4 の削除

プロキシサーバーは、サーバーがリッスンする IPv6 アドレスの一覧から IPv6 ポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv6 ポートを指定します。                                    |
| **リッスンアドレス** | 削除する IPv6 アドレスを指定します。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|   **プロトコール**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov6"></a>v6tov6 の削除

プロキシサーバーは、サーバーがリッスンする IPv6 アドレスの一覧から IPv6 アドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv6 ポートを指定します。                                    |
| **リッスンアドレス** | 削除する IPv6 アドレスを指定します。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|   **プロトコール**    |                                      使用するプロトコルを指定します。                                      |

## <a name="reset"></a>reset

IPv6 構成の状態をリセットします。

### <a name="syntax"></a>構文

`reset`

## <a name="set-v4tov4"></a>v4tov4 の設定

**Add v4tov4**コマンドを使用して作成されたポートプロキシサーバー上の既存のエントリのパラメーター値を変更するか、ポートとアドレスのペアをマップする新しいエントリをリストに追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv4 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v4tov6"></a>v4tov6 の設定

**Add v4tov6**コマンドを使用して作成されたポートプロキシサーバー上の既存のエントリのパラメーター値を変更するか、ポートとアドレスのペアをマップする新しいエントリをリストに追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv4 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv6 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov4"></a>v6tov4 の設定

**Add v6tov4**コマンドを使用して作成されたポートプロキシサーバー上の既存のエントリのパラメーター値を変更するか、ポートとアドレスのペアをマップする新しいエントリをリストに追加します。

### <a name="syntax"></a>構文

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           リッスンするポート番号またはサービス名を使用して、IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv4 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。 |
|  **connectport**   |       接続先のポート番号またはサービス名を使用して、IPv4 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|    **プロトコール**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov6"></a>v6tov6 の設定

**Add v6tov6**コマンドを使用して作成されたポートプロキシサーバー上の既存のエントリのパラメーター値を変更するか、ポートとアドレスのペアをマップする新しいエントリをリストに追加します。

### <a name="syntax"></a>構文

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                            リッスンするポート番号またはサービス名を使用して、IPv6 ポートを指定します。                                                            |
| **connectaddress** | 接続先の IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスが指定されていない場合、既定値はローカルコンピューターです。  |
|  **connectport**   |        接続先のポート番号またはサービス名を使用して、IPv6 ポートを指定します。 **Connectport**が指定されていない場合、既定値はローカルコンピューターの**listenport が**の値になります。        |
| **リッスンアドレス**  | リッスンする IPv6 アドレスを指定します。 使用可能な値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名です。 アドレスを指定しない場合、既定値はローカルコンピューターになります。 |
|    **プロトコール**    |                                                                                   使用するプロトコルを指定します。                                                                                   |

## <a name="show-all"></a>すべての表示

V4tov4、v4tov6、v6tov4、および v6tov6 のポートとアドレスのペアを含む、すべてのポートプロキシパラメーターが表示されます。

### <a name="syntax"></a>構文

`show all`


## <a name="show-v4tov4"></a>v4tov4 の表示

V4tov4 のポートプロキシパラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 の表示

V4tov6 のポートプロキシパラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 の表示

V6tov4 のポートプロキシパラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 の表示

V6tov6 のポートプロキシパラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov6`

---
