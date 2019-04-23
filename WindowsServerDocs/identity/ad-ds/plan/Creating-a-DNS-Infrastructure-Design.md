---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: DNS インフラストラクチャの設計を作成する
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 080c36f8410be4d6b1933c74730e2b55ce8d0a0b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856133"
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS インフラストラクチャの設計を作成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フォレストおよびドメイン設計を作成した後は、Active Directory 論理構造をサポートするためにドメイン ネーム システム (DNS) インフラストラクチャを設計する必要があります。 DNS は、コンピュータおよび IP ネットワーク上の他のリソースへの接続に覚えやすいフレンドリ名を使用することができます。 Active Directory Domain Services (AD DS) で Windows Server 2008 では、DNS が必要です。  
  
AD DS をサポートするために DNS を設計するためのプロセスによって既存の DNS サーバー サービスが組織に既に異なりますか、新しい DNS サーバー サービスを展開します。  
  
- 既存の DNS インフラストラクチャは、既にある場合は、その環境に Active Directory 名前空間を統合する必要があります。 詳細については、次を参照してください。[既存の DNS インフラストラクチャに AD DS の統合](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)します。  
- インプレース DNS インフラストラクチャがいない場合は、設計し、AD DS をサポートするために、新しい DNS インフラストラクチャを展開する必要があります。 詳細については、次を参照してください。[を展開するドメイン ネーム システム (DNS)](https://go.microsoft.com/fwlink/?LinkId=93656)します。  
  
お客様の組織は、既存の DNS インフラストラクチャがある場合、は、Active Directory 名前空間に、DNS インフラストラクチャが対話する方法を理解することを確認する必要があります。 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードして、既存の DNS インフラストラクチャの設計を文書化するためのワークシート、[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)と「DNS インベントリ」(DSSLOGI_8.doc) を開きます。  
  
> [!NOTE]  
> に加えて IP バージョン 4 (IPv4) アドレス、IP バージョン 6 (IPv6) をサポートするもの Windows Server のアドレスします。 ワークシートで、現在の構造の DNS の再帰的名前解決方法を文書化中に、IPv6 アドレスを一覧表示を支援するためには、次を参照してください[付録 a:。DNS インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)します。
  
AD DS をサポートするために、DNS インフラストラクチャを設計する前に、DNS 階層、DNS 名前解決プロセス、および DNS が AD DS をサポートする方法について説明立つことができます。 DNS 階層と名前解決プロセスの詳細については、DNS のテクニカル リファレンスを参照してください ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145))。 DNS は AD DS をサポートする方法の詳細については、Active Directory に関するテクニカル リファレンスの DNS のサポートを参照して ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147))。  
  
## <a name="in-this-section"></a>このセクションの内容  

- [DNS の概念を確認します。](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
- [AD DS および DNS](../../ad-ds/plan/DNS-and-AD-DS.md)  
- [DNS の AD DS の所有者ロールの割り当てください。](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
- [既存の DNS インフラストラクチャへの AD DS の統合](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
