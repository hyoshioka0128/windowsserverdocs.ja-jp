---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: "フォレスト ルート ドメイン コントローラーの配置を計画します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 374ce31c61c666302e2b00a8f365c289cb8799f8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="planning-forest-root-domain-controller-placement"></a>フォレスト ルート ドメイン コントローラーの配置を計画します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメイン以外の独自のリソースにアクセスする必要があるクライアントの信頼のパスを作成するには、フォレスト ルート ドメイン コントローラーが必要です。 ハブの場所、およびデータ センターをホストしている場所では、フォレスト ルート ドメイン コントローラーを配置します。 指定の場所でユーザーが、同じ場所に他のドメインからリソースにアクセスする必要があります、データ センターとユーザーの場所の間でネットワークの可用性の信頼性が低い場合は、いずれかフォレスト ルート ドメイン コントローラーを場所に追加したり、2 つのドメイン間のショートカットの信頼を作成できます。 コストをフォレスト ルート ドメイン コントローラーをその場所に配置するには、他の理由がない限り、ドメイン間でショートカットの信頼を作成する効率を実現することをお勧めします。  
  
ショートカットは、いずれかのドメインにあるユーザーから行われる認証要求を最適化するためにヘルプを信頼します。 ドメイン間でショートカットの信頼に関する詳細についてを参照してください、ショートカットの信頼を作成する場合 ([https://go.microsoft.com/fwlink/?LinkId=107061](https://go.microsoft.com/fwlink/?LinkId=107061))。  
  
フォレスト ルート ドメイン コントローラーの配置を文書化するためのワークシートで、ジョブ エイドの Windows Server 2003 導入ガイドを参照してください ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))、ダウンロードJob_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip、および「ドメイン コントローラー配置」(DSSTOPO_4.doc) を開きます。  
  
フォレスト ルート ドメインを作成するときに、この情報を参照する必要があります。 フォレスト ルート ドメインの展開に関する詳細については、次を参照してください。[Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  


