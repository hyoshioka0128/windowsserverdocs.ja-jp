---
title: Windows Server での DNS クライアントの新機能
description: このトピックでは、Windows Server と Windows 10 の DNS クライアントの新機能の概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 6edaba84-4595-4fd8-95d7-64d4d975a38a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 696ea0b499a4132d630cc0cda15a1d7efdac37a8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356063"
---
# <a name="whats-new-in-dns-client-in-windows-server-2016"></a>Windows Server 2016 の DNS クライアントの新機能

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows 10 および Windows Server 2016 以降のバージョンのオペレーティングシステムで追加または変更されたドメインネームシステム (DNS) クライアントの機能について説明します。
  
## <a name="updates-to-dns-client"></a>DNS クライアントの更新プログラム

**DNS クライアントサービスのバインド**:Windows 10 では、DNS クライアントサービスは、複数のネットワークインターフェイスを持つコンピューターの拡張サポートを提供します。 マルチホームコンピューターの場合、DNS 解決は次の方法で最適化されます。  
  
-   特定のインターフェイスで構成されている DNS サーバーを使用して DNS クエリを解決すると、dns クライアントサービスは、dns クエリを送信する前にこのインターフェイスにバインドします。  
  
    DNS クライアントは、特定のインターフェイスにバインドすることによって、名前解決が行われるインターフェイスを明確に指定できます。これにより、アプリケーションはこのネットワークインターフェイス経由で DNS クライアントとの通信を最適化できます。  
  
-   使用する DNS サーバーが名前解決ポリシーテーブル (NRPT) のグループポリシー設定によって指定されている場合、DNS クライアントサービスは特定のインターフェイスにバインドされません。  
  
> [!NOTE]  
> Windows 10 の DNS クライアントサービスに加えられた変更は、Windows Server 2016 以降のバージョンを実行しているコンピューターにも存在します。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server 2016 の DNS サーバーの新機能](What-s-New-in-DNS-Server.md)  
  

