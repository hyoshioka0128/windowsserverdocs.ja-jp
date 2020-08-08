---
title: AD FS のトラブルシューティング-DNS 解決
description: このドキュメントでは、AD FS の DNS の側面をトラブルシューティングする方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: b0134478ce0a4e91d6e33d5a0845a2be5df53d3f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954178"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS のトラブルシューティング-DNS
AD FS が動作していないか、応答していないかを確認する最初の項目の1つは、DNS 名の解決です。  これらは、AD FS サーバーまたは WAP サーバーがネットワーク上で検出されているかどうかを判断するための基本的なテストです。  内部ユーザーの場合、これらのテストは AD FS サーバー (STS) に解決される必要があります。    外部ユーザーの場合、これらのテストは WAP サーバーに解決される必要があります。

このドキュメントの残りの部分では、コマンドラインツールを使用して、名前解決のクイックチェックを実行する方法について説明します。

## <a name="ping-test"></a>Ping テスト
インターネット制御メッセージ プロトコル (ICMP) エコー要求メッセージを送信することによって IP レベルで別の TCP/IP コンピューターへの接続を確認します。 対応するエコー応答メッセージの受信は、ラウンドト リップ時間と共に表示されます。  詳細については、「 [Ping](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961503(v=ws.11))」を参照してください。


>[!NOTE]
>組織によっては、サーバー上でこのポートがブロックされ、**要求がタイムアウト**になる場合があることに注意してください。

### <a name="to-use-a-ping-test"></a>PING テストを使用するには
1.  コマンド プロンプトを開きます
2. 「PING <name of adfs server> a」と入力します。 例: PING sts.contoso.com
3. サーバーからの応答が表示されます。

![ping](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>NSLookup
ドメインネームシステム (DNS) インフラストラクチャの診断に使用できる情報を表示します。  詳細については、「 [NSLookup](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc725991(v=ws.11))」を参照してください。

### <a name="to-use-a-nslookup"></a>NSLookup を使用するには
1.  コマンド プロンプトを開きます
2. 「PING <name of adfs server> a」と入力します。 例: nslookup sts.contoso.com
3. NSLookup サーバーの dns 情報が表示されます。 ![](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
インクリメンタルに増加する Time to Live (TTL) フィールド値を使用して、送信先にインターネット制御メッセージプロトコル (ICMP) エコー要求または ICMPv6 メッセージを送信することによって、宛先へのパスを決定します。   詳細については、「 [Tracert](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff961507(v=ws.11))」を参照してください。


### <a name="to-use-tracert"></a>Tracert を使用するには
1.  コマンド プロンプトを開きます
2. 「Tracert <name of adfs server> a」と入力します。 例: tracert sts.contoso.com
3. サーバー Tracert への接続先のパスが表示されます。 ![](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
