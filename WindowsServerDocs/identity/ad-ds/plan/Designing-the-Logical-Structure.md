---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: 論理構造の設計
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: de56205c163abff1b05d57ea90954fa93606abce
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822615"
---
# <a name="designing-the-logical-structure"></a>論理構造の設計

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) を使用すると、組織は、ユーザーおよびリソース管理のためのスケーラブルで安全な、管理しやすいインフラストラクチャを作成できます。 また、ディレクトリ対応アプリケーションをサポートすることもできます。  
  
適切に設計された Active Directory 論理構造には、次のような利点があります。  
  
-   多数のオブジェクトを含む Microsoft Windows ベースのネットワークの管理の簡略化  
  
-   統合ドメイン構造と管理コストの削減  
  
-   必要に応じて、リソースに対する管理制御を委任する機能  
  
-   ネットワーク帯域幅への影響の軽減  
  
-   簡素化されたリソースの共有  
  
-   最適な検索パフォーマンス  
  
-   総保有コストの削減  
  
適切に設計された Active Directory 論理構造を利用すると、グループポリシーのような機能を効率的に統合できます。デスクトップのロックダウンソフトウェアの配布システムにユーザー、グループ、ワークステーション、およびサーバー管理を行います。 また、慎重に設計された論理構造により、microsoft と microsoft 以外のアプリケーションやサービス (Microsoft Exchange Server、公開キー基盤 (PKI)、ドメインベースの分散ファイルシステム (DFS) など) の統合が容易になります。  
  
AD DS を配置する前に Active Directory 論理構造を設計する場合は、Active Directory の機能を最大限に活用するために、展開プロセスを最適化できます。 Active Directory の論理構造を設計するために、設計チームはまず組織の要件を特定し、この情報に基づいて、フォレストとドメインの境界をどこに配置するかを決定します。 次に、設計チームは、フォレストのニーズに合わせてドメインネームシステム (DNS) 環境を構成する方法を決定します。 最後に、設計チームは、組織内のリソースの管理を委任するために必要な組織単位 (OU) 構造を識別します。  
  
## <a name="in-this-guide"></a>このガイドの内容  
  
-   [Active Directory の論理モデルについて](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [展開プロジェクトの参加者を識別する](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [フォレスト設計の作成](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [フォレスト設計の作成](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS インフラストラクチャの設計を作成する](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [組織単位の設計を作成する](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [付録 A: DNS インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


