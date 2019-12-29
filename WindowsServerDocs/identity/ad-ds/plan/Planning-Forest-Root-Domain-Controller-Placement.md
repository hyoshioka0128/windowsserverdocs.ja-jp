---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: フォレスト ルート ドメイン コントローラーの配置を計画する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e619d5f5e9cc317f9ba1548d5ed3a32e7bd12c2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402550"
---
# <a name="planning-forest-root-domain-controller-placement"></a>フォレスト ルート ドメイン コントローラーの配置を計画する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フォレストルートドメインコントローラーは、自身以外のドメインのリソースにアクセスする必要があるクライアントの信頼パスを作成するために必要です。 ハブの場所およびデータセンターをホストする場所に、フォレストルートドメインコントローラーを配置します。 特定の場所のユーザーが同じ場所にある他のドメインのリソースにアクセスする必要があり、データセンターとユーザーの場所の間のネットワークの可用性が信頼できない場合は、その場所にフォレストルートドメインコントローラーを追加するか、を作成します。2つのドメイン間のショートカットの信頼。 フォレストルートドメインコントローラーをその場所に配置する他の理由がない限り、ドメイン間にショートカットの信頼を作成する方がコスト効率が高くなります。  
  
ショートカットの信頼は、いずれかのドメインにあるユーザーからの認証要求を最適化するのに役立ちます。 ドメイン間のショートカットの信頼の詳細については、「[ショートカットの信頼を作成する場合](https://go.microsoft.com/fwlink/?LinkId=107061)」を参照してください。  
  
フォレストルートドメインコントローラーの配置を文書化するのに役立つワークシートについては、「 [Windows Server 2003 展開キット用のジョブエイド](https://go.microsoft.com/fwlink/?LinkID=102558)」、「Job_Aids_Designing_and_Deploying_Directory_and_Security_Services をダウンロードして、ドメインを開く」を参照してください。コントローラーの配置 "(DSSTOPO_4)。  
  
この情報は、フォレストのルートドメインを作成するときに参照する必要があります。 フォレストルートドメインの展開の詳細については、「 [Windows Server 2008 のフォレストルートドメインの展開](https://technet.microsoft.com/library/cc731174.aspx)」を参照してください。  
