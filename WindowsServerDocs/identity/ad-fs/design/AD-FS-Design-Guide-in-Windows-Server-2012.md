---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: "Windows Server 2012 で AD FS 設計ガイドします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e660c1dabcc5a683fa74068ea148fd4efbeee569
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012"></a>Windows Server 2012 で AD FS 設計ガイドします。

>適用対象: Windows Server 2012
  
> [!NOTE]  
> Windows Server 2012 R2 で AD FS を展開する方法については、次を参照してください。[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)します。  
  
フェデレーション サービス プロバイダーの役割での Windows Server® 2012 オペレーティング システムと Active Directory® フェデレーション サービス \(AD FS\) を使用すると、Web ベースのサービスまたは管理者が作成または管理の外部の信頼またはフォレストの信頼関係の両方の組織と、ユーザーがもう一度ログオンするのに必要なしのネットワーク間で必要とせず、リソース パートナー組織に存在するアプリケーションをユーザーにシームレスに認証を行います。 別のネットワーク リソースにアクセスするときに、1 つのネットワークに認証するためのプロセス: ユーザーがログオン操作の負担がない — \(SSO\) sign\ で 1 つと呼ばれます。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドは、組織の要件に基づき、AD FS の新しい展開を計画するための推奨事項を提供 \ (展開 goals\ としては、このガイドでも言います) と特定の設計を作成します。 このガイドは、インフラストラクチャ専門家やシステム アーキテクトによって対象読者です。 明らかに主要な判断基準ように AD FS の展開を計画します。 このガイドを読む前の機能レベルでの AD FS のしくみを良く理解が必要です。 AD FS 設計に反映される組織の要件を良く理解もが必要です。  
  
このガイドでは一連の 3 つのプライマリ AD FS 設計に基づいた展開の目標について説明し、環境に最適な設計を決定できます。 次の包括的な AD FS 設計または環境のニーズを満たしているカスタム設計のいずれかの形式にこれらの展開の目標を使用することができます。  
  
-   フェデレーション Web SSO business\ 商取引へ記述 \(B2B\) シナリオをサポートして、独立したフォレストの事業単位間のコラボレーションをサポートするには  
  
-   Web SSO 消費者へ記述 business\ \(B2C\) シナリオで顧客アプリケーションへのアクセスをサポートするには  
  
それぞれの設計では、自社環境について必要なデータを収集するためのガイドラインが表示されます。 次のガイドラインを使用してに計画立案し、AD FS の展開を設計できます。 ガイダンスを使用して AD FS の展開を開始するために必要な情報がこのガイドを参照し、収集、文書化、および組織の要件をマッピングを完了した後、[Windows Server 2012 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md)します。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [AD FS 展開目標の特定](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 設計への展開目標のマッピング](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [AD FS 展開トポロジを決定します。](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [展開の計画](Planning-Your-Deployment.md)  
  
-   [フェデレーション サーバーの配置を計画します。](Planning-Federation-Server-Placement.md)  
  
-   [フェデレーション サーバー プロキシの配置を計画します。](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [AD FS サーバーの容量計画](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [付録 a: AD FS の要件を確認します。](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

