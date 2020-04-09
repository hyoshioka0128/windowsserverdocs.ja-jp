---
title: arp
description: Windows コマンドの**arp**のトピックでは、IP アドレスとその解決済みの物理アドレスを格納するために使用するアドレス解決プロトコル (arp) キャッシュのエントリを表示および変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 827e96eb-1945-483f-980f-714703456f7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 289ab87c99512c7c34154d4b85d541db82ab296b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851315"
---
# <a name="arp"></a>arp

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

アドレス解決プロトコル (ARP) キャッシュのエントリを表示および変更します。 ARP キャッシュには、IP アドレスとその解決済みのイーサネットまたはトークンリングの物理アドレスを格納するために使用される1つ以上のテーブルが含まれています。 コンピューターにインストールされているイーサネットまたはトークンリングネットワークアダプターごとに個別のテーブルがあります。 パラメーターを指定せずに使用します。 **arp**はヘルプ情報を表示します。

## <a name="syntax"></a>構文
```
arp [/a [<Inetaddr>] [/n <ifaceaddr>]] [/g [<Inetaddr>] [-n <ifaceaddr>]] [/d <Inetaddr> [<ifaceaddr>]] [/s <Inetaddr> <Etheraddr> [<ifaceaddr>]]
```
#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `/a [<Inetaddr>] [/n <ifaceaddr>]` | すべてのインターフェイスの現在の arp キャッシュテーブルを表示します。 `/n` パラメーターでは、大文字と小文字が区別されます。 特定の IP アドレスの arp キャッシュエントリを表示するには、 *Inetaddr*パラメーターで**arp/a**を使用します。ここで、 *Inetaddr*は IP アドレスです。 場合*Inetaddr*が指定されていない、最初の該当するインターフェイスが使用されます。 特定のインターフェイスの arp キャッシュテーブルを表示するには、 **/a**パラメーターと共に * */n * * * ifaceaddr*パラメーターを使用します。 *ifaceaddr*は、インターフェイスに割り当てられた IP アドレスです。 |
| `/g [<Inetaddr>] [/n <ifaceaddr> `] | **/A**と同じです。 |
|`[/d <Inetaddr> [<ifaceaddr>]` | 特定の IP アドレスを持つエントリを削除します。ここで、 *Inetaddr*は ip アドレスです。 特定のインターフェイスのテーブル内のエントリを削除するには、 *ifaceaddr*パラメーターを使用します。 *ifaceaddr*は、インターフェイスに割り当てられた IP アドレスです。 すべてのエントリを削除するには、 *Inetaddr*の代わりにアスタリスク (\*) ワイルドカード文字を使用します。 |
|`/s <Inetaddr> <Etheraddr> [<ifaceaddr>]` | IP アドレス*Inetaddr*を物理アドレス*Etheraddr*に解決する静的エントリを arp キャッシュに追加します。 特定のインターフェイスの静的 arp キャッシュエントリをテーブルに追加するには、 *ifaceaddr*パラメーターを使用します。 *ifaceaddr*は、インターフェイスに割り当てられた IP アドレスです。 |
|`/?`| コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント
- *Inetaddr*と*ifaceaddr*の IP アドレスは、ドット形式の10進表記で表されます。
- *Etheraddr*の物理アドレスは、16進表記で表され、ハイフンで区切られた6バイトで構成されます (たとえば、00-AA-00-4F-9C)。

- **/S**パラメーターを使用して追加されたエントリは静的であり、arp キャッシュのタイムアウトはありません。 TCP/IP プロトコルが停止して開始されると、エントリは削除されます。 永続的な静的 arp キャッシュエントリを作成するには、適切な**arp**コマンドをバッチファイルに配置し、スケジュールされたタスクを使用して起動時にバッチファイルを実行します。

## <a name="examples"></a><a name=BKMK_Examples></a>例

すべてのインターフェイスの arp キャッシュテーブルを表示するには、次のように入力します。

```
arp /a
```

IP アドレス10.0.0.99 が割り当てられているインターフェイスの arp キャッシュテーブルを表示するには、次のように入力します。

```
arp /a /n 10.0.0.99
```

IP アドレス10.0.0.80 を解決する静的 arp キャッシュエントリを物理アドレス 00-AA-00-4F-9C に追加するには、次のように入力します。

```
arp /s 10.0.0.80 00-AA-00-4F-2A-9C 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
