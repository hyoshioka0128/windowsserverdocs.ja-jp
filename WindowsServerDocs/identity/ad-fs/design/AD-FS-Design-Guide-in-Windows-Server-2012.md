---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: Windows Server 2012 での AD FS 設計ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3f2a6df6a9c9a5cbdfa9c64bc6521e92f4982a15
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191734"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>Windows Server で AD FS 設計ガイドします。 


  
> [!NOTE]  
> Windows Server 2012 R2 で AD FS をデプロイする方法については、次を参照してください。 [Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)します。  
  
Active Directory® フェデレーション サービスを使用する\(AD FS\)フェデレーションでは、オペレーティング システム サービスをシームレスに任意の Web にユーザーを認証プロバイダーの役割の Windows Server® 2012\-ベースのサービスまたは管理者を作成したり、外部の信頼またはフォレストの信頼をもう一度ログオンするユーザーを必要としないと両方の組織のネットワーク間の管理を必要としない、リソース パートナー組織に存在するアプリケーション。 別のネットワーク内のリソースにアクセス中に 1 つのネットワークへの認証のプロセス-ユーザーが繰り返しログオン操作を行うことがなく — はシングル サインオンと呼ばれます\-で\(SSO\)します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドは、組織の要件に基づいて、AD FS の新しい展開を計画に役立つ推奨事項を提供します。\(も展開の目標としてこのガイドで指す\)と特定の設計を作成します。 このガイドの対象読者は、インフラストラクチャ専門家またはシステム アーキテクトです。 AD FS の展開を計画するときの主要な判断基準が強調表示されます。 このガイドを読む前に、AD FS が機能レベルでどのように動作するしくみをよく理解が必要です。 反映される組織の要件の理解は、AD FS 設計にも必要です。  
  
このガイドは、一連の 3 つのプライマリ AD FS 設計に基づいた展開の目標をについて説明し、環境に最適な設計を決定できます。 次の包括的な AD FS 設計または環境のニーズを満たすカスタム デザインの 1 つのフォームにこれらの展開目標を使用できます。  
  
-   フェデレーション Web SSO ビジネスをサポートする\-に\-ビジネス\(B2B\)シナリオと、独立したフォレストの事業単位間のコラボレーションをサポートするには  
  
-   ビジネス アプリケーションを顧客へのアクセスをサポートするために SSO を web\-に\-コンシューマー \(B2C\)シナリオ  
  
それぞれの設計について、環境に関して必要なデータを収集するガイドラインが示されています。 計画し、AD FS の展開を設計し、次のガイドラインを使用できます。 このガイドを参照する、収集、文書化、および、組織の要件のマッピングを完了すると、必要があります」のガイダンスを使用して AD FS の展開を開始するために必要な情報、 [Windows Server 2012 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [AD FS 展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [展開目標の AD FS 設計への反映](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [AD FS 展開トポロジの決定](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [展開の計画](Planning-Your-Deployment.md)  
  
-   [フェデレーション サーバーの配置の計画](Planning-Federation-Server-Placement.md)  
  
-   [フェデレーション サーバー プロキシの配置の計画](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [AD FS サーバーの容量計画](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [付録 A: AD FS 要件の確認](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

