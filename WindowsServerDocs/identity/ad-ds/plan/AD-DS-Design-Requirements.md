---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: "AD DS の設計の要件"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 17338cd00fecec098865095dd9613f62beb3a457
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="ad-ds-design-requirements"></a>AD DS の設計の要件

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Active Directory 論理構造の設計  
Windows Server 2008 Active Directory ドメイン サービス (AD DS) を展開する前の計画し、環境の AD DS 論理構造を設計する必要があります。 AD DS 論理構造体は、ディレクトリ オブジェクトの編成方法を決定し、ネットワーク アカウントとの共有リソースを管理するための効果的な方法を示します。 AD DS 論理的な構造を設計するときに、組織のネットワーク インフラストラクチャの重要な要素を定義します。  
  
AD DS 論理構造を設計するには、組織が必要なフォレスト数を決定し、ドメイン、ドメイン ネーム システム (DNS) インフラストラクチャ、および組織単位 (Ou) の設計を作成します。 次の図は、論理構造の設計プロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
詳細については、次を参照してください。 [、論理構造の Windows Server 2008 AD DS の設計](Designing-the-Logical-Structure.md)します。  
  
## <a name="designing-the-site-topology"></a>サイト トポロジの設計  
論理構造を設計するには、AD DS インフラストラクチャ、後に、ネットワークのサイト トポロジを設計する必要があります。 サイトのトポロジは、物理ネットワークの論理表現です。 AD DS サイト、サイトごとに、サイト リンクとサイト間での AD DS のレプリケーションをサポートするサイト リンク ブリッジ内の AD DS ドメイン コント ローラーの場所に関する情報が含まれています。 次の図は、サイトのトポロジの設計プロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
詳細については、次を参照してください。 [、サイトのトポロジの Windows Server 2008 AD DS の設計](Designing-the-Site-Topology.md)します。  
  
## <a name="planning-domain-controller-capacity"></a>ドメイン コント ローラーの処理能力の計画  
効率的な AD DS のパフォーマンスを確保する必要があるには、各サイトのドメイン コント ローラーの適切な数を特定し、Windows Server 2008 のハードウェア要件を満たしていることを確認します。 注意の容量計画、ドメイン コント ローラーにより、ハードウェアの要件は、不適切なドメイン コント ローラーのパフォーマンスとアプリケーションの応答時間が発生する可能性が少なく見積もらされません。 次の図では、ドメイン コント ローラーの容量計画のプロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>高度な AD DS の機能を Windows Server 2008 を有効にします。  
Windows Server 2008 AD DS を使用すると、ドメインまたはフォレストの機能レベルを上げるによってお客様の環境に高度な機能を紹介します。 ドメインまたはフォレスト内のすべてのドメイン コント ローラーは、Windows Server 2008 を実行しているときに、Windows Server 2008 機能レベルを上げることができます。  
  
詳細については、次を参照してください。 [AD DS の高度な機能を有効にすると](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)します。  
  


