---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: ドメイン名を割り当てる
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ba5a7ee8b7d9728c48e2798853aab8d55047e86f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866563"
---
# <a name="assigning-domain-names"></a>ドメイン名を割り当てる

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

計画のすべてのドメインに名前を割り当てる必要があります。 Active Directory Domain Services (AD DS) ドメインでは、2 種類の名前があります。ドメイン ネーム システム (DNS) 名と NetBIOS 名。 一般に、両方の名前は、エンドユーザーに表示されます。 Active Directory ドメインの DNS 名には、2 つの部分、プレフィックスおよびサフィックスが含まれます。 ドメイン名を作成する場合は、まず DNS プレフィックスを特定します。 これは、最初のラベルのドメインの DNS 名です。 フォレスト ルート ドメインの名前を選択すると、サフィックスが決定されます。 次の表では、名前付け規則を DNS 名のプレフィックスを示します。  
  
|ルール|説明|  
|--------|---------------|  
|期限切れになる可能性が高くないプレフィックスを選択します。|製品ラインや今後変わる可能性があるオペレーティング システムなどの名前を回避します。 地理的な名前を使用することをお勧めします。|  
|インターネットの標準的な文字のみを含むプレフィックスを選択します。|A ~ Z、a ~ z、0 ~ 9、および (-) がすべて数値ではありません。|  
|15 文字を含めるプレフィックス以下。|プレフィックス長に 15 文字以下の場合は、NetBIOS 名は、プレフィックスと同じです。|  
  
詳細については、コンピューター、ドメイン、サイト、および Ou の Active Directory 内の名前付け規則を参照してください ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629))。  
  
> [!NOTE]  
>  Windows Server 2008 および Windows Server 2003 の Dcpromo.exe を使用すれば、単一ラベル DNS ドメイン名を作成できますが、いくつかの理由からドメインに対しては単一ラベル DNS 名を使用しないでください。 Windows Server 2008 R2 では、Dcpromo.exe を使用して、ドメインに対して単一ラベル DNS 名を作成することはできません。 詳細については、次を参照してください。 [https://go.microsoft.com/fwlink/?LinkId=92467します。](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
ドメインの現在の NetBIOS 名は、リージョンを表す適切でないまたはプレフィックスの名前付け規則を満たすことができない、新しいプレフィックスを選択します。 ここでは、ドメインの NetBIOS 名が異なるドメインの DNS プレフィックスです。  
  
展開する新しいドメインごとに、プレフィックスの名前付け規則を満たす、リージョンの適切なプレフィックスを選択します。 ドメインの NetBIOS 名が DNS プレフィックスとして同じであることをお勧めします。  
  
DNS プレフィックスと、フォレスト内の各ドメインに対して選択した NetBIOS 名を文書化します。 DNS、NetBIOS 名の情報は、新規とアップグレード ドメインの計画を文書化するために作成する「ドメイン計画」ワークシートに追加できます。 開くには、ジョブ エイドの Windows Server 2003 展開キットから Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードします。 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))"ドメイン計画"(DSSLOGI_5.doc) を開きます。  
  


