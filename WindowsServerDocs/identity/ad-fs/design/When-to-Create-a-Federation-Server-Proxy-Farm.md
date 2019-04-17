---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: "フェデレーション サーバー プロキシ ファームを作成する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8935760cad272d5b82edb675cda85caf0456565f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>フェデレーション サーバー プロキシ ファームを作成する場合

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

大規模な Active Directory フェデレーション サービス \(AD FS\) 展開があるし、プロキシ展開用のフォールト トレランス、load\ 分散、およびスケーラビリティを提供するその他のフェデレーション サーバー プロキシのインストールを検討してください。 同じ境界ネットワーク内の 2 つ以上のフェデレーション サーバー プロキシを作成し、同じ AD FS フェデレーション サービスを保護するように構成するのでは、フェデレーション サーバー プロキシ ファームを作成します。  
  
フェデレーション サーバー プロキシ ファームを作成したり、AD FS フェデレーション サーバー プロキシ構成ウィザードを使用して、既存のファームに追加のフェデレーション サーバー プロキシをインストールすることができます。 詳細については、次を参照してください。[When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md)します。  
  
すべてのフェデレーション サーバー プロキシは、ファームとして機能させることができます、前にする必要があります最初にクラスター化下にある 1 つの IP アドレスと 1 つのドメイン ネーム システム \(DNS\) 完全修飾ドメイン名 \(FQDN\) します。 境界ネットワーク内の Microsoft Network Load Balancing \(NLB\) を展開することにより、サーバーをクラスターことができます。 次の表に、タスクでは、NLB は、ファーム内のフェデレーション サーバー プロキシをクラスターに適切に構成する必要があります。  
  
Microsoft の NLB テクノロジを使用してクラスターの FQDN を構成する方法の詳細については、次を参照してください。[クラスター パラメーターを指定して](https://go.microsoft.com/fwlink/?linkid=74651)します。  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>ファームのフェデレーション サーバー プロキシを構成します。  
次の表では、各フェデレーション サーバー プロキシは、ファームに参加できるように、完了する必要があるタスクについて説明します。  
  
|タスク|説明|  
|--------|---------------|  
|同じの AD FS フェデレーション サービス名をポイントして、ファーム内のすべてのプロキシ|フェデレーション サーバー プロキシを作成する場合は、ファームに参加するすべてのフェデレーション サーバー プロキシの AD FS フェデレーション サーバー プロキシ構成ウィザードで同じフェデレーション サービス名を入力してください。 フェデレーション サーバー プロキシを構成する先の AD FS フェデレーション サービス インスタンスをこの DNS ホスト名、連絡先、URL を使用します。<br /><br />詳細については、次を参照してください。[for Federation Server Proxy Role Configure a Computer](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。|  
|取得し、証明書の共有|パブリック証明機関から、サーバー認証証明書を取得できます \ (CA\) —、VeriSign-すべてのフェデレーション サーバー プロキシは、各フェデレーション サーバー プロキシの既定の Web サイトで同じ証明書の同じ秘密キー部分を共有できるようにし、証明書を構成します。 証明書を共有するには、各フェデレーション サーバー プロキシの既定の Web サイトで同じサーバー認証証明書をインストールする必要があります。 詳細については、次を参照してください。[既定の Web サイトにサーバー認証証明書をインポート](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)します。<br /><br />詳細については、次を参照してください。[フェデレーション サーバー プロキシの証明書の要件](Certificate-Requirements-for-Federation-Server-Proxies.md)します。|  
  
フェデレーション サーバー プロキシ ファームを作成する新しいフェデレーション サーバー プロキシを追加する方法の詳細については、次を参照してください。[チェックリスト: 設定をフェデレーション サーバー プロキシの](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
