---
ms.assetid: d04dd17e-a843-46fd-8711-0039918f92d9
title: "設計計画の AD FS を実装します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 31c2e048c3c125d0ea60610b049501151d7aa823
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="implementing-your-ad-fs-design-plan"></a>設計計画の AD FS を実装します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

環境の次の条件と要件は、Active Directory フェデレーション サービス \(AD FS\) 設計計画の実装で重要な要素には。  
  
-   **パートナーのサポート:**通常パートナー組織と連携する AD FS を使用します。 Id フェデレーションを確立するには、パートナーシップを形成する組織を決定します。 基準 AD FS の展開を配置した後はパートナーで動作してパートナーを追加、パートナーを削除およびパートナー情報を更新する必要があります。 さまざまな理由パートナーシップへの変更は発生します。 たとえば、AD FS 展開は、パートナーの事業を大幅に変更する、大規模な組織や、組織のフェデレーションの一部となり、組織または別の会社によって、組織が取得された場合パートナーシップの更新プログラムを必要があります。 複数のドメインからの id をフェデレーションでどのようなシナリオをサポートしているドメイン \(partners\) と潜在的なパートナーを表すすべての他のドメインを知っている必要があります。  
  
-   **サポートされているアプリケーションとサービスの種類:**られるものもあれば「要求に対応します」にオペレーティング システムのリソースへのアクセスを必要と、一部のアプリケーションとサービス。 これは、アプリケーションと AD FS をサポートするため、管理の要件を策定するサービスの種類を理解する重要です。  
  
-   **アーキテクチャ図の論理的および物理的なまたは展開トポロジ:**を知る必要があります。  
  
    -   かどうかのフェデレーション サーバー ファームのサーバーまたは単一のサーバー上のセットで機能します。  
  
    -   ここで、ネットワークのファイアウォールとプロキシを展開します。  
  
    -   リソースとユーザーが組織、またはその両方の外部の組織内からのリソースにアクセスしているかどうかの場所です。  
  
## <a name="how-to-implement-your-ad-fs-design-using-this-guide"></a>このガイドを使用して AD FS 設計を実装する方法  
次の手順、設計の実装では、どのような順序で各展開のタスクを実行する必要がありますを決定します。 このガイドでは、さまざまなサーバーとアプリケーションの展開タスク設計計画を実装するのに必要がある順を追ってするためのチェックリストを使用します。 親と子チェックリストは、特定の AD FS のタスクの設計を処理する必要があります順序を表すを必要に応じてが使用されます。  
  
このガイドのこのセクションで、次の親チェックリストを使用して、習熟して、組織の優先 AD FS 設計の実装の展開タスク。  
  
-   [チェックリスト: Web SSO 設計の実装](Checklist--Implementing-a-Web-SSO-Design.md)  
  
-   [チェックリスト: フェデレーション Web SSO 設計の実装](Checklist--Implementing-a-Federated-Web-SSO-Design.md)  
