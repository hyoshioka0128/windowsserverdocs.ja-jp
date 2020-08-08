---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: DNS インフラストラクチャの設計を作成する
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: b96f0b5fd47fc4a7d4d1fe6d68fcfa1543108d3f
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947860"
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS インフラストラクチャの設計を作成する

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フォレストとドメインの設計を作成した後、Active Directory 論理構造をサポートするために、ドメインネームシステム (DNS) インフラストラクチャを設計する必要があります。 DNS を使用すると、ユーザーは覚えやすいわかりやすい名前を使用して、IP ネットワーク上のコンピューターやその他のリソースに接続できます。 Windows Server 2008 の Active Directory Domain Services (AD DS) には DNS が必要です。

AD DS をサポートするように DNS を設計するプロセスは、既存の DNS サーバーサービスが組織に既に存在するか、または新しい DNS サーバーサービスを展開するかによって異なります。

- 既存の DNS インフラストラクチャが既に存在する場合は、その環境に Active Directory 名前空間を統合する必要があります。 詳細については、「 [AD DS を既存の DNS インフラストラクチャに統合する](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)」を参照してください。
- DNS インフラストラクチャが配置されていない場合は、AD DS をサポートするために新しい DNS インフラストラクチャを設計および展開する必要があります。 詳細については、「[ドメインネームシステム (DNS) の展開](/previous-versions/windows/it-pro/windows-server-2003/cc780661(v=ws.10))」を参照してください。

組織に既存の DNS インフラストラクチャがある場合は、DNS インフラストラクチャが Active Directory 名前空間とどのように対話するかを理解しておく必要があります。 既存の DNS インフラストラクチャ設計を文書化するのに役立つワークシートについては、「 [Windows Server 2003 Deployment Kit のジョブエイド](https://microsoft.com/download/details.aspx?id=9608)」から Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードし、「dns インベントリ」 (DSSLOGI_8.doc) を開いてください。

> [!NOTE]
> Windows Server では、IP version 4 (IPv4) アドレスに加えて、IP version 6 (IPv6) アドレスもサポートしています。 現在の DNS 構造の再帰的な名前解決方法を文書化しながら、IPv6 アドレスの一覧を作成するためのワークシートについては、「[付録 a: Dns インベントリ](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)」を参照してください。

AD DS をサポートするように DNS インフラストラクチャを設計する前に、dns 階層、DNS 名前解決プロセス、および DNS が AD DS をサポートする方法について理解しておくことをお勧めします。 DNS 階層と名前解決プロセスの詳細については、「 [Dns テクニカルリファレンス](/previous-versions/windows/it-pro/windows-server-2003/cc779926(v=ws.10))」を参照してください。 DNS が AD DS をサポートする方法の詳細については、「 [Active Directory テクニカルリファレンスの Dns サポート](/previous-versions/windows/it-pro/windows-server-2003/cc781627(v=ws.10))」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

- [DNS の概念を確認する](../../ad-ds/plan/Reviewing-DNS-Concepts.md)
- [DNS と AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)
- [AD DS の DNS の所有者の役割を割り当てる](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)
- [AD DS を既存の DNS インフラストラクチャに統合する](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)
