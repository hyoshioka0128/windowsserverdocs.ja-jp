---
ms.assetid: ce3be131-06ad-41dc-a26b-1168fa68c8ed
title: AD DS の展開戦略に要件をマッピングする
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 412e1ccb13b4d92801faf019b1ed6d01eff8b8d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402536"
---
# <a name="mapping-your-requirements-to-an-ad-ds-deployment-strategy"></a>AD DS の展開戦略に要件をマッピングする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) の設計と展開の要件を確認して特定し、特定の展開に関連付けられているものを特定したら、それらの要件を特定の AD DS の展開にマップできます。選択肢.  
  
次の表を使用して、組織の AD DS の設計と展開の要件の適切な組み合わせに対応する AD DS 展開方法を決定します。 ("Yes" は、展開戦略に特定の要件が必要であることを意味します。"いいえ" は、展開戦略に特定の要件が必要ないことを意味します)。  
  
次の表は、このガイドで説明されている3つの主要な AD DS デプロイ方法のみを示しています。  
  
-   [新しい組織の AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-New-Organization.md)  
  
-   [Windows Server 2003 組織への AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-Server-2003-Organization.md)  
  
-   [Windows Server 2000 組織への AD DS の展開](../../ad-ds/plan/Deploying-AD-DS-in-a-Windows-2000-Organization.md)  
  
ただし、組織のニーズを満たすために、AD DS の設計と展開の要件の任意の組み合わせを使用して、ハイブリッドまたはカスタムの AD DS 展開戦略を作成することができます。  
  
|AD DS の設計と展開の要件|新しい組織の AD DS の展開|Windows Server 2003 組織への AD DS の展開|Windows Server 2000 組織への AD DS の展開|  
|--------------------------------------------|-----------------------------------------|---------------------------------------------------------|--------------------------------------------------|  
|[Windows Server 2008 の論理構造の設計 AD DS](https://technet.microsoft.com/library/cc770806.aspx)|はい|[はい]|はい|  
|[Windows Server 2008 用のサイトトポロジの設計 AD DS](Designing-the-Site-Topology.md)|はい|[はい]|はい|  
|ドメイン コント ローラーの処理能力の計画|はい|[はい]|はい|  
|[Windows Server 2008 フォレストルートドメインの展開](https://technet.microsoft.com/library/cc731174.aspx)|はい|いいえ|いいえ|  
|[Windows Server 2008 の地域ドメインの展開](https://technet.microsoft.com/library/cc755118.aspx)|はい|[はい]|はい|  
|[AD DS の高度な機能を有効にする](../../ad-ds/plan/Enabling-Advanced-Features-for-AD-DS.md)|はい|はい。ただし、ドメインまたはフォレストの機能レベルを Windows Server 2008 に設定する前に、環境内のすべてのドメインコントローラーが Windows Server 2008 を実行している必要があります。|はい。ただし、ドメインまたはフォレストの機能レベルを Windows Server 2008 に設定する前に、環境内のすべてのドメインコントローラーが Windows Server 2008 を実行している必要があります。|  
|[Active Directory ドメインを Windows Server 2008 および Windows Server 2008 R2 AD DS ドメインにアップグレードする](https://technet.microsoft.com/library/cc731188.aspx)|いいえ|はい|はい|  
|[フォレスト間での AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=93678)|はい。パイロットドメインを運用環境に移行する場合は、別の組織と統合して、2つの情報技術 (IT) インフラストラクチャを統合するか、Windows からアップグレードしたリソースとアカウントのドメインを統合します。2000または Windows Server 2003 の環境。|はい。別の組織と統合して、2つの IT インフラストラクチャを統合する場合、または、アップグレードしたリソースとアカウントドメインを Windows 2000 または Windows Server 2003 環境から統合する場合に使用します。|はい。別の組織と統合して、2つの IT インフラストラクチャを統合する場合、または、アップグレードしたリソースとアカウントドメインを Windows 2000 または Windows Server 2003 環境から統合する場合に使用します。|  
|[フォレスト内の AD DS ドメインの再構築](https://go.microsoft.com/fwlink/?LinkId=82740))|いいえ|はい。ドメインの数を減らす必要がある場合は、レプリケーションのトラフィックと必要なユーザーとグループの管理の量を減らし、グループポリシーの管理を簡略化します。|はい。ドメインの数を減らす必要がある場合は、レプリケーションのトラフィックと必要なユーザーとグループの管理の量を減らし、グループポリシーの管理を簡略化します。|  
  


