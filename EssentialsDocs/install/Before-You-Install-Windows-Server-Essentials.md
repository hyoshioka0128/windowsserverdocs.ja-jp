---
title: Windows Server Essentials をインストールする前に
description: Windows Server Essentials の使用方法について説明します。
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
ms.openlocfilehash: 4629c0ba04cc7ee617a2fc6b6a73a19b9e45ada8
ms.sourcegitcommit: 3d76683718ec6f38613f552f518ebfc6a5db5401
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74829549"
---
# <a name="before-you-install-windows-server-essentials"></a>Windows Server Essentials をインストールする前に

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_BeforeYouBegin"></a>Windows Server Essentials のインストールを開始する前に、次のタスクを実行します。  

-   **コンピューターが最小ハードウェア要件を満たしていることを確認します**。 これには、追加のハードウェアが必要かどうかの判断や、ハードウェアのドライバーが Windows Server Essentials でサポートされているかどうかの確認が含まれます。 詳細については、「 [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)」を参照してください。   

> [!IMPORTANT]
> Windows Server Essentials を既存のコンピューターにインストールする前に、既存のコンピューターのハードディスクを完全にフォーマットし、パーティションを再作成することをお勧めします。 ハード ディスクをフォーマットし、パーティションを再分割することで、ハード ディスクに隠しパーティションが残る可能性がなくなります。  

- **ネットワークを準備する**Windows Server Essentials をインストールするためにネットワークを準備するには、次の手順を実行します。  


  - **クライアントコンピューターのオペレーティングシステムのアップグレード** Windows Server Essentials は、Windows 8、Windows 7、Windows 10、Macintosh OS X ライオン以上のオペレーティングシステムをサポートしています。 これらのオペレーティング システムは、ローカル ネットワークに対して必要なセキュリティ機能、信頼性、パフォーマンスを備えています。  

  - **ルーターを構成する** ルーターが次のように構成されていることを確認します。  

    -   ルーターで UPnP フレームワークが有効になっています。  

    -   LAN の動的ホスト構成プロトコル (DHCP) サーバー サービスを有効または無効にできます。  Windows Server Essentials では、DHCP がサーバーとルーターの両方で実行されていないことが保証されますか。 ルーターで DHCP が有効になっていると、インストール中に DHCP がサーバーで有効になりません。  

    -   ルーターの外部インターフェイス用の IP アドレスがあります。これは、インターネット サービス プロバイダー (ISP) から提供されています。 IP アドレスが ISP で DHCP サーバー サービスによって動的に割り当てられているか、ルーター管理コンソールを使用して静的 IP アドレスを手動で構成する必要があります。  

    -   インターネット接続でユーザー名とパスワードが要求される場合 (PPPoE (Point to Point Protocol over Ethernet) とも呼びます)、デバイスが UPnP フレームワークをサポートしているとしても、ルーター上でこれらの設定が構成されます。  

    -   ルーターが LAN とインターネットに接続されており、電源がオンで、正常に機能しています。  

    ルーターが UPnP フレームワークをサポートしない場合、またはインストール中にルーターを構成できない場合、ネットワークの設定を使って手動でルーターを構成する必要があります。 次のポートが開いていて、移行先サーバーの IP アドレスに接続されていることを確認してください。  

  |ポート番号|アプリケーション|  
  |-----------------|-----------------|  
  |ポート 80|HTTP Web トラフィック|  
  |ポート 443|HTTPS Web トラフィック|  


- **Windows Server Essentials リリースのドキュメントを参照して**ください。 リリースドキュメントには、Windows Server Essentials を適切にインストールおよび構成するために重要な最新情報が記載されています。 リリースドキュメントを表示または印刷するには、「 [Windows Server Essentials のリリースドキュメント](../get-started/release-notes.md)」を参照してください。  

## <a name="see-also"></a>関連項目  

-   [Windows Server Essentials のインストール](Install-Windows-Server-Essentials.md)

