---
title: 新機能 Windows Server での DNS クライアントの新機能
description: このトピックでは、Windows Server および Windows 10 での DNS クライアントの新機能の概要を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 34b1a64465e217fbd7e6b3ae55e89832a7a4e48c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860563"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Windows Server 2016 の DNS クライアントの新機能

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Windows 10 および Windows Server 2016 以降のバージョンのこれらのオペレーティング システムで追加または変更は、ドメイン ネーム システム (DNS) クライアントの機能について説明します。
  
## <a name="updates-to-dns-client"></a>DNS クライアントの更新

**DNS クライアント サービスのバインド**:Windows 10 では、DNS クライアント サービスは、1 つ以上のネットワーク インターフェイスを持つコンピューターのサポートの強化を提供します。 マルチホーム コンピューターでは、DNS 解決は、次の方法で最適化します。  
  
-   特定のインターフェイスで構成されている DNS サーバーを使用するには DNS クエリを解決する、DNS クライアント サービスは、DNS クエリを送信する前に、このインターフェイスにバインドされます。  
  
    特定のインターフェイス、クライアントは、DNS へのバインドを明確にには、この DNS クライアントとの通信を最適化するためにアプリケーションを有効にするネットワーク インターフェイス、インターフェイスの名前解決が発生するを指定します。  
  
-   名前解決ポリシー テーブル (NRPT) からのグループ ポリシー設定で使用される DNS サーバーが指定されると、DNS クライアント サービスは特定のインターフェイスをバインドしません。  
  
> [!NOTE]  
> Windows 10 での DNS クライアント サービスへの変更は、Windows Server 2016 およびそれ以降のバージョンを実行しているコンピューターにもできます。  
  
## <a name="see-also"></a>関連項目  
  
-   [新機能 Windows Server 2016 での DNS サーバーの新機能](What-s-New-in-DNS-Server.md)  
  

