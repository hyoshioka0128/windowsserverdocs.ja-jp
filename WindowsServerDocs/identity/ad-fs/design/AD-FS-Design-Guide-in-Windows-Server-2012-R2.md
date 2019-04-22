---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: Windows Server 2012 R2 での AD FS 設計ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 498b399818fb8c9e463f9990fa13c87648c0a33d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822153"
---
# <a name="ad-fs-design-guide-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での AD FS 設計ガイド

>適用先:Windows Server 2016、Windows Server 2012 R2

Active Directory フェデレーション サービス\(AD FS\)シンプルで安全な id フェデレーションと Web シングル サインオンを提供します\-で\(SSO\)アプリケーションへのアクセスを希望するエンドユーザー向け機能。AD FS 内\-enterprise、またはクラウドでフェデレーション パートナー組織では、セキュリティで保護します。  
  
Windows Server® 2012 R2 では、AD FS には id プロバイダーとして機能するフェデレーション サービス役割サービスが含まれます\(AD FS を信頼するアプリケーションにセキュリティ トークンを提供するユーザーを認証\)またはフェデレーション プロバイダー \(他の id プロバイダーからトークンを使用して、AD FS を信頼するアプリケーションにセキュリティ トークン\)します。  
  
Windows Server 2012 R2 の AD FS によって保護されたアプリケーションやサービスへのエクストラネット アクセスを提供する機能は、Web アプリケーション プロキシと呼ばれる新しいリモート アクセス役割サービスによて実行されるようになりました。 以前のバージョンの Windows Server では、この機能は AD FS フェデレーション サーバー プロキシによって処理されていました。 Web アプリケーション プロキシは、AD FS のアクセスを提供するサーバーの役割\-エクストラネット シナリオとその他のエクストラネット シナリオに関連します。 Web アプリケーション プロキシの詳細については、次を参照してください。 [Web アプリケーション プロキシのチュートリアル ガイド](https://technet.microsoft.com/library/dn280944.aspx)します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドでは、組織の要件に基づいて、AD FS の新しい展開を計画に役立つ推奨事項を提供します。 このガイドの対象読者は、インフラストラクチャ専門家またはシステム アーキテクトです。 AD FS の展開を計画するときの主要な判断基準が強調表示されます。 このガイドを読む前に、AD FS が機能レベルでどのように動作するしくみをよく理解が必要です。 詳細については、「 [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)」を参照してください。  
  
## <a name="in-this-guide"></a>このガイドについて  
  
-   [AD FS 展開目標を識別します。](Identify-Your-AD-FS-Deployment-Goals.md)  
  
-   [AD FS 展開トポロジを計画します。](Plan-Your-AD-FS-Deployment-Topology.md)  
  
-   [AD FS の要件](AD-FS-Requirements.md)  
  
  
## <a name="see-also"></a>関連項目  
[AD FS の設計](../../ad-fs/AD-FS-Design.md)  
  

