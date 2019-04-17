---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: "AD FS 展開トポロジを決定します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3300c16be6d516d7ec0bf4d0c3a025e59e6126b6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="determine-your-ad-fs-deployment-topology"></a>AD FS 展開トポロジを決定します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) の展開の計画の最初の手順を 1 つで sign\ \(SSO\) を満たすために最適な展開トポロジの決定には、組織の必要があります。 このセクションのトピックでは、AD FS で使用できるさまざまな展開トポロジについて説明します。 利点と、特定のビジネス ニーズに最も適切なトポロジを選択できるように、各展開トポロジに関連付けられている制限事項についても説明します。  
  
この展開トポロジに関するトピックを読む前に、まず次の表に示されている順序でタスクを完了することをお勧めします。  
  
|推奨されるタスク|説明|リファレンス|  
|--------------------|---------------|-------------|  
|AD FS データは保存され、フェデレーション サーバー ファームの他のフェデレーション サーバーにレプリケートされる方法を確認します。|目的とすることができます、AD FS 構成データベースに格納されている基になるデータのレプリケーションの方法を理解してください。 このトピックは、構成データベースの概念を紹介し、2 つのデータベースの種類について説明します。Windows Internal Database \(WID\) と Microsoft SQL Server。|[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|組織で展開する AD FS 構成データベースの種類を選択します。|さまざまな利点とサポートされるさまざまなアプリケーションのシナリオと、AD FS 構成データベースとして WID または SQL Server のいずれかを使用して関連付けられている制限事項を確認します。|[AD FS 展開トポロジに関する考慮事項](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> 基本的な冗長性、負荷分散、およびフェデレーション サービス \(if required\) をスケーリングするオプションを実装するにを使用するデータベースの種類に関係なく、すべての運用環境でフェデレーション サーバー ファームごとに少なくとも 2 つのフェデレーション サーバーを展開することをお勧めします。  
  
前の表に、コンテンツを確認したときに、このセクションで、次のトピックに進みます。  
  
-   [WID を使用するスタンドアロン フェデレーション サーバー](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [フェデレーション サーバー ファームが WID を使用します。](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [WID とプロキシを使用してフェデレーション サーバー ファーム](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [SQL Server を使用してフェデレーション サーバー ファーム](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
トピックを確認することをお勧め AD FS 展開トポロジの選択が完了したら、[AD FS サーバーの容量計画](Planning-for-AD-FS-Server-Capacity.md)をこのトポロジをサポートするために展開する必要のあるサーバーの推奨数を決定します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

