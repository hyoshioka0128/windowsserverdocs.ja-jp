---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: フォレスト ルート ドメイン コントローラーの配置を計画する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 57eafcc884a827d98c249e2da0c0af6888abc5b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823643"
---
# <a name="planning-forest-root-domain-controller-placement"></a>フォレスト ルート ドメイン コントローラーの配置を計画する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ドメイン以外の独自のリソースにアクセスする必要があるクライアントの信頼のパスを作成するには、フォレスト ルート ドメイン コント ローラーが必要です。 ハブの場所とデータ センターをホストする場所では、フォレスト ルート ドメイン コント ローラーを配置します。 指定された場所にユーザーが同じ場所、他のドメインからリソースにアクセスする必要があり、データ センターとユーザーの場所の間のネットワークの可用性が信頼性の高い、場所にフォレスト ルート ドメイン コント ローラーを追加するかを作成します。2 つのドメイン間にショートカット信頼。 フォレスト ルート ドメイン コント ローラーをその場所に配置するには、その他の理由がない限り、ドメイン間のショートカットの信頼を作成する経済的になります。  
  
ショートカットは、いずれかのドメインにあるユーザーからの認証要求を最適化するためにヘルプを信頼します。 ドメイン間でのショートカットの信頼の詳細については、記事を参照してください。 [Understanding When to Create a Shortcut Trust](https://go.microsoft.com/fwlink/?LinkId=107061)します。  
  
フォレスト ルート ドメイン コント ローラーの配置を文書化するために、ワークシートでは、次を参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロード。、「ドメイン コント ローラー配置」(DSSTOPO_4.doc) を開きます。  
  
フォレスト ルート ドメインを作成するときに、この情報を参照する必要があります。 フォレスト ルート ドメインの展開に関する詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
