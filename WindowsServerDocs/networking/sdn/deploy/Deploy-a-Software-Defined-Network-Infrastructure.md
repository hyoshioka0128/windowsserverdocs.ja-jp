---
title: ソフトウェア定義ネットワーク インフラストラクチャを展開する
description: このトピックでは、Windows Server 2016 のスクリプトを使用して、Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開する方法に関するトピックへのリンクを示します。
ms.topic: get-started-article
ms.assetid: 6c665c88-df28-4150-81d4-a47e9fa5255c
ms.date: 08/23/2018
ms.author: anpaul
author: AnirbanPaul
manager: grcusanz
ms.openlocfilehash: affc2a3e75411a210aa1335d797b778fc12a8a7f
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993779"
---
# <a name="deploy-a-software-defined-network-infrastructure"></a>ソフトウェアで定義されたネットワークインフラストラクチャを展開する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Microsoft のソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開します。

これらの展開には、Hyper-v ネットワーク仮想化 (HNV)、ネットワークコントローラー、ソフトウェアロードバランサー (SLB/MUX)、ゲートウェイなど、完全に機能するインフラストラクチャに必要なすべてのテクノロジが含まれます。

## <a name="set-up-sdn-infrastructure-in-the-vmm-fabric"></a>VMM ファブリックでの SDN インフラストラクチャのセットアップ




-   [VMM ファブリックでソフトウェアによるネットワーク制御 (SDN) インフラストラクチャを設定する](/system-center/vmm/deploy-sdn)

    SDN インフラストラクチャを管理するために System Center Virtual Machine manager (VMM) を組み込む場合は、この方法を使用します。

## <a name="deploy-sdn-infrastructure-using-scripts"></a>スクリプトを使用して SDN インフラストラクチャを展開する

-   [スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する](../../sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)

    SDN インフラストラクチャの管理に VMM を使用しない場合、または別の管理方法がある場合は、この方法を使用します。


## <a name="deploy-individual-sdn-technologies-instead-of-an-entire-infrastructure"></a>インフラストラクチャ全体ではなく個々の SDN テクノロジを展開する
 インフラストラクチャ全体ではなく個々の SDN テクノロジを展開する場合は、「 [Windows PowerShell を使用してソフトウェアで定義されたネットワークテクノロジを展開](Deploy-Software-Defined-Network-Technologies-using-Windows-PowerShell.md)する」を参照してください。








## <a name="related-topics"></a>関連トピック
- [ソフトウェア定義ネットワーク (SDN)](../software-defined-networking.md)
- [SDN テクノロジ](../technologies/Software-Defined-Networking-Technologies.md)
- [プラン SDN](../plan/plan-a-software-defined-network-infrastructure.md)
- [SDN の管理](../manage/manage-sdn.md)
- [SDN のセキュリティ](../security/sdn-security-top.md)
- [SDN のトラブルシューティング](../troubleshoot/Troubleshoot-Software-Defined-Networking.md)