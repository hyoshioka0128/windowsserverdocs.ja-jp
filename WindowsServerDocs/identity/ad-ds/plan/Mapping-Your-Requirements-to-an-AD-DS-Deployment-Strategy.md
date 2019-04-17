---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: "要件、AD DS の展開戦略をマッピングします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b4f625f06fede5b9dc751282cda19b68d7f9e535
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>要件、AD DS の展開戦略をマッピングします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

終了後、確認して、Active Directory ドメイン サービス (AD DS) の設計を識別して展開の要件とするを決定し、特定の展開に関連するが、それらの要件を特定の AD DS の展開戦略にマップできます。  
  
AD DS の設計と展開の適切な組み合わせ、組織の要件にマップする AD DS の展開戦略を決定するのにには、次の表を使用します。 (「はい」特定の要件が、展開戦略; ために必要なことを示します"No"を意味特定の要件が、展開戦略に必要ないことです。)  
  
次の表は、このガイドで説明するよう、3 つの主な AD DS の展開戦略にのみ参照します。  
  
-   [新しい組織内の AD DS を展開](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 組織内の AD DS を展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows 2000 組織内の AD DS を展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
ただし、組織のニーズを満たすために、AD DS の設計と展開の要件の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD DS 展開戦略を作成できます。  
  
|AD DS の設計と展開の要件|新しい組織内の AD DS を展開|Windows Server 2003 組織内の AD DS を展開|Windows 2000 組織内の AD DS を展開|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008 AD DS の論理構造の設計](https://technet.microsoft.com/library/cc770806.aspx)|うん|うん|うん|  
|[Windows Server 2008 AD DS のサイト トポロジの設計](Designing-the-Site-Topology.md)|うん|うん|うん|  
|ドメイン コントローラーの処理能力の計画|うん|うん|うん|  
|[Windows Server 2008 フォレスト ルート ドメインを展開します。](https://technet.microsoft.com/library/cc731174.aspx)|うん|違います|違います|  
|[Windows Server 2008 地域ドメインの展開](https://technet.microsoft.com/library/cc755118.aspx)|うん|うん|うん|  
|[AD DS の高度な機能を有効にします。](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|うん|[はい] が環境内のすべてのドメイン コントローラーは、Windows Server 2008 ドメインまたはフォレストの機能レベルを設定する前に Windows Server 2008 を実行する必要があります。|[はい] が環境内のすべてのドメイン コントローラーは、Windows Server 2008 ドメインまたはフォレストの機能レベルを設定する前に Windows Server 2008 を実行する必要があります。|  
|[Windows Server 2008 および Windows Server 2008 R2 の AD DS ドメインに Active Directory ドメインをアップグレードします。](https://technet.microsoft.com/library/cc731188.aspx)|違います|うん|うん|  
|[フォレスト間での AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=93678)|はい、パイロット ドメインを実稼働環境に移行する場合は、別の組織とのマージし 2 つの情報技術 (IT) インフラストラクチャを統合または Windows 2000 または Windows Server 2003 環境からのインプレース アップグレードするリソースとアカウントのドメインを統合します。|はい (別の組織と結合し、2 つの IT インフラストラクチャの統合または Windows 2000 または Windows Server 2003 環境からのインプレース アップグレードするリソースとアカウントのドメインを統合する場合)。|はい (別の組織と結合し、2 つの IT インフラストラクチャの統合または Windows 2000 または Windows Server 2003 環境からのインプレース アップグレードするリソースとアカウントのドメインを統合する場合)。|  
|[フォレスト内にある AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=82740))|違います|はい、ドメインの数を減らす場合は、レプリケーション トラフィックと、必要なユーザーおよびグループの管理の量を減らすまたはグループ ポリシーの管理を簡略化します。|はい、ドメインの数を減らす場合は、レプリケーション トラフィックと、必要なユーザーおよびグループの管理の量を減らすまたはグループ ポリシーの管理を簡略化します。|  
  


