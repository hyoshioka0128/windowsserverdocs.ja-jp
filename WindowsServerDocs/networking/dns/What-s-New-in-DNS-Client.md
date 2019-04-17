---
title: Windows Server での DNS クライアントの新機能
description: このトピックでは、Windows Server および Windows 10 での DNS クライアントの新機能の概要
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: defe88fe2a1e4f5393be4d5d5938d9f5bfbfb5d6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Windows Server 2016 での DNS クライアントの新機能

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows 10 と Windows Server 2016 とこれらのオペレーティング システム以降のバージョンで追加または変更は、ドメイン ネーム システム (DNS) クライアントの機能について説明します。
  
## <a name="updates-to-dns-client"></a>DNS クライアントの更新

**DNS クライアント サービスのバインド**: Windows 10 では、DNS クライアント サービスは、1 つ以上のネットワーク インターフェイスを備えたコンピューターの拡張のサポートを提供します。 マルチホーム コンピューターでは、DNS 解決は、次の方法で最適化します。  
  
-   使用する場合、特定のインターフェイスで構成されている DNS サーバーは DNS クエリを解決するのには、DNS クライアント サービスは、DNS クエリを送信する前に、このインターフェイスにバインドされます。  
  
    明確に DNS クライアントは、特定のインターフェイスにバインドすることでは、ネットワーク インターフェイスを有効にするとアプリケーションには、この DNS クライアントとの通信を最適化するために、名前解決が発生するインターフェイスを指定します。  
  
-   名前解決ポリシー テーブル (NRPT) からのグループ ポリシー設定で使用される DNS サーバーを指定すると場合、DNS クライアント サービスが特定のインターフェイスにバインドできません。  
  
> [!NOTE]  
> Windows 10 では、DNS クライアント サービスへの変更は、Windows Server 2016 とそれ以降のバージョンを実行しているコンピューターにもできます。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server 2016 の DNS サーバーの新機能](What-s-New-in-DNS-Server.md)  
  

