---
title: 企業でのリモート アクセスの展開
description: このトピックでは、エンタープライズ向け Windows Server 2016 での DirectAccess のシナリオの概要を説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4781df0a-158b-4562-b8f5-32b27615a4f8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cbcc844c356978f5bb5f34b66aa36dec9b163c1
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283002"
---
# <a name="deploy-remote-access-in-an-enterprise"></a>企業でのリモート アクセスの展開

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、企業向けの DirectAccess のシナリオについて説明します。  
  
  
> [!IMPORTANT]  
> このガイドを使用して DirectAccess を展開するには、Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 を実行している DirectAccess サーバーを使用する必要があります。  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>展開を開始する前に、サポートされない構成、既知の問題、前提条件のリストを参照してください  
  
-   [DirectAccess のサポートされない構成](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-unsupported-configurations)  
  
-   [DirectAccess の既知の問題](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-known-issues)  
  
-   [DirectAccess の展開の前提条件) の前提条件](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/prerequisites-for-deploying-directaccess)  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
リモート アクセスは、Windows ネットワーク負荷分散 (NLB) または外部のロード バランサーを使用して負荷分散するクラスターへの複数のリモート アクセス サーバーの展開、リモート アクセス サーバーが地理的に離れた場所に設置されているマルチサイト展開のセットアップ、ワンタイム パスワード (OTP) を使用してクライアントの 2 要素認証を行う DirectAccess の展開など、さまざまなエンタープライズ機能を備えています。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
各エンタープライズ シナリオについては、計画と展開の手順を含むドキュメントで説明します。 詳しくは、次のトピックをご覧ください。  
  
-   [クラスターのリモート アクセスを展開します。](cluster/Deploy-Remote-Access-In-Cluster.md)  
  
-   [マルチサイト展開での複数のリモート アクセス サーバーの展開](multisite/Deploy-Multiple-Remote-Access-Servers-in-a-Multisite-Deployment.md)  
  
-   [OTP 認証を使用するリモート アクセスの展開](otp/Deploy-RA-OTP.md)  
  
-   [マルチ フォレスト環境でのリモート アクセスを展開します。](multi-forest/Deploy-Remote-Access-in-a-Multi-Forest-Environment.md)  
  
## <a name="BKMK_APP"></a>実際の適用  
リモート アクセスのエンタープライズ シナリオでは、次のことが実現されます。  
  
-   **可用性を向上させる**します。 クラスター内の複数のリモート アクセス サーバーを展開し、スケーラビリティを提供します、スループットとユーザーの数の容量が増加します。 クラスターの負荷を分散することで、高可用性が実現されます。 クラスター内のサーバーで障害が発生しても、リモート ユーザーはクラスター内の別のサーバーを経由して企業内部ネットワークに引き続きアクセスすることができます。 クラスターは仮想 IP (VIP) アドレスを使用してクラスターに接続するため、フェールオーバーは透過的です。  
  
-   **容易な管理**します。 クラスターまたはマルチサイト展開を構成およびクラスター サーバーのいずれかで実行されているリモート アクセス管理コンソールを使用して 1 つのエンティティとして管理します。 また、マルチサイト展開により、管理者はリモート アクセス展開を Active Directory サイトに配置して、アーキテクチャを簡素化することができます。 クラスター サーバー全体やすべてのマルチサイト エントリ ポイント サーバーで共有設定を簡単に設定できます。 リモート アクセス設定をクラスターまたは展開内の任意のサーバーから管理することや、リモート サーバー管理ツール (RSAT) を使用してリモートで管理することができます。 また、単一のリモート アクセス管理コンソールから、クラスターまたはマルチサイト展開全体を監視できます。  
  
-   **コスト効率**します。 リモート アクセスのマルチサイト展開により、クライアントの場所に対応する複数のサイトにリモート アクセス サーバーをデプロイする企業です。 これにより、場所に関係なくリモート クライアントのアクセス環境が予測可能になり、インターネット経由のクライアント トラフィックを最も近いリモート アクセス サーバーにルーティングすることでコストとイントラネットの帯域幅が削減されます。  
  
-   **セキュリティ**。 標準の Active Directory パスワードの代わりに、ワンタイム パスワード (OTP) での強力なクライアント認証を展開すると、セキュリティが向上します。  
  
## <a name="BKMK_NEW"></a>役割と機能がこのシナリオに含まれる  
次の表に、このエンタープライズ シナリオで使用する役割と機能を示します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセス サーバーの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービスの両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />1. DirectAccess およびルーティングとリモート アクセス サービス (RRAS) VPN DirectAccess と VPN は、リモート アクセス管理コンソールでまとめて管理します。<br />2. RRAS ルーティング RRAS ルーティング機能は、従来のルーティングとリモート アクセス コンソールで管理されます。<br /><br />リモート アクセス サーバーの役割は、次のサーバーの機能に依存しています。<br /><br />-インターネット インフォメーション サービス (IIS) - この機能は、ネットワーク ロケーション サーバーおよび既定の web プローブを構成するために必要です。<br />-グループ ポリシー管理コンソールの機能 - 機能は作成して Active Directory でグループ ポリシー オブジェクト (Gpo) の管理の DirectAccess に必要であり、サーバーの役割に必要な機能としてインストールする必要があります。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-は、リモート アクセスの役割がインストールされているし、リモート管理コンソールのユーザー インターフェイスをサポートしているときに、既定でリモート アクセス サーバーにインストールされます。<br />-は、リモート アクセス サーバーの役割が実行されていないサーバーで必要に応じてインストールすることができます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />1. リモート アクセス GUI およびコマンド ライン ツール<br />2. Windows PowerShell 用のリモート アクセス モジュール<br /><br />次の要素と依存関係があります。<br /><br />1. グループ ポリシー管理コンソール<br />2. RAS 接続マネージャー管理キット (CMAK)<br />3.Windows PowerShell 3.0<br />4。グラフィカル管理ツールとインフラストラクチャ|  
|Windows NLB|この機能を使用すると、複数のリモート アクセス サーバーの負荷を分散できます。|  
  

  


