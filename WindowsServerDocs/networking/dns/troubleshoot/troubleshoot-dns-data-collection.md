---
title: ドメインネームシステム (DNS) に関する問題のトラブルシューティング
description: この記事では、DNS の問題が発生したときにデータを収集する方法について説明します。
manager: dcscontentpm
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 04bfbfbd2957aec21da966a48feca8d7f160a29c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860045"
---
# <a name="troubleshooting-domain-name-system-dns-issues"></a>ドメインネームシステム (DNS) に関する問題のトラブルシューティング
 
ドメイン名解決の問題は、クライアント側とサーバー側の問題に分けることができます。 一般に、サーバー側で問題が発生していることが明らかな場合を除き、クライアント側のトラブルシューティングから始めることをお勧めします。

- [DNS クライアントのトラブルシューティング](troubleshoot-dns-client.md)

- [DNS サーバーのトラブルシューティング](troubleshoot-dns-server.md)
 
## <a name="data-collection"></a>データ コレクション
 
問題が発生したときに、クライアント側とサーバー側の両方で同時にデータを収集することをお勧めします。 ただし、実際の問題によっては、DNS クライアントまたは DNS サーバーの1つのデータセットでコレクションを開始できます。
 
影響を受けるクライアントとその構成済みの DNS サーバーから Windows ネットワーク診断を収集するには、次の手順を実行します。

1. クライアントとサーバーでネットワークキャプチャを開始します。

   ```cmd
   netsh trace start capture=yes tracefile=c:\%computername%_nettrace.etl
   ```

2. 次のコマンドを実行して、DNS クライアントの DNS キャッシュをクリアします。

   ```cmd
   ipconfig /flushdns
   ```

3. 問題を再現します。

4. トレースを停止して保存します。

   ```cmd
   netsh trace stop
   ```

5. 各コンピューターから Nettrace .cab ファイルを保存します。 この情報は、Microsoft サポートに連絡するときに役立ちます。