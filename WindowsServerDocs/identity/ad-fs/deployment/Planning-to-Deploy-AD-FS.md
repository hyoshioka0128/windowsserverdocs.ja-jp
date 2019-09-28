---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: AD FS の展開計画
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ed2082706975d58a1535aaeb61e6c5283d23306a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359503"
---
# <a name="planning-to-deploy-ad-fs"></a>AD FS の展開計画


環境に関する情報を収集し、 [Windows Server 2012 の AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)のガイダンスに従って Active Directory フェデレーションサービス (AD FS) @no__t 0ad FS @ no__t の設計を決定した後、次の展開の計画を開始できます。組織の AD FS 設計。 完成した設計とこのトピックの情報により、組織内の AD FS を展開するために実行するタスクを決定できます。  
  
## <a name="reviewing-your-ad-fs-design"></a>AD FS 設計の確認  
組織に対して元の AD FS 設計を構築した設計チームが、実際に配置を実装する配置チームと異なる場合は、配置チームが設計チームで最終的な設計をレビューしていることを確認してください。 設計に関して以下の点を確認します。  
  
-   企業ネットワークまたは境界ネットワークにフェデレーション サーバーを配置するのに最適な物理トポロジを決定するための設計チームの戦略。 展開チームは、AD FS 設計ガイドの次のトピックを確認することで、このテーマに関するドキュメントを参照できます。  
  
    -   [AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [フェデレーション サーバー プロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)  
  
    設計チームがフェデレーション サーバーまたはフェデレーション サーバー プロキシの配置を展開チームに委任する場合もあります。 配置作業を引き受けた展開チームは、サーバーの物理トポロジの文書化および実装を担当します。  
  
-   文書化された AD FS 設計の範囲内で、要求プロバイダー、証明書利用者、またはその両方として組織が指定する業務上の理由。 展開チームのメンバーが、AD FS が展開される理由と、フェデレーションパートナーシップに関係する他の企業や組織を理解していることを確認します。 また、展開チームのメンバーは、他の企業または @no__t 組織に存在する制約を理解していることを確認してください。これは、no__t のないハードウェア、エクストラネット環境のない、@-1 など、何らかの方法で設計の範囲を制限することがあるためです。 パートナー組織の詳細については、「[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)」を参照してください。  
  
設計チームと展開チームがこれらの問題に同意したら、AD FS 設計のデプロイを進めることができます。 詳細については、「[AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)」を参照してください。  
