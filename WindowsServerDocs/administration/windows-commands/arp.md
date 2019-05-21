---
title: arp
description: Windows コマンド」のトピック**arp** -表示し、IP アドレスとその解決の物理アドレスの格納に使用されるアドレス解決プロトコル (arp) キャッシュ内のエントリを変更します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5cd84269a5ac1a85d4b6cf359cc97f478a500c4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825983"
---
# <a name="arp"></a>arp

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示され、アドレス解決プロトコル (ARP) キャッシュ内のエントリを変更します。 ARP キャッシュには、IP アドレスおよび解決イーサネットまたはトークン リング物理アドレスの格納に使用される 1 つまたは複数のテーブルが含まれています。 イーサネットまたはトークン リング ネットワーク アダプターごとに、コンピューターにインストールされている別のテーブルがあります。 パラメーターを指定せずに使用される**arp**ヘルプ情報を表示します。
## <a name="syntax"></a>構文
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/a [<Inetaddr>] [/n <ifaceaddr>]|すべてのインターフェイスの現在の arp キャッシュ テーブルが表示されます。 /N パラメーターは大文字小文字を区別します。<br /><br />特定の IP アドレスの arp キャッシュ エントリを表示する使用**arp/a**で、 *Inetaddr*パラメーター、場所*Inetaddr* IP アドレスです。 場合*Inetaddr*が指定されていない、最初に適用可能なインターフェイスを使用します。<br /><br />Arp キャッシュ テーブルの特定のインターフェイスを表示するを使用して、**n/***ifaceaddr* パラメーターと組み合わせて、 **/a**パラメーター場所*ifaceaddr*は IP アドレスですインターフェイスに割り当てられます。|
|/g [<Inetaddr>] [/n <ifaceaddr>]|同じ **/a**します。|
|[/d <Inetaddr> [<ifaceaddr>]|特定の IP アドレスを持つエントリを削除します。 ここ*Inetaddr*は IP アドレスです。<br /><br />特定のインターフェイス用のテーブルにエントリを削除するには使用、 *ifaceaddr*パラメーター、 *ifaceaddr*インターフェイスに割り当てられている IP アドレスです。<br /><br />すべてのエントリを削除するには、アスタリスクを使用 (\*) の代わりにワイルドカード文字*Inetaddr*します。|
|/s <Inetaddr> <Etheraddr> [<ifaceaddr>]|IP アドレスを解決するための arp キャッシュに静的なエントリを追加します。 *Inetaddr*物理アドレスに*Etheraddr*します。<br /><br />特定のインターフェイスのテーブルには、静的 arp キャッシュ エントリを追加するには、使用、 *ifaceaddr*パラメーター、 *ifaceaddr*インターフェイスに割り当てられている IP アドレスです。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   IP アドレス*Inetaddr*と*ifaceaddr*ドット形式 10 進表記で表現されます。
-   物理アドレス*Etheraddr* 16 進表記で表され、(たとえば、00-AA-00-4F-2A-9C) をハイフンで区切られた 6 つのバイトで構成されます。
-   使用して追加のエントリ、 **/s**パラメーターは静的と arp キャッシュ期間内にはありません。 TCP/IP プロトコルを停止および開始する場合、エントリが削除されます。 永続的な静的 arp キャッシュ エントリを作成するには、適切な配置**arp**バッチ内のコマンド ファイルし、スケジュールされたタスクを使用して、起動時に、バッチ ファイルを実行します。
## <a name="BKMK_Examples"></a>例
すべてのインターフェイスの arp キャッシュ テーブルを表示するには、次のように入力します。
```
arp /a
```
10.0.0.99 の IP アドレスが割り当てられているインターフェイスの arp キャッシュ テーブルを表示するには、次のように入力します。
```
arp /a /n 10.0.0.99
```
IP アドレス 10.0.0.80 を 00-AA-00-4F-2A-9C 物理アドレスに解決される静的 arp キャッシュ エントリを追加するには、次のように入力します。
```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
