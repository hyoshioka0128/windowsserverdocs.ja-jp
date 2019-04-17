---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: "論理構造の設計"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8d1b9c27f05faef49f7fd4228f4ebe689b75d30f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-logical-structure"></a>論理構造の設計

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory ドメイン サービス (AD DS) を使用することにより、スケーラブルで安全であり、および管理できるユーザーおよびリソース管理のインフラストラクチャを作成します。 ディレクトリ対応アプリケーションをサポートすることもできます。  
  
適切に設計された Active Directory 論理構造体には、次の利点があります。  
  
-   多数オブジェクトにはが含まれている Microsoft Windows ベースのネットワークの簡略化された管理  
  
-   統合のドメイン構造と管理コストの削減  
  
-   必要に応じて、リソースの管理制御を委任する機能  
  
-   ネットワーク帯域幅に与える影響を軽減  
  
-   簡素化されたリソースの共有  
  
-   最適な検索のパフォーマンス  
  
-   総保有コストを低  
  
適切に設計された Active Directory 論理構造体には、グループ ポリシー; などの機能の効率的な統合が容易になります。デスクトップのロックダウンします。ソフトウェアの配布ユーザー、グループ、ワークステーション、およびサーバーの管理システムにします。 さらに、Microsoft および Microsoft 以外のアプリケーションとサービス、Microsoft Exchange Server、公開キー基盤 (PKI) などの統合を容易に慎重に考慮した設計の論理構造とドメイン ベースの分散ファイル システム (DFS)。  
  
AD DS を展開する前に、Active Directory 論理構造を設計する場合は、最適な利用するために Active Directory の機能の展開プロセスを最適化できます。 Active Directory 論理構造を設計するには、設計チーム最初に、組織の要件を特定し、この情報に基づいて、フォレストおよびドメインの境界を配置する場所を決定します。 次に、設計チームは、フォレストのニーズに合わせてドメイン ネーム システム (DNS) 環境を構成する方法を決定します。 最後に、設計チームは、組織内のリソースの管理に委任するために必要な組織単位 (OU) 構造体を識別します。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [Active Directory 論理モデルを理解します。](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [展開プロジェクトの参加者を識別します。](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [フォレストの設計を作成します。](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [ドメインの設計を作成します。](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS インフラストラクチャの設計を作成します。](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [組織単位設計を作成します。](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [付録 a: DNS インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


