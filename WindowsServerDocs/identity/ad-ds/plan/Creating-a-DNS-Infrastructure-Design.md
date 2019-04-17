---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: "DNS インフラストラクチャの設計を作成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6e5093b05fd81a693cec87ddb00d39e70483df23
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS インフラストラクチャの設計を作成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フォレストおよびドメインのデザインを作成した後は、Active Directory 論理構造をサポートするために、ドメイン ネーム システム (DNS) インフラストラクチャを設計する必要があります。 DNS は、ユーザーはコンピューターおよび IP ネットワーク上の他のリソースへの接続に覚えやすいフレンドリ名を使用できるようにします。 Active Directory ドメイン サービス (AD DS) Windows Server 2008 では、DNS が必要です。  
  
AD DS をサポートするために DNS を設計するためのプロセスは、組織は既にが既存の DNS サーバー サービスを持つかどうかによって異なりますか、新しい DNS サーバー サービスを展開します。  
  
-   既存の DNS インフラストラクチャを既にある場合は場合、は、その環境に Active Directory 名前空間を統合する必要があります。 詳細については、次を参照してください。[を既存の DNS インフラストラクチャに AD DS の統合](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)します。  
  
-   配置に DNS インフラストラクチャがあるない場合は、設計し、AD DS をサポートするために、新しい DNS インフラストラクチャを展開する必要があります。 詳細については、展開のドメイン ネーム システム (DNS) を参照してください ([https://go.microsoft.com/fwlink/?LinkId=93656](https://go.microsoft.com/fwlink/?LinkId=93656))。  
  
組織に既存の DNS インフラストラクチャがある場合は、DNS インフラストラクチャが Active Directory 名前空間とどのように対話する方法を理解していることを確認する必要があります。 既存の DNS インフラストラクチャの設計を文書化するためのワークシート、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip ジョブ エイドの Windows Server 2003 導入ガイドから ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) と、「DNS インベントリ」(DSSLOGI_8.doc).  
  
> [!NOTE]  
> に加えて IP バージョン 4 (IPv4) アドレス、IP version 6 (IPv6) をサポートしているも Windows Server 2008 に対処します。 現在、DNS の構造体の再帰的名前解決の方法を文書化中に IPv6 アドレスを一覧表示するためのワークシートで、次を参照してください。[付録 a: DNS インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)します。  
  
AD DS をサポートするために、DNS インフラストラクチャを設計する前に、DNS の階層、DNS 名前解決の処理、および DNS が AD DS をサポートする方法に関する情報を読む役に立つができます。 DNS の階層と名前解決プロセスの詳細については、DNS のテクニカル リファレンスを参照してください ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145))。 DNS が AD DS をサポートする方法の詳細については、Active Directory のテクニカル リファレンスの DNS のサポートを参照してください ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147))。  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [DNS の概念を確認します。](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
  
-   [DNS と AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
  
-   [AD DS の所有者の役割用の DNS の割り当てください。](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
  
-   [AD DS を既存の DNS インフラストラクチャに統合します。](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
  


