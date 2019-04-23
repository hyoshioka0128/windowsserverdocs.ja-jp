---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: 論理構造の設計
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 82184fe678c05b1d7458584de8eecd0c07ece02f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832333"
---
# <a name="designing-the-logical-structure"></a>論理構造の設計

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) を使用することにより、ユーザーおよびリソース管理の拡張性の高い、安全かつ管理しやすいインフラストラクチャを作成します。 ディレクトリ対応アプリケーションをサポートすることもできます。  
  
適切に設計された Active Directory 論理構造には、次の利点があります。  
  
-   多数オブジェクトにはが含まれている Microsoft Windows ベースのネットワークの管理の簡略化  
  
-   統合されたドメイン構造と管理コストの削減  
  
-   必要に応じて、リソースの管理制御を委任する機能  
  
-   ネットワーク帯域幅に影響が低減  
  
-   簡略化されたリソースの共有  
  
-   最適な検索のパフォーマンス  
  
-   所有権の総保有コスト  
  
適切に設計された Active Directory 論理構造には、グループ ポリシーなどの機能の効率的な統合が容易になります。デスクトップ ロックダウンソフトウェアの配布システムにユーザー、グループ、ワークステーション、およびサーバーの管理。 さらに、慎重に設計された論理構造には、Microsoft と Microsoft 以外のアプリケーションと Microsoft Exchange Server の公開キー基盤 (PKI) などのサービスの統合が容易にし、ドメイン ベースの分散ファイル システム (DFS)。  
  
AD DS を展開する前に、Active Directory 論理構造を設計するときは、最適に Active Directory の機能の活用するための展開プロセスを最適化できます。 Active Directory 論理構造を設計するには、デザイン チームまず、組織の要件を特定して、この情報に基づいて、フォレストおよびドメインの境界を配置する場所を決定します。 次に、設計チームは、フォレストのニーズを満たすために、ドメイン ネーム システム (DNS) 環境を構成する方法を決定します。 最後に、設計チームは、組織内のリソースの管理を委任するために必要な組織単位 (OU) 構造体を識別します。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [Active Directory 論理モデルをについてください。](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [展開プロジェクトの参加者を識別します。](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [フォレスト設計の作成](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [フォレスト設計の作成](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [DNS インフラストラクチャの設計を作成します。](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [組織単位設計の作成](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [付録 a:DNS インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


