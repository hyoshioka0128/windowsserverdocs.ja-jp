---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: AD FS の展開計画
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831693"
---
# <a name="planning-to-deploy-ad-fs"></a>AD FS の展開計画

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


環境に関する情報を収集し、Active の Directory フェデレーション サービスを決定後\(AD FS\)設計のガイダンスに従って、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)、組織の AD FS 設計の展開の計画を開始することができます。 完成した設計と、このトピックの情報をお客様の組織で AD FS を展開するために実行するタスクを指定できます。  
  
## <a name="reviewing-your-ad-fs-design"></a>AD FS 設計の確認  
構築元の AD FS 設計チームがデザインの場合は、組織が実際には、展開を実装、展開チームが設計チームと最終的な設計をレビューすることを確認する展開チームと異なる。 設計に関して以下の点を確認します。  
  
-   企業ネットワークまたは境界ネットワークにフェデレーション サーバーを配置するのに最適な物理トポロジを決定するための設計チームの戦略。 展開チームは、AD FS の設計ガイドでは、次のトピックを確認してこのテーマに関するドキュメントを参照できます。  
  
    -   [AD FS 構成データベースのロール](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [フェデレーション サーバーの配置の計画](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [フェデレーション サーバー プロキシの配置の計画](https://technet.microsoft.com/library/dd807130.aspx)  
  
    設計チームがフェデレーション サーバーまたはフェデレーション サーバー プロキシの配置を展開チームに委任する場合もあります。 配置作業を引き受けた展開チームは、サーバーの物理トポロジの文書化および実装を担当します。  
  
-   文書化された AD FS 設計の範囲内で、要求プロバイダー、証明書利用者、またはその両方として組織が指定する業務上の理由。 AD FS をデプロイする理由理由とその他の企業や組織は、展開チームのメンバーが理解していることを確認、フェデレーション パートナーシップに関係します。 展開チームのメンバーが他の企業や組織に存在する制約も理解していることを確認\(ハードウェア、エクストラネット環境がないなどの限定\)何らかの方法で設計の範囲を制限することがあります。 パートナー組織の詳細については、「[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)」を参照してください。  
  
設計後にチームと展開チームについて合意これらの問題では、AD FS 設計の展開を続行します。 詳細については、「[AD FS 設計計画の実装](Implementing-Your-AD-FS-Design-Plan.md)」を参照してください。  
