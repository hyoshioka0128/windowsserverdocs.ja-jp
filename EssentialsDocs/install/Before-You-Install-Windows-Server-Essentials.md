---
title: "Windows Server Essentials をインストールする前に"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="before-you-install-windows-server-essentials"></a>Windows Server Essentials をインストールする前に

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_BeforeYouBegin"></a>Windows Server Essentials のインストールを開始する前に、次のタスクを実行します。  

-   **コンピューターがハードウェアの最小要件を満たしていることを確認**します。 これには、追加のハードウェアが必要なかどうかを決定して、ハードウェアのドライバーが Windows Server Essentials でサポートされていることを確認が含まれます。 詳細については、次を参照してください。[Windows Server Essentials のシステム要件](../get-started/system-requirements.md)します。   

  
    > [!IMPORTANT]
    >  既存のコンピューターで Windows Server Essentials をインストールする前に、完全にフォーマットし、パーティションの既存のコンピューターのハード _ ディスクを再作成することお勧めします。 書式設定して、ハード ディスク パーティションの再作成、ハード_ディスクに隠しパーティションが残っている可能性が削除されます。  
  
-   **ネットワークを準備**に Windows Server Essentials をインストールするネットワークを準備するには、次の操作します。  
    
  
    -   **クライアント コンピューターにオペレーティング システムをアップグレード**Windows Server Essentials は、次のオペレーティング システムをサポートしています。Windows 8、Windows 7、Windows 10、および Macintosh OS X Lion 以上。 これらのオペレーティング システムでは、必要なセキュリティ機能、信頼性、パフォーマンス、およびローカル ネットワークの機能を提供します。  
  
    -   **ルーターを構成**ルーターが次のように構成されていることを確認します。  
  
        -   ルーターで UPnP フレームワークを有効にします。  
  
        -   LAN の動的ホスト構成プロトコル (DHCP) サーバー サービスを有効または無効になっていることができます。  Windows Server Essentials では、DHCP がサーバーとルーターの両方で実行されていないことを確実ですか。 DHCP がルーターで有効な場合、DHCP は無効で、サーバーのインストール中にです。  
  
        -   インターネット サービス プロバイダー (ISP) によって提供される、ルーターの外部インターフェイスの IP アドレスがあります。 IP アドレスを ISP で DHCP サーバー サービスによって動的に割り当てることができます、またはルーター管理コンソールを使用して静的 IP アドレスを手動で構成する必要があります。  
  
        -   ユーザー名とパスワード、Point-to-Point Protocol over Ethernet (PPPoE) とも呼ばれますが、インターネット接続に必要とする場合は、デバイスが UPnP フレームワークをサポートしている場合でも、ルーターでこれらの設定が構成されます。  
  
        -   ルーターが LAN とインターネットに接続されているが入っていること、および適切に機能しています。  
  
     ルーターが UPnP フレームワークをサポートしていない場合、またはインストール中にルーターを構成できない場合は、する必要があります手動で構成設定で、ネットワークのします。 次のポートが開いているしは、移行先サーバーの IP アドレスに転送することを確認します。  
  
    |ポート番号|アプリケーション|  
    |-----------------|-----------------|  
    |ポート 80|HTTP Web トラフィック|  
    |ポート 443|HTTPS Web トラフィック|  
  

-   **Windows Server Essentials のリリース ノートを読み**します。 リリース ノートには、正しくインストールし、Windows Server Essentials の構成に重要な最新の情報が含まれています。 表示または印刷するリリース ノートには、次を参照してください。[リリース ドキュメント for Windows Server Essentials](../get-started/release-notes.md)します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)

