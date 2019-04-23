---
title: ソフトウェア定義ネットワーク インフラストラクチャを展開する
description: このトピックでは、Windows Server 2016 でスクリプトを使用して、Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャをデプロイする方法のトピックへのリンクを提供します。
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: virtual-network
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 6c665c88-df28-4150-81d4-a47e9fa5255c
ms.author: pashort
ms.date: 08/23/2018
ms.openlocfilehash: 30d5597cdeb76d636cdf5236228f035999a6bdf6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878023"
---
# <a name="deploy-a-software-defined-network-infrastructure"></a>ソフトウェア定義ネットワーク インフラストラクチャをデプロイします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Microsoft のソフトウェア定義ネットワーク (SDN) インフラストラクチャをデプロイします。   
  
これらの展開には、HYPER-V ネットワーク仮想化 (HNV)、ネットワーク コント ローラー、ソフトウェア ロード バランサー (SLB/MUX)、およびゲートウェイを含む、完全に機能のインフラストラクチャに必要なすべてのテクノロジが含まれます。  
  
## <a name="set-up-sdn-infrastructure-in-the-vmm-fabric"></a>VMM ファブリックで SDN インフラストラクチャを設定します。



  
-   [VMM ファブリックでソフトウェア定義ネットワーク (SDN) インフラストラクチャの設定します。](https://docs.microsoft.com/system-center/vmm/deploy-sdn)  
  
    SDN インフラストラクチャを管理する System Center Virtual Machine Manger (VMM) を組み込みたい場合は、このメソッドを使用します。  
 
## <a name="deploy-sdn-infrastructure-using-scripts"></a>スクリプトを使用して SDN インフラストラクチャをデプロイします。
 
-   [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイします。](../../sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)  
  
    VMM を使用して、SDN インフラストラクチャを管理する必要がない場合、または別の管理方法がある場合は、このメソッドを使用します。  


## <a name="deploy-individual-sdn-technologies-instead-of-an-entire-infrastructure"></a>インフラストラクチャ全体ではなく個々 の SDN テクノロジを展開します。  
 インフラストラクチャ全体ではなく個々 の SDN テクノロジを展開する場合を参照してください。  
[ソフトウェア定義ネットワーク テクノロジ Windows PowerShell を使用してデプロイ](Deploy-Software-Defined-Network-Technologies-using-Windows-PowerShell.md)します。    
  




  


## <a name="related-topics"></a>関連トピック
- [ソフトウェア定義ネットワーク (SDN)](../Software-Defined-Networking--SDN-.md)  
- [SDN テクノロジ](../technologies/Software-Defined-Networking-Technologies.md)  
- [SDN を計画します。](../plan/plan-a-software-defined-network-infrastructure.md)  
- [SDN を管理します。](../manage/manage-sdn.md)
- [SDN のセキュリティ](../security/sdn-security-top.md)
- [SDN をトラブルシューティングします。](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)