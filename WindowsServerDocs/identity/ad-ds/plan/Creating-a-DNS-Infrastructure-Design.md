---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: DNS インフラストラクチャの設計を作成する
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b4b7cea18a6bb6b435b3c3fb6b4e94cfdddb2c04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408974"
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS インフラストラクチャの設計を作成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フォレストとドメインの設計を作成した後、Active Directory 論理構造をサポートするために、ドメインネームシステム (DNS) インフラストラクチャを設計する必要があります。 DNS を使用すると、ユーザーは覚えやすいわかりやすい名前を使用して、IP ネットワーク上のコンピューターやその他のリソースに接続できます。 Windows Server 2008 の Active Directory Domain Services (AD DS) には DNS が必要です。  
  
AD DS をサポートするように DNS を設計するプロセスは、既存の DNS サーバーサービスが組織に既に存在するか、または新しい DNS サーバーサービスを展開するかによって異なります。  
  
- 既存の DNS インフラストラクチャが既に存在する場合は、その環境に Active Directory 名前空間を統合する必要があります。 詳細については、「 [AD DS を既存の DNS インフラストラクチャに統合する](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)」を参照してください。  
- DNS インフラストラクチャが配置されていない場合は、AD DS をサポートするために新しい DNS インフラストラクチャを設計および展開する必要があります。 詳細については、「[ドメインネームシステム (DNS) の展開](https://go.microsoft.com/fwlink/?LinkId=93656)」を参照してください。  
  
組織に既存の DNS インフラストラクチャがある場合は、DNS インフラストラクチャが Active Directory 名前空間とどのように対話するかを理解しておく必要があります。 既存の DNS インフラストラクチャ設計を文書化するのに役立つワークシートについては、「 [Windows Server 2003 Deployment Kit のジョブエイド](https://go.microsoft.com/fwlink/?LinkID=102558)」から Job_Aids_Designing_and_Deploying_Directory_and_Security_Services をダウンロードし、「DNS インベントリ」を開きます (DSSLOGI_8)。  
  
> [!NOTE]  
> Windows Server では、IP version 4 (IPv4) アドレスに加えて、IP version 6 (IPv6) アドレスもサポートしています。 現在の DNS 構造の再帰的な名前解決方法を文書化しながら、IPv6 アドレスの一覧を作成するのに役立つワークシートについては、「[Appendix A:DNS インベントリ @ no__t-0。
  
AD DS をサポートするように DNS インフラストラクチャを設計する前に、dns 階層、DNS 名前解決プロセス、および DNS が AD DS をサポートする方法について理解しておくことをお勧めします。 DNS 階層と名前解決プロセスの詳細については、DNS のテクニカルリファレンス ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145)) を参照してください。 DNS が AD DS をサポートする方法の詳細については、「Active Directory テクニカルリファレンスの DNS サポート ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147))」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  

- [DNS の概念を確認する](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
- [DNS と AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
- [AD DS の DNS の所有者の役割を割り当てる](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
- [AD DS を既存の DNS インフラストラクチャに統合する](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
