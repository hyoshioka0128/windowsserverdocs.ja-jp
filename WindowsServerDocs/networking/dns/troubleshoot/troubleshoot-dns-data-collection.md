---
title: ドメインネームシステム (DNS) に関する問題のトラブルシューティング
description: この記事では、DNS の問題が発生したときにデータを収集する方法について説明します。
manager: willchen
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: a86b1f34c3b21f5bcde710e2a98323492ea51b62
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68917779"
---
# <a name="troubleshooting-domain-name-system-dns-issues"></a>ドメインネームシステム (DNS) に関する問題のトラブルシューティング
 
ドメイン名解決の問題は、クライアント側とサーバー側の問題に分けることができます。 一般に、サーバー側で問題が発生していることが明らかな場合を除き、クライアント側のトラブルシューティングから始めることをお勧めします。

- [DNS クライアントのトラブルシューティング](troubleshoot-dns-client.md)

- [DNS サーバーのトラブルシューティング](troubleshoot-dns-server.md)
 
## <a name="data-collection"></a>データ収集
 
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