---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: "Windows Server 2012 R2 で AD FS 設計ガイドします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 498b399818fb8c9e463f9990fa13c87648c0a33d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-design-guide-in-windows-server-2012-r2"></a>Windows Server 2012 R2 で AD FS 設計ガイドします。

>適用対象: Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス \(AD FS\) は、AD FS\ で保護された企業内、フェデレーション パートナー組織では、またはクラウド アプリケーションにアクセスしエンド ユーザーのシンプルで安全な ID フェデレーションと Web シングル sign\ で \(SSO\) 機能を提供します。  
  
Windows Server® 2012 R2 では、AD FS には、id プロバイダーとして機能するフェデレーション サービス役割サービスが含まれています \ (AD FS\ を信頼するアプリケーションにセキュリティ トークンを提供するユーザーを認証) またはフェデレーション プロバイダー \ (他の ID プロバイダーからのトークンを使用して AD FS\ を信頼するアプリケーションにセキュリティ トークンを提供)。  
  
アプリケーションと Windows Server 2012 R2 の AD FS によって保護されたサービスへのエクストラネット アクセスを提供する機能は Web アプリケーション プロキシという新しいリモート アクセス役割サービスを実行できるようになりました。 これは、AD FS フェデレーション サーバー プロキシによって処理されたこの関数を Windows Server の以前のバージョンからの飛躍です。 Web アプリケーション プロキシは、サーバーの役割を AD FS\ に関連するエクストラネット シナリオとその他のエクストラネット シナリオのアクセスを提供するよう設計されています。 Web アプリケーション プロキシの詳細については、次を参照してください。[Web アプリケーション プロキシのチュートリアル ガイド](https://technet.microsoft.com/library/dn280944.aspx)します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドでは、組織の要件に基づき、AD FS の新しい展開を計画するための推奨事項を提供します。 このガイドは、インフラストラクチャ専門家やシステム アーキテクトによって対象読者です。 明らかに主要な判断基準ように AD FS の展開を計画します。 このガイドを読む前の機能レベルでの AD FS のしくみを良く理解が必要です。 詳細については、次を参照してください。[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)します。  
  
## <a name="in-this-guide"></a>このガイドで  
  
-   [AD FS 展開目標を特定します。](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS の要件](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>参照してください。  
[AD FS の設計](../../ad-fs/AD-FS-Design.md)  
  

