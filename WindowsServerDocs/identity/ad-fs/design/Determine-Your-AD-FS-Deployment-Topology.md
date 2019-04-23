---
ms.assetid: f67b0bc9-e5af-4891-9da0-d9be539af42d
title: AD FS 展開トポロジの決定
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3300c16be6d516d7ec0bf4d0c3a025e59e6126b6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834523"
---
# <a name="determine-your-ad-fs-deployment-topology"></a>AD FS 展開トポロジの決定

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスの展開の計画の最初の手順\(AD FS\)は、シングル サインオンを満たすために適切な展開トポロジを決定\-で\(SSO\)の必要があります、組織。 このセクションのトピックでは、AD FS で使用できるさまざまな展開トポロジについて説明します。 また、特定のビジネスのニーズに最適なトポロジを選択できるよう、各展開トポロジに関連する利点と制約事項についても説明します。  
  
この展開トポロジに関するトピックを読む前に、まず次の表に示したタスクを記載された順に実行することをお勧めします。  
  
|推奨されるタスク|説明|リファレンス|  
|--------------------|---------------|-------------|  
|AD FS のデータが格納され、フェデレーション サーバー ファーム内の他のフェデレーション サーバーにレプリケートする方法を確認します。|AD FS 構成データベースに保存されている基になるデータの目的と使用可能なレプリケーション方法について理解します。 このトピックでは、構成データベースの概念を紹介し、2 種類のデータベースWindows Internal Database \(WID\)と Microsoft SQL Server。|[AD FS 構成データベースのロール](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)|  
|組織で展開する AD FS 構成データベースの種類を選択する。|AD FS 構成データベースとして WID または SQL Server のどちらかを使用することに関連するさまざまな利点および制約事項と、データベースでサポートされるさまざまな利用シナリオを確認します。|[AD FS 展開トポロジに関する考慮事項](AD-FS-Deployment-Topology-Considerations.md)|  
  
> [!NOTE]  
> 基本的な冗長性、負荷分散、およびフェデレーション サービスをスケーリングするオプションを実装する\(必要な場合\)、すべての運用環境でのフェデレーション サーバー ファームごとに少なくとも 2 つのフェデレーション サーバーをデプロイすることをお勧めします。使用するデータベースの種類に関係なく。  
  
前述の表の内容を確認したら、このセクションの次のトピックに進んでください。  
  
-   [WID を使用してスタンドアロン フェデレーション サーバー](Stand-Alone-Federation-Server-Using-WID.md)  
  
-   [WID を使用してフェデレーション サーバー ファーム](Federation-Server-Farm-Using-WID-2012.md)  
  
-   [WID とプロキシを使用してフェデレーション サーバー ファーム](Federation-Server-Farm-Using-WID-and-Proxies-2012.md)  
  
-   [SQL Server を使用してフェデレーション サーバー ファーム](Federation-Server-Farm-Using-SQL-Server-2012.md)  
  
トピックを確認することをお勧め、AD FS 展開トポロジの選択が完了したら、 [AD FS サーバーのキャパシティ プランニング](Planning-for-AD-FS-Server-Capacity.md)このトポロジをサポートするためにデプロイする必要がありますサーバーの推奨される数を決定します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

