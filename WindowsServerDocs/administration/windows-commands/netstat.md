---
title: netstat
description: Netstat コマンドのリファレンストピックでは、アクティブな TCP 接続、コンピューターがリッスンしているポート、イーサネット統計、IP ルーティングテーブル、IPv4 統計情報、および IPv6 統計が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60e2718f-93cc-4ceb-bf0e-58a6a6e4fc8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6eae779216724d82ef7ca05026bcfd9725e6ea35
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721545"
---
# <a name="netstat"></a>netstat

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アクティブな TCP 接続をコンピューターがリッスンしている、イーサネットの統計情報、IP ルーティング テーブル、IPv4 プロトコルの統計情報 (、IP、ICMP、TCP、および UDP)、および IPv6 の統計情報 (の IPv6、ICMPv6、IPv6 経由で TCP および UDP IPv6 プロトコル経由で) ポートを表示します。 パラメーターを指定せずに使用します。このコマンドは、アクティブな TCP 接続を表示します。

> [!IMPORTANT]
> このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。

## <a name="syntax"></a>構文

```
netstat [-a] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<interval>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| -a | すべてのアクティブな TCP 接続と、コンピューターがリッスンする TCP および UDP ポートが表示されます。 |
| -E | バイトと送受信されるパケットの数などのイーサネットの統計情報を表示します。 このパラメーターと組み合わせることができます **-s**します。 |
| -n | アクティブな TCP 接続の表示、ただし、アドレスし [ポート番号が数値で表される、名前を決定する試行が行われません。 |
| -o | アクティブな TCP 接続が表示され、接続ごとにプロセス ID (PID) が含まれています。 Windows タスク マネージャーで [プロセス] タブには、PID に基づくアプリケーションが表示されます。 このパラメーターと組み合わせることができます **-a**, 、**-n**, 、および **-p**します。 |
| -p`<Protocol>` | によって指定されたプロトコルの接続を示します *プロトコル*します。 ここで、 *プロトコル* tcp、udp、tcpv6、または udpv6 できます。 このパラメーターを使用した場合 **-s** プロトコルで統計を表示する *プロトコル* は、tcp、udp、icmp、ip、tcpv6、udpv6、icmpv6、または ipv6 します。 |
| -S | プロトコルによって統計が表示されます。 既定では、TCP、UDP、ICMP、および IP プロトコルに対して統計値が表示されます。 IPv6 プロトコルがインストールされている場合統計値が表示 (TCP)、IPv6、UDP 経由で、IPv6、ICMPv6、IPv6 プロトコルです。 **-P** パラメーターは、一連のプロトコルの指定を使用することができます。 |
| -r | IP ルーティング テーブルの内容を表示します。 これは、route print コマンドに相当します。 |
| `<interval>` | *間隔*(秒単位) ごとに、選択した情報を再指定します。 再表示を停止するには、CTRL + C キーを押します。 このパラメーターを省略した場合、このコマンドは選択した情報を1回だけ印刷します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- **Netstat**コマンドは、次の統計情報を提供します。

    | パラメーター | Description |
    | --------- | ----------- |
    | Mask | プロトコルの名前 (TCP または UDP)。 |
    | ローカルアドレス | ローカルコンピューターの IP アドレスと使用されているポート番号。 IP アドレスに対応するローカル コンピューターの名前とポートの名前が示すようにしない限り、 **-n** パラメーターを指定します。 ポートがまだ確立されていない場合、ポート番号は、アスタリスク (*) として表示されます。 |
    | 外部アドレス | ソケットが接続されているリモートコンピューターの IP アドレスとポート番号。 しない限り、IP アドレスとポートに対応する名前のとおり、 **-n** パラメーターを指定します。 ポートがまだ確立されていない場合、ポート番号は、アスタリスク (*) として表示されます。 |
    | State | 次のような TCP 接続の状態を示します。<ul><li>CLOSE_WAIT</li><li>CLOSED</li><li>定め</li><li>FIN_WAIT_1</li><li>FIN_WAIT_2</li><li>LAST_ACK</li><li>意見</li><li>SYN_RECEIVED</li><li>SYN_SEND</li><li>TIMED_WAIT</li></ul> |

### <a name="examples"></a>例

イーサネットの統計情報とプロトコルのすべての統計情報の両方を表示するには、次のように入力します。

```
netstat -e -s
```

TCP および UDP プロトコルのみの統計情報を表示するには、次のように入力します。

```
netstat -s -p tcp udp
```

表示するにはアクティブな TCP 接続とプロセス Id 5 秒ごとに次のように入力します。

```
netstat -o 5
```

アクティブな TCP を表示する接続とプロセス Id を数値の書式を入力します。

```
netstat -n -o
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
