---
title: AD FS のトラブルシューティング - DNS 解決
description: このドキュメントは、AD FS の DNS の側面をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e0065feac4241b617b8b13c6867d5dc36634bd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815903"
---
# <a name="ad-fs-troubleshooting---dns"></a>AD FS のトラブルシューティング - DNS 
最初に AD FS は操作、または応答していない場合、確認することの 1 つは、DNS 名前解決です。  これらは、基本的なテストのかどうか、AD FS サーバーまたは WAP サーバーが見つかったネットワーク上の決定です。  内部ユーザーは、これらのテストは、AD FS サーバー (STS) に解決する必要があります。    外部のユーザーに対してこれらのテストは、WAP サーバーに解決する必要があります。

このドキュメントの残りの部分では、コマンド ライン ツールを使用していくつかの簡単な名前解決チェックを行う方法を示します。

## <a name="ping-test"></a>Ping テスト
インターネット制御メッセージ プロトコル (ICMP) エコー要求メッセージを送信することによって IP レベルで別の TCP/IP コンピューターへの接続を確認します。 対応するエコー応答メッセージの受信は、ラウンドト リップ時間と共に表示されます。  詳細については、次を参照してください。 [Ping](https://technet.microsoft.com/library/ff961503.aspx)します。


>[!NOTE]
>組織によっては、サーバー上のこのポートをブロックしてしまうこと注意してください、**要求がタイムアウト**応答します。

### <a name="to-use-a-ping-test"></a>PING テストを使用するには
1.  コマンド プロンプトを開く
2. PING の入力<name of adfs server>をします。 以下に例を示します。PING sts.contoso.com
3. サーバーからの応答を表示する必要があります。

![Ping](media/ad-fs-tshoot-dns/dns1.png)

## <a name="nslookup"></a>NSLookup
ドメイン ネーム システム (DNS) インフラストラクチャの診断に使用できる情報を表示します。  詳細については、次を参照してください。 [NSLookup](https://technet.microsoft.com/library/cc725991.aspx)します。

### <a name="to-use-a-nslookup"></a>NSLookup を使用するには
1.  コマンド プロンプトを開く
2. PING の入力<name of adfs server>をします。 例: nslookup sts.contoso.com
3. サーバーの dns 情報を表示する必要があります![NSLookup](media/ad-fs-tshoot-dns/dns2.png)

## <a name="tracert"></a>Tracert
送信インターネット コントロール メッセージ プロトコル (ICMP) エコー要求メッセージまたは Live (TTL) フィールドの値に時間を段階的に増加による変換先を ICMPv6 メッセージで、先に使用されるパスを決定します。   詳細については、次を参照してください。 [Tracert](https://technet.microsoft.com/library/ff961507.aspx)します。


### <a name="to-use-tracert"></a>Tracert を使用するには
1.  コマンド プロンプトを開く
2. 入力 tracert<name of adfs server>をします。 例: tracert sts.contoso.com
3. サーバーに到達するために使用するデプロイ先のパスが表示![Tracert](media/ad-fs-tshoot-dns/dns3.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)