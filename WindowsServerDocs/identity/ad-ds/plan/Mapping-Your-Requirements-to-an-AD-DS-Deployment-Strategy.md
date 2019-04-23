---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: AD DS の展開戦略に要件をマッピングする
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: a61e5e6d429acd92e48a353bc829cb620dd66054
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881833"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>AD DS の展開戦略に要件をマッピングする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

特定の AD DS 展開にそれらの要件を割り当てることを確認して、Active Directory Domain Services (AD DS) のデザインを識別するが完了したら、展開要件とするうちに関連する、特定の配置を決定をした後戦略。  
  
次の表を使用して、適切な AD DS の設計と展開の組み合わせ、組織の要件にマップする AD DS の展開戦略を決定します。 (「はい」の特定の要件が、展開戦略; に必要なことを示します"No"を意味の特定の要件が、展開戦略に必要ないこと。)  
  
このテーブルは、このガイドで説明したように、3 つのプライマリの AD DS 展開戦略だけを参照します。  
  
-   [新しい組織で AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 組織で AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows 2000 組織で AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
ただし、組織のニーズを満たすために AD DS の設計とデプロイの要件の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD DS 展開戦略を作成できます。  
  
|AD DS の設計とデプロイの要件|新しい組織の AD DS の展開|Windows Server 2003 組織への AD DS の展開|Windows Server 2000 組織への AD DS の展開|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008 AD DS の論理構造の設計](https://technet.microsoft.com/library/cc770806.aspx)|〇|〇|〇|  
|[Windows Server 2008 AD DS のサイト トポロジの設計](Designing-the-Site-Topology.md)|〇|〇|〇|  
|ドメイン コント ローラーの処理能力の計画|〇|〇|〇|  
|[Windows Server 2008 フォレスト ルート ドメインを展開します。](https://technet.microsoft.com/library/cc731174.aspx)|〇|X|X|  
|[Windows Server 2008 地域ドメインの展開](https://technet.microsoft.com/library/cc755118.aspx)|〇|〇|〇|  
|[AD DS の高度な機能を有効にします。](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|〇|[はい] が、環境内のすべてのドメイン コント ローラーは、Windows Server 2008 へのドメインまたはフォレスト機能レベルを設定する前に Windows Server 2008 を実行する必要があります。|[はい] が、環境内のすべてのドメイン コント ローラーは、Windows Server 2008 へのドメインまたはフォレスト機能レベルを設定する前に Windows Server 2008 を実行する必要があります。|  
|[Windows Server 2008 および Windows Server 2008 R2 の AD DS ドメインを Active Directory ドメインのアップグレード](https://technet.microsoft.com/library/cc731188.aspx)|X|〇|〇|  
|[フォレスト間での AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=93678)|はい、パイロットのドメインを運用環境に移行する場合は、別の組織とマージし、2 つの情報技術 (IT) インフラストラクチャを統合または統合 Windows からのインプレース アップグレードするリソースとアカウントのドメイン2000 または Windows Server 2003 環境にします。|はい、別の組織とのマージし 2 つの IT インフラストラクチャの統合、または Windows 2000 または Windows Server 2003 環境からのインプレース アップグレードするリソースとアカウントのドメインを統合する場合です。|はい、別の組織とのマージし 2 つの IT インフラストラクチャの統合、または Windows 2000 または Windows Server 2003 環境からのインプレース アップグレードするリソースとアカウントのドメインを統合する場合です。|  
|[フォレスト内の AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=82740))|X|はい、ドメインの数を減らす必要がある場合は、レプリケーション トラフィックと、必要なユーザーとグループの管理の量を減らすか、グループ ポリシーの管理を簡略化します。|はい、ドメインの数を減らす必要がある場合は、レプリケーション トラフィックと、必要なユーザーとグループの管理の量を減らすか、グループ ポリシーの管理を簡略化します。|  
  


