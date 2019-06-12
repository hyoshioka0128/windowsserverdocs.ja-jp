---
title: インターフェイスのプロキシ用の Netsh コマンド
description: IPv4 と IPv6 のネットワークとアプリケーション間のプロキシとして機能するには、netsh インターフェイスのプロキシ コマンドを使用します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 8ac4f8e7cd0aed5a81e89672354622dd81afce2a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446180"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh interface portproxy コマンド

使用して、 **netsh インターフェイス プロキシ**IPv4 と IPv6 のネットワークとアプリケーション間のプロキシとして機能するコマンド。 これらのコマンドは、次のようにプロキシ サービスを確立するために使用できます。

-   IPv4 構成のコンピューターとアプリケーションの他のコンピューターの IPv4 構成とアプリケーションに送信されるメッセージ。

-   IPv4 構成のコンピューターとアプリケーション IPv6 構成を送信したコンピューターおよびアプリケーションをメッセージします。

-   IPv6 構成のコンピューターとアプリケーション IPv4 構成を送信したコンピューターおよびアプリケーションをメッセージします。

-   IPv6 構成のコンピューターとアプリケーションの他の IPv6 構成のコンピューターとアプリケーションに送信されるメッセージ。

各コマンドで始まらなければなりませんバッチ ファイル、またはこれらのコマンドを使用してスクリプトを記述するときに**netsh インターフェイス プロキシ**します。 使用する場合など、 **delete v4tov6** IPv4 ポートとアドレスをサーバーがリッスンする IPv4 アドレスの一覧から削除するプロキシ サーバーをバッチ ファイルまたはスクリプトは、次の構文を使用する必要がありますを指定するコマンド。

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

Netsh インターフェイスのプロキシ コマンドは次のとおりです。

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

-   [すべて表示します。](#show-all)

-   [show v4tov4](#show-v4tov4)

-   [show v4tov6](#show-v4tov6)

-   [show v6tov4](#show-v6tov4)

-   [show v6tov6](#show-v6tov6)


## <a name="add-v4tov4"></a>v4tov4 を追加します。

プロキシ サーバーは、ポートと IPv4 アドレスの別の TCP 接続を確立した後に受信したメッセージを送信する特定のポートと IPv4 アドレスとマップに送信されるメッセージをリッスンします。

### <a name="syntax"></a>構文

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv4 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv4 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンに使用する IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v4tov6"></a>v4tov6 を追加します。

プロキシ サーバーは、ポートと IPv6 アドレスの別の TCP 接続を確立した後に受信したメッセージを送信する特定のポートと IPv4 アドレス、およびマップに送信されるメッセージをリッスンします。

### <a name="syntax"></a>構文

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv4 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv6 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov4"></a>v6tov4 を追加します。

プロキシ サーバーは、特定のポートと IPv6 アドレス、およびポートと IPv4 アドレスの別の TCP 接続を確立した後に受信したメッセージを送信するマップに送信されるメッセージをリッスンします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv6 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv4 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="add-v6tov6"></a>v6tov6 を追加します。

プロキシ サーバーは、特定のポートと IPv6 アドレス、およびマップを別の TCP 接続を確立した後に受信したメッセージを送信するポートと IPv6 のアドレスに送信されるメッセージをリッスンします。

### <a name="syntax"></a>構文

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv6 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv6 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="delete-v4tov4"></a>v4tov4 を削除します。

プロキシ サーバーは、IPv4 アドレスを IPv4 ポートと、サーバーがリッスンするアドレスの一覧から削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv4 ポートを指定します。                                    |
| **リッスン アドレス** | 削除する IPv4 アドレスを指定します。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|   **プロトコル**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v4tov6"></a>v4tov6 を削除します。

プロキシ サーバーは、サーバーがリッスンする IPv4 アドレスの一覧から IPv4 ポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv4 ポートを指定します。                                    |
| **リッスン アドレス** | 削除する IPv4 アドレスを指定します。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|   **プロトコル**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov4"></a>v6tov4 を削除します。

プロキシ サーバーは、サーバーがリッスン対象の IPv6 アドレスの一覧から、IPv6 のポートとアドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv6 ポートを指定します。                                    |
| **リッスン アドレス** | 削除する IPv6 アドレスを指定します。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|   **プロトコル**    |                                      使用するプロトコルを指定します。                                      |

## <a name="delete-v6tov6"></a>v6tov6 を削除します。

プロキシ サーバーは、サーバーがリッスン対象の IPv6 アドレスの一覧から、IPv6 アドレスを削除します。

### <a name="syntax"></a>構文

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport が**   |                                    削除する IPv6 ポートを指定します。                                    |
| **リッスン アドレス** | 削除する IPv6 アドレスを指定します。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|   **プロトコル**    |                                      使用するプロトコルを指定します。                                      |

## <a name="reset"></a>reset

IPv6 構成の状態をリセットします。

### <a name="syntax"></a>構文

`reset`

## <a name="set-v4tov4"></a>セット v4tov4

作成されたプロキシ サーバー上の既存のエントリのパラメーター値を変更、 **add v4tov4**コマンド、またはあるマップ ポート/アドレスのペアの一覧に新しいエントリを追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv4 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv4 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンに使用する IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v4tov6"></a>set v4tov6

作成されたプロキシ サーバー上の既存のエントリのパラメーター値を変更、 **add v4tov6**コマンド、またはあるマップ ポート/アドレスのペアの一覧に新しいエントリを追加します。

### <a name="syntax"></a>構文

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv4 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv6 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov4"></a>セット v6tov4

作成されたプロキシ サーバー上の既存のエントリのパラメーター値を変更、 **add v6tov4**コマンド、またはあるマップ ポート/アドレスのペアの一覧に新しいエントリを追加します。

### <a name="syntax"></a>構文

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                           IPv6 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv4 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。 |
|  **connectport**   |       IPv4 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|    **プロトコル**    |                                                                                  使用するプロトコルを指定します。                                                                                   |

## <a name="set-v6tov6"></a>セット v6tov6

作成されたプロキシ サーバー上の既存のエントリのパラメーター値を変更、 **add v6tov6**コマンド、またはあるマップ ポート/アドレスのペアの一覧に新しいエントリを追加します。

### <a name="syntax"></a>構文

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>パラメーター

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport が**   |                                                            IPv6 ポートをポート番号またはサービスを指定します。 名前、リッスンに使用します。                                                            |
| **connectaddress** | 接続先となる、IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスが指定されていない場合は、既定では、ローカル コンピューターです。  |
|  **connectport**   |        IPv6 ポートをポート番号またはサービスを指定します。 接続先の名前。 場合**connectport**が指定されていない、既定の値は**listenport が**ローカル コンピューター上です。        |
| **リッスン アドレス**  | リッスンする IPv6 アドレスを指定します。 指定できる値は、IP アドレス、コンピューターの NetBIOS 名、またはコンピューターの DNS 名には。 アドレスを指定しない場合は、既定では、ローカル コンピューターです。 |
|    **プロトコル**    |                                                                                   使用するプロトコルを指定します。                                                                                   |

## <a name="show-all"></a>すべての表示

V4tov4、v4tov6、v6tov4、および v6tov6 のポートとアドレスのペアを含む、すべてのプロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show all`


## <a name="show-v4tov4"></a>v4tov4 を表示します。

V4tov4 プロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 を表示します。

V4tov6 プロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 を表示します。

V6tov4 プロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 を表示します。

V6tov6 プロキシ パラメーターを表示します。

### <a name="syntax"></a>構文

`show v6tov6`

---
