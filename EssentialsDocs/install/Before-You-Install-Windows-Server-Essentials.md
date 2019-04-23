---
title: Windows Server Essentials をインストールする前に
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d0893bd-e2b7-4494-9537-02b1cbbcd57a
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e7eb1b7bed780b41f1a87589add4ab015f41624a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828723"
---
# <a name="before-you-install-windows-server-essentials"></a>Windows Server Essentials をインストールする前に

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_BeforeYouBegin"></a> Windows Server Essentials のインストールを開始する前に、次のタスクを実行します。  

-   **コンピューターが最小ハードウェア要件を満たしていることを確認します**。 これは、追加のハードウェアが必要なかどうかを決定する、ハードウェアのドライバーは Windows Server Essentials でサポートされていることを確認が含まれます。 詳細については、次を参照してください。 [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)します。   

  
    > [!IMPORTANT]
    >  既存のコンピューターで Windows Server Essentials をインストールする前に完全にフォーマットし、既存のコンピューターのハード ディスク パーティションに再分割することお勧めします。 ハード ディスクをフォーマットし、パーティションを再分割することで、ハード ディスクに隠しパーティションが残る可能性がなくなります。  
  
-   **ネットワークを準備**に Windows Server Essentials をインストールするネットワークを準備するには、次の操作を行います。  
    
  
    -   **クライアント コンピューターにオペレーティング システムをアップグレード**Windows Server Essentials は、次のオペレーティング システムをサポートしています。Windows 8、Windows 7、Windows 10、および Macintosh OS X Lion 以上。 これらのオペレーティング システムは、ローカル ネットワークに対して必要なセキュリティ機能、信頼性、パフォーマンスを備えています。  
  
    -   **ルーターを構成する** ルーターが次のように構成されていることを確認します。  
  
        -   ルーターで UPnP フレームワークが有効になっています。  
  
        -   LAN の動的ホスト構成プロトコル (DHCP) サーバー サービスを有効または無効にできます。  Windows Server Essentials では、DHCP がサーバーとルーターの両方で実行されていないことをによりしますか。 DHCP がルーターで有効な場合、DHCP は無効、サーバーのインストール中にです。  
  
        -   ルーターの外部インターフェイス用の IP アドレスがあります。これは、インターネット サービス プロバイダー (ISP) から提供されています。 IP アドレスが ISP で DHCP サーバー サービスによって動的に割り当てられているか、ルーター管理コンソールを使用して静的 IP アドレスを手動で構成する必要があります。  
  
        -   インターネット接続でユーザー名とパスワードが要求される場合 (PPPoE (Point to Point Protocol over Ethernet) とも呼びます)、デバイスが UPnP フレームワークをサポートしているとしても、ルーター上でこれらの設定が構成されます。  
  
        -   ルーターが LAN とインターネットに接続されており、電源がオンで、正常に機能しています。  
  
     ルーターが UPnP フレームワークをサポートしない場合、またはインストール中にルーターを構成できない場合、ネットワークの設定を使って手動でルーターを構成する必要があります。 次のポートが開いていて、移行先サーバーの IP アドレスに接続されていることを確認してください。  
  
    |[ポート番号]|アプリケーション|  
    |-----------------|-----------------|  
    |ポート 80|HTTP Web トラフィック|  
    |ポート 443|HTTPS Web トラフィック|  
  

-   **Windows Server Essentials のリリースに関するドキュメントを読み取る**します。 リリース ノートには、正しくインストールして、Windows Server Essentials を構成する重要な可能性のある最新の情報が含まれています。 を表示または印刷版のドキュメントを参照してください。 [Release Documentation for Windows Server Essentials](../get-started/release-notes.md)します。  
  
## <a name="see-also"></a>関連項目  
  
-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)

