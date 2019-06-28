---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: フェデレーション サーバー プロキシ ファームを作成するのに適した状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c33475d7420383448439e2b769562e55127c7b0e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190632"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>フェデレーション サーバー プロキシ ファームを作成するのに適した状況

大規模な Active Directory フェデレーション サービスがある場合、追加のフェデレーション サーバー プロキシのインストールを検討\(AD FS\)展開し、フォールト トレランス、負荷を\-分散、およびスケーラビリティをプロキシの展開。 同じ境界ネットワーク内の 2 つ以上のフェデレーション サーバー プロキシを作成し、それぞれ同じ AD FS フェデレーション サービスを保護するための構成は、フェデレーション サーバー プロキシ ファームを作成します。  
  
フェデレーション サーバー プロキシ ファームを作成したり、AD FS フェデレーション サーバー プロキシ構成ウィザードを使用して、既存のファームに追加のフェデレーション サーバー プロキシをインストールすることができます。 詳細については、次を参照してください。[フェデレーション サーバー プロキシを作成するときに](When-to-Create-a-Federation-Server-Proxy.md)します。  
  
すべてのフェデレーション サーバー プロキシとして機能させるファームを前にする必要がありますまずクラスター化する 1 つの IP アドレスと 1 つのドメイン ネーム システム\(DNS\)完全修飾ドメイン名\(FQDN\)します。 Microsoft ネットワーク負荷分散を展開することで、サーバーをクラスター化できる\(NLB\)境界ネットワーク内で。 次の表に、タスクでは、NLB クラスターのファームにフェデレーション サーバー プロキシを適切に構成する必要があります。  
  
Microsoft の NLB テクノロジを使用してクラスターの FQDN を構成する方法の詳細については、次を参照してください。[クラスター パラメーターの指定](https://go.microsoft.com/fwlink/?linkid=74651)します。  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>ファーム用のフェデレーション サーバー プロキシの構成  
次の表では、各フェデレーション サーバー プロキシがファームに参加できるように、完了する必要があるタスクについて説明します。  
  
|タスク|説明|  
|--------|---------------|  
|ファーム内のすべてのプロキシをポイントして、同じ AD FS フェデレーション サービス名|フェデレーション サーバー プロキシを作成するときは、ファームに参加するすべてのフェデレーション サーバー プロキシの AD FS フェデレーション サーバー プロキシ構成ウィザードで、同じフェデレーション サービス名を入力してください。 フェデレーション サーバー プロキシを構成する先の AD FS フェデレーション サービス インスタンスを判断するこの DNS ホスト名、連絡先 URL を使用します。<br /><br />詳細については、次を参照してください。 [、フェデレーション サーバー プロキシ ロール用コンピューターの構成](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。|  
|証明書を取得して共有する|公開証明機関から、サーバー認証証明書を取得できます\(CA\)—、VeriSign-すべてのフェデレーション サーバー プロキシの同じ秘密キー部分を共有できるように、証明書を構成し、各フェデレーション サーバー プロキシの既定の Web サイトで同じ証明書。 証明書を共有するには、各フェデレーション サーバー プロキシの既定の Web サイトで同じサーバー認証証明書をインストールする必要があります。 詳細については、次を参照してください。[既定の Web サイトにサーバー認証証明書をインポート](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)します。<br /><br />詳細については、次を参照してください。[フェデレーション サーバー プロキシの証明書要件](Certificate-Requirements-for-Federation-Server-Proxies.md)します。|  
  
フェデレーション サーバー プロキシ ファームを作成する新しいフェデレーション サーバー プロキシを追加する方法の詳細については、次を参照してください。[チェックリスト。フェデレーション サーバー プロキシを設定する](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
