---
title: netstat
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e2718f-93cc-4ceb-bf0e-58a6a6e4fc8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 666a15056e75cea37959d821c34288ffc2c6a6c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825673"
---
# <a name="netstat"></a>netstat

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アクティブな TCP 接続をコンピューターがリッスンしている、イーサネットの統計情報、IP ルーティング テーブル、IPv4 プロトコルの統計情報 (、IP、ICMP、TCP、および UDP)、および IPv6 の統計情報 (の IPv6、ICMPv6、IPv6 経由で TCP および UDP IPv6 プロトコル経由で) ポートを表示します。 パラメーターを指定せずに使用される **netstat** アクティブな TCP 接続が表示されます。 

## <a name="syntax"></a>構文
```
netstat [-a] [-e] [-n] [-o] [-p <Protocol>] [-r] [-s] [<Interval>]
```

### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|-a|すべてのアクティブな TCP 接続と、コンピューターがリッスンする TCP および UDP ポートが表示されます。|
|-e|バイトと送受信されるパケットの数などのイーサネットの統計情報を表示します。 このパラメーターと組み合わせることができます **-s**します。|
|-n|アクティブな TCP 接続の表示、ただし、アドレスし ポート番号が数値で表される、名前を決定する試行が行われません。|
|-o|アクティブな TCP 接続が表示され、接続ごとにプロセス ID (PID) が含まれています。 Windows タスク マネージャーで [プロセス] タブには、PID に基づくアプリケーションが表示されます。 このパラメーターと組み合わせることができます **-a**, 、**-n**, 、および **-p**します。|
|-p <Protocol>|によって指定されたプロトコルの接続を示します *プロトコル*します。 ここで、 *プロトコル* tcp、udp、tcpv6、または udpv6 できます。 このパラメーターを使用した場合 **-s** プロトコルで統計を表示する *プロトコル* は、tcp、udp、icmp、ip、tcpv6、udpv6、icmpv6、または ipv6 します。|
|-s|プロトコルによって統計が表示されます。 既定では、TCP、UDP、ICMP、および IP プロトコルに対して統計値が表示されます。 IPv6 プロトコルがインストールされている場合統計値が表示 (TCP)、IPv6、UDP 経由で、IPv6、ICMPv6、IPv6 プロトコルです。 **-P** パラメーターは、一連のプロトコルの指定を使用することができます。|
|-r|IP ルーティング テーブルの内容を表示します。 これは、route print コマンドに相当します。|
|<Interval>|選択した情報を再表示すべて *間隔* 秒です。 再表示を停止するには、CTRL + C キーを押します。 このパラメーターを省略すると、 **netstat** 選択されている情報を 1 回だけを出力します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
-   次のコマンドで使用されるパラメーターをハイフンで接頭辞必要があります (**-**)、スラッシュではなく (**/**)。
-   **netstat**次の統計情報を提供します。
    -   Proto プロトコル (TCP または UDP) の名前。
    -   ローカル アドレス、ローカル コンピューターと使用するポート番号の IP アドレスです。 IP アドレスに対応するローカル コンピューターの名前とポートの名前が示すようにしない限り、 **-n** パラメーターを指定します。 ポートがまだ確立されていない場合、ポート番号は、アスタリスク (*) として表示されます。
    -   外部アドレス、IP アドレスとポートの数、ソケットが接続されているリモート コンピューター。 しない限り、IP アドレスとポートに対応する名前のとおり、 **-n** パラメーターを指定します。 ポートがまだ確立されていない場合、ポート番号は、アスタリスク (*) として表示されます。
    -   (状態)TCP 接続の状態を示します。 可能な状態は次のとおりです。詳細については、TCP 接続の状態の CLOSE_WAIT 閉じた確立 FIN_WAIT_1 FIN_WAIT_2 LAST_ACK リッスン SYN_RECEIVED SYN_SEND timeD_WAIT は、Rfc 793 を参照してください。
-   このコマンドは、インターネット プロトコル (TCP/IP) プロトコルがネットワーク接続のネットワーク アダプターのプロパティでコンポーネントとしてインストールされている場合にのみ使用できます。

## <a name="BKMK_Examples"></a>例
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

## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
