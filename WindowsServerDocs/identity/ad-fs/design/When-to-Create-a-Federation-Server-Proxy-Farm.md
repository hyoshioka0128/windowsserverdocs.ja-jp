---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: フェデレーション サーバー プロキシ ファームを作成するのに適した状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 247daf1b9b49124188f6bb16bce7da381fe997ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402429"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>フェデレーション サーバー プロキシ ファームを作成するのに適した状況

大規模な Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t のデプロイを使用していて、フォールトトレランスを提供し、no__t の負荷を分散し、プロキシ展開のためにスケーラビリティを確保する場合は、追加のフェデレーションサーバープロキシをインストールすることを検討してください。 同じ境界ネットワーク内に複数のフェデレーションサーバープロキシを作成し、それぞれを同じ AD FS を保護するように構成するとフェデレーションサービスフェデレーションサーバープロキシファームが作成されます。  
  
AD FS フェデレーションサーバープロキシ構成ウィザードを使用して、フェデレーションサーバープロキシファームを作成するか、既存のファームに追加のフェデレーションサーバープロキシをインストールすることができます。 詳細については、次を参照してください。[フェデレーション サーバー プロキシを作成するときに](When-to-Create-a-Federation-Server-Proxy.md)します。  
  
すべてのフェデレーションサーバープロキシをファームとして機能させるには、まず、1つの IP アドレスと1つのドメインネームシステム \(DNS @ no__t-1 完全修飾ドメイン名 \( FQDN @ no__t の下にクラスターをクラスター化する必要があります。 Microsoft ネットワーク負荷分散 \(NLB @ no__t-1 を境界ネットワーク内に展開することによって、サーバーをクラスター化することができます。 次の表のタスクでは、ファーム内のフェデレーションサーバープロキシをクラスター化するために NLB が適切に構成されている必要があります。  
  
Microsoft NLB テクノロジを使用してクラスターの FQDN を構成する方法の詳細については、「[クラスターパラメーターの指定](https://go.microsoft.com/fwlink/?linkid=74651)」を参照してください。  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>ファーム用のフェデレーション サーバー プロキシの構成  
次の表では、各フェデレーションサーバープロキシがファームに参加できるようにするために完了する必要があるタスクについて説明します。  
  
|タスク|説明|  
|--------|---------------|  
|ファーム内のすべてのプロキシが同じ AD FS フェデレーションサービス名を指すようにする|フェデレーションサーバープロキシを作成する場合は、ファームに参加するすべてのフェデレーションサーバープロキシに対して、AD FS フェデレーションサーバープロキシ構成ウィザードで同じフェデレーションサービス名を入力する必要があります。 フェデレーションサーバープロキシは、この DNS ホスト名を構成する URL を使用して、接続先の AD FS フェデレーションサービスインスタンスを決定します。<br /><br />詳細については、次を参照してください。 [、フェデレーション サーバー プロキシ ロール用コンピューターの構成](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。|  
|証明書を取得して共有する|パブリック証明機関 (たとえば VeriSign) からサーバー認証証明書を取得し、すべてのフェデレーションサーバープロキシが同じ同じ秘密キー部分を共有するように証明書を構成することができ @no__t各フェデレーションサーバープロキシの既定の Web サイトの証明書。 証明書を共有するには、各フェデレーションサーバープロキシの既定の Web サイトに同じサーバー認証証明書をインストールする必要があります。 詳細については、「[サーバー認証証明書を既定の Web サイトにインポートする](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)」を参照してください。<br /><br />詳細については、次を参照してください。[フェデレーション サーバー プロキシの証明書要件](Certificate-Requirements-for-Federation-Server-Proxies.md)します。|  
  
新しいフェデレーションサーバープロキシを追加してフェデレーションサーバープロキシファームを作成する方法の詳細については、「@no__t」を参照してください。フェデレーションサーバープロキシのセットアップ @ no__t-0  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
