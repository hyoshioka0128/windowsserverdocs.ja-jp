---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: "ドメイン名を割り当てる"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0d5ec9b76798f21503f650527a7961cff0b592b4
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="assigning-domain-names"></a>ドメイン名を割り当てる

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プランには、すべてのドメインに名前を指定する必要があります。 Active Directory ドメイン サービス (AD DS) ドメインがある 2 種類の名前: ドメイン ネーム システム (DNS) 名と NetBIOS 名。 一般に、両方の名前は、エンド ユーザーに表示されます。 Active Directory ドメインの DNS 名には、2 つの部分、プレフィックスおよびサフィックスが含まれます。 ドメイン名を作成する場合は、まず、DNS のプレフィックスを確認します。 これは、ドメインの DNS 名の最初のラベルです。 フォレスト ルート ドメインの名前を選択すると、サフィックスが決定されます。 次の表は、名前付け規則を DNS 名のプレフィックスを示します。  
  
|ルール|説明|  
|--------|---------------|  
|古くなる可能性が低いプレフィックスを選択します。|製品ラインや、今後変わる可能性があるオペレーティング システムなどの名前を回避します。 地理的な名を使用することをお勧めします。|  
|インターネット標準の文字のみを含むプレフィックスを選択します。|A ~ Z、a ~ z、0 ~ 9、および (-) が、数値がまったくないです。|  
|15 文字以内、プレフィックスのします。|15 文字以内にプレフィックスの長さを選択した場合、NetBIOS 名は、プレフィックスと同じです。|  
  
詳細については、コンピューター、ドメイン、サイト、および Ou の Active Directory 内の名前付け規則を参照してください ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629))。  
  
> [!NOTE]  
>  Windows Server 2008 および Windows Server 2003 の Dcpromo.exe には、単一ラベル DNS ドメイン名を作成することができます、いくつかの理由をドメインに単一ラベル DNS 名を使用する必要がありますできません。 Windows Server 2008 r2 で Dcpromo.exe できませんをドメインに単一ラベル DNS 名を作成できます。 詳細については、次を参照してください。[https://go.microsoft.com/fwlink/?LinkId=92467 します。](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
場合、現在の NetBIOS 名、ドメインを地域を表す適切ではありません、または、プレフィックスの命名規則を満たすことができない場合は、新しいプレフィックスを選択します。 この場合は、ドメインの NetBIOS 名は、ドメインの DNS プレフィックスとは異なるです。  
  
展開する新しいドメインごとに、地域に適した、プレフィックスの命名規則を満たす、プレフィックスを選択します。 ドメインの NetBIOS 名が DNS プレフィックスと同じであることをお勧めします。  
  
DNS プレフィックスと NetBIOS 名のフォレスト内の各ドメインに対して選択した文書化します。 ドメインの新しいとアップグレードの計画を文書化するために作成した「ドメインの計画」ワークシートに、DNS および NetBIOS 名の情報を追加できます。 開くにはを Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip ジョブ エイドの Windows Server 2003 導入ガイドから ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))「ドメインの計画」(DSSLOGI_5.doc (DSSLOGI_5.doc).  
  


