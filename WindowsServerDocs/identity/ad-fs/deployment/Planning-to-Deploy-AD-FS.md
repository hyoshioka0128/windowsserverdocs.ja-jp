---
ms.assetid: c87dc32d-ab33-44d2-a46f-f9f878b4e5b4
title: "AD FS の展開を計画するには"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ca9e53d7d98f3ae5e6b7b329e52d4979e8c10215
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="planning-to-deploy-ad-fs"></a>AD FS の展開を計画するには

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


お客様の環境に関する情報を収集すると、ガイダンスに従って、Active Directory フェデレーション サービス \(AD FS\) 設計を決定する、[Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)、組織の AD FS 設計の展開の計画を開始することができます。 完成した設計と、このトピックの情報、組織内の AD FS の展開を実行するタスクを決定できます。  
  
## <a name="reviewing-your-ad-fs-design"></a>AD FS 設計を確認します。  
作成元の AD FS 設計チームを設計する場合、組織は、実際には、展開を実装展開チームが最終的な設計チームと設計を確認することを確認する展開チームとは異なるです。 設計に関して以下の点を確認します。  
  
-   企業ネットワークまたは境界ネットワーク内のフェデレーション サーバーの配置のための最良の物理トポロジを決定する設計チームの戦略です。 展開チームは、AD FS 設計ガイドの次のトピックを確認して、このテーマに関するドキュメントを参照できます。  
  
    -   [AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)  
  
    -   [フェデレーション サーバーの配置を計画します。](https://technet.microsoft.com/library/dd807069.aspx)  
  
    -   [フェデレーション サーバー プロキシの配置を計画します。](https://technet.microsoft.com/library/dd807130.aspx)  
  
    設計チームにフェデレーション サーバーまたはフェデレーション サーバー プロキシの配置を展開チームのサブジェクトがそのまま使用可能性があることができます。 展開チームは、文書化して、サーバーの物理トポロジを実装します。  
  
-   業務上の理由としては、要求プロバイダー、証明書利用者、またはその両方を文書化された AD FS 設計のスコープ内にある組織が指定します。 AD FS が展開されている理由上の理由から、および他の企業や組織に展開チームのメンバーが理解していることを確認して、フェデレーション パートナーシップに関係します。 展開チームのメンバーが他の企業や組織に存在する制約も理解していることを確認 \ (ハードウェア、エクストラネット環境がない、およびその forth\ 制限付き) 何らかの方法で設計の範囲を制限することがあります。 パートナー組織の詳細については、次を参照してください。[展開の計画](https://technet.microsoft.com/library/dd807083.aspx)します。  
  
設計後チームと展開チームが一致してこれらの問題では、AD FS 設計の展開を進めることができます。 詳細については、次を参照してください。[AD FS 設計の計画を実装する](Implementing-Your-AD-FS-Design-Plan.md)します。  
