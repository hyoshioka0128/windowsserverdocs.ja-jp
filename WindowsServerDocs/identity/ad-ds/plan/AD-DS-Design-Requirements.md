---
ms.assetid: f6e76ef0-2217-4cdb-980f-22a780a85ebb
title: AD DS の設計の要件
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 79c694112f39adf5d37cd28f6bd7a770dedf3976
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857523"
---
# <a name="ad-ds-design-requirements"></a>AD DS の設計の要件

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

  
## <a name="designing-the-active-directory-logical-structure"></a>Active Directory 論理構造の設計  
Windows Server 2008 Active Directory Domain Services (AD DS) を展開する前に、計画し、環境内の AD DS の論理構造を設計する必要があります。 AD DS の論理構造が、ディレクトリ オブジェクトの編成方法を決定し、ネットワーク アカウントおよび共有リソースを管理するための有効な手段を提供します。 AD DS の論理構造を設計するときは、組織のネットワーク インフラストラクチャのかなりの部分を定義します。  
  
AD DS の論理構造を設計するには、組織に必要なフォレスト数を特定し、し、ドメイン、ドメイン ネーム システム (DNS) インフラストラクチャ、および組織単位 (Ou) のデザインを作成します。 次の図は、論理構造を設計するためのプロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/d5cebae6-a752-4063-a98f-473799c251bd.gif)  
  
詳細については、次を参照してください。 [、論理構造の Windows Server 2008 AD DS の設計](Designing-the-Logical-Structure.md)します。  
  
## <a name="designing-the-site-topology"></a>サイト トポロジの設計  
AD DS インフラストラクチャの論理構造を設計した後は、ネットワークのサイト トポロジを設計する必要があります。 サイト トポロジは、物理的なネットワークの論理表現です。 AD DS サイトでは、各サイトとサイト リンクとサイト間での AD DS のレプリケーションをサポートするサイト リンク ブリッジ内で AD DS ドメイン コント ローラーの場所に関する情報が含まれています。 次の図は、サイトのトポロジの設計プロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/d34d43c0-437f-47cb-9b64-09c0f9ce6479.gif)  
  
詳細については、次を参照してください。[サイト トポロジの Windows Server 2008 AD DS の設計](Designing-the-Site-Topology.md)します。  
  
## <a name="planning-domain-controller-capacity"></a>ドメイン コント ローラーの処理能力の計画  
効率的な AD DS のパフォーマンスを確保する必要があるには、各サイトのドメイン コント ローラーの適切な数を決定し、Windows Server 2008 のハードウェア要件を満たしていることを確認します。 注意の容量計画、ドメイン コント ローラーは、不適切なドメイン コント ローラーのパフォーマンスとアプリケーションの応答時間が発生することができますのハードウェア要件を過小評価しないようにします。 次の図は、ドメイン コント ローラーの容量計画のプロセスを示します。  
  
![AD DS の設計要件](media/AD-DS-Design-Requirements/fff6ef22-5c7b-4478-ad76-42b296dcf769.gif)  
  
## <a name="enabling-windows-server-2008-advanced-ad-ds-features"></a>高度な AD DS の機能を Windows Server 2008 を有効にします。  
Windows Server 2008 AD DS を使用して、ドメインまたはフォレスト機能レベルを上げて、環境に高度な機能を導入することができます。 ドメインまたはフォレスト内のすべてのドメイン コント ローラーが Windows Server 2008 を実行している場合は、Windows Server 2008 への機能のレベルを上げることができます。  
  
詳細については、次を参照してください。 [for AD DS を使用して高度な機能を有効にする](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)します。  
  


