---
title: Windows Server 2016 Essentials の新機能
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: affff774-5fa6-4944-887a-9bfde05f6a3f
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 420d3b043959b8b1201aad7a5b3210fd9bd6a0da
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817755"
---
# <a name="whats-new-in-windows-server-2016-essentials"></a>Windows Server 2016 Essentials の新機能

> 適用対象: Windows Server 2016 Essentials

Windows Server 2016 Essentials の新機能と強化された機能は次のとおりです。

## <a name="integration-with-azure-site-recovery-services"></a>[Azure Site Recovery Services との統合](azure-site-recovery-services-integration.md)

保護されているバーチャルマシンに障害が発生した場合、または保護されたバーチャルマシンが実行されているホストサーバーで障害が発生した場合に、オンプレミスのバーチャルマシンまたはホストサーバーが修復されて使用可能になるまで、Azure Site Recovery サービスとのフェールオーバーによっ**て**ビジネスの継続性が維持 --&reg; 

**しくみ**: Microsoft Azure で提供されている Azure Site Recovery サービスを使用すると、仮想マシン (VM) を Azure のバックアップコンテナーにリアルタイムでレプリケートできます。 ハードウェアやその他の障害が原因でサーバーまたはサイトがダウンした場合は、Azure Site Recovery サービスとのフェールオーバーを実行して、バックアップコンテナーに格納されている VM イメージが Azure で実行中の VM としてプロビジョニングされるようにすることができます。 Azure 仮想ネットワークと組み合わせると、オンプレミスサーバーに接続されているクライアント Pc は、Azure で実行されているサーバーに透過的に接続します。     
                                                                                                                                                                                                                                                                                                               

## <a name="integration-with-azure-virtual-network"></a>[Azure Virtual network との統合](azure-virtual-network-integration.md)

クラウドコンピューティングに対して組織が行っていることは、すべてのリソースを一度に移行することはめったにあり**ません**。 代わりに、リソースをクラウドに移動し、一部のリソースをオンプレミスに保持します。 こうすることで、時間の経過と共に組織を段階的にクラウドに移行することが容易になります。 Azure virtual Network の統合により、そのプロセスをシームレスかつ管理しやすいネットワークインフラストラクチャが提供されます。

**しくみ**--azure virtual network は Microsoft Azure で提供されるサービスであり、azure で実行されているリソース (仮想マシンやストレージなど) が、シームレスなアプリケーションとリソースのアクセスのためにローカルネットワーク上にあるかのように、組織はポイントツーポイント (P2P) またはサイト間 (S2S) 仮想プライベートネットワークを作成できます。



## <a name="support-for-larger-deployments"></a>[大規模な展開のサポート](support-for-larger-deployments.md) 

大規模な小規模企業では、Windows Server Essentials を効果的に実装するために、より多くの機能と容量が必要になります。 Windows Server 2016 Essentials では、より大規模な展開のサポートを追加することで、ドメイン、ユーザー、デバイスの管理性が向上します。                                                                                                                                                                                                 

 - 複数のドメイン
 - 複数のドメインコントローラー                                                                                                                                                                                                                                        
 - 指定されたドメインコントローラーを指定する機能                                                                                                                                                                                                                   
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       

<a name="see-also"></a>参照
--------

[Windows Server Essentials &copy;&reg; の概要](get-started.md)