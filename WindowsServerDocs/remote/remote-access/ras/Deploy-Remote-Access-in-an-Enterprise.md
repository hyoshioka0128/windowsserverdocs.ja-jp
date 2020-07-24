---
title: 企業でのリモート アクセスの展開
description: このトピックでは、企業向けの Windows Server 2016 の DirectAccess シナリオの概要について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 4781df0a-158b-4562-b8f5-32b27615a4f8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0cf216cb785d01ed08bb3a4490b25d4c4549b1c4
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965594"
---
# <a name="deploy-remote-access-in-an-enterprise"></a>企業でのリモート アクセスの展開

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、企業向けの DirectAccess のシナリオについて説明します。  
  
  
> [!IMPORTANT]  
> このガイドを使用して DirectAccess を展開するには、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行している DirectAccess サーバーを使用する必要があります。  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>展開を開始する前に、サポートされない構成、既知の問題、前提条件の一覧を参照してください  
  
-   [DirectAccess のサポートされない構成](../directaccess/directaccess-unsupported-configurations.md)  
  
-   [DirectAccess の既知の問題](../directaccess/directaccess-known-issues.md)  
  
-   [DirectAccess を展開するための前提条件) の前提条件](../directaccess/prerequisites-for-deploying-directaccess.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>シナリオの説明  
リモート アクセスは、Windows ネットワーク負荷分散 (NLB) または外部のロード バランサーを使用して負荷分散するクラスターへの複数のリモート アクセス サーバーの展開、リモート アクセス サーバーが地理的に離れた場所に設置されているマルチサイト展開のセットアップ、ワンタイム パスワード (OTP) を使用してクライアントの 2 要素認証を行う DirectAccess の展開など、さまざまなエンタープライズ機能を備えています。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
各エンタープライズ シナリオについては、計画と展開の手順を含むドキュメントで説明します。 詳細については、次を参照してください。  
  
-   [クラスターへのリモートアクセスの展開](cluster/Deploy-Remote-Access-In-Cluster.md)  
  
-   [マルチサイト展開での複数のリモート アクセス サーバーの展開](multisite/Deploy-Multiple-Remote-Access-Servers-in-a-Multisite-Deployment.md)  
  
-   [OTP 認証を使用するリモート アクセスの展開](otp/Deploy-RA-OTP.md)  
  
-   [マルチフォレスト環境でのリモートアクセスの展開](multi-forest/Deploy-Remote-Access-in-a-Multi-Forest-Environment.md)  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例  
リモート アクセスのエンタープライズ シナリオでは、次のことが実現されます。  
  
-   **可用性の向上**。 クラスターに複数のリモートアクセスサーバーを展開すると、スケーラビリティが実現され、スループットとユーザー数の容量が増加します。 クラスターの負荷を分散することで、高可用性が実現されます。 クラスター内のサーバーで障害が発生しても、リモート ユーザーはクラスター内の別のサーバーを経由して企業内部ネットワークに引き続きアクセスすることができます。 クラスターは仮想 IP (VIP) アドレスを使用してクラスターに接続するため、フェールオーバーは透過的です。  
  
-   **簡単に管理**できます。 クラスターまたはマルチサイト展開は、いずれかのクラスターサーバーで実行されているリモートアクセス管理コンソールを使用して、単一のエンティティとして構成および管理できます。 また、マルチサイト展開により、管理者はリモート アクセス展開を Active Directory サイトに配置して、アーキテクチャを簡素化することができます。 クラスター サーバー全体やすべてのマルチサイト エントリ ポイント サーバーで共有設定を簡単に設定できます。 リモート アクセス設定をクラスターまたは展開内の任意のサーバーから管理することや、リモート サーバー管理ツール (RSAT) を使用してリモートで管理することができます。 また、単一のリモート アクセス管理コンソールから、クラスターまたはマルチサイト展開全体を監視できます。  
  
-   **コスト効率**。 リモートアクセスのマルチサイト展開により、企業はクライアントの場所に対応する複数のサイトにリモートアクセスサーバーを展開することができます。 これにより、場所に関係なくリモート クライアントのアクセス環境が予測可能になり、インターネット経由のクライアント トラフィックを最も近いリモート アクセス サーバーにルーティングすることでコストとイントラネットの帯域幅が削減されます。  
  
-   **セキュリティ**。 標準 Active Directory パスワードの代わりにワンタイムパスワード (OTP) を使用して強力なクライアント認証を展開すると、セキュリティが強化されます。  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>このシナリオに含まれている役割と機能  
次の表に、このエンタープライズ シナリオで使用する役割と機能を示します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセス サーバーの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービスの両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<p>1. DirectAccess およびルーティングとリモートアクセスサービス (RRAS) VPN-DirectAccess と VPN は、リモートアクセス管理コンソールで一緒に管理されます。<br />2. RRAS ルーティング-RRAS ルーティング機能は、従来のルーティングとリモートアクセスコンソールで管理されます。<p>リモート アクセス サーバーの役割は、次のサーバーの機能に依存しています。<p>-インターネットインフォメーションサービス (IIS)-この機能は、ネットワークロケーションサーバーと既定の web プローブを構成するために必要です。<br />-グループポリシー管理コンソール機能-DirectAccess で Active Directory でグループポリシーオブジェクト (Gpo) を作成および管理するために必要な機能であり、サーバーの役割に必要な機能としてインストールする必要があります。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<p>-リモートアクセスの役割をインストールするときに、リモートアクセスサーバーに既定でインストールされ、リモート管理コンソールのユーザーインターフェイスをサポートします。<br />-必要に応じて、リモートアクセスサーバーの役割を実行していないサーバーにインストールできます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<p>リモート アクセス管理ツールの機能は、次の要素で構成されています。<p>1. リモートアクセス GUI およびコマンドラインツール<br />2. Windows PowerShell 用リモートアクセスモジュール<p>次の要素と依存関係があります。<p>1. グループポリシー管理コンソール<br />2. RAS 接続マネージャー管理キット (CMAK)<br />3. Windows PowerShell 3.0<br />4. グラフィカルな管理ツールとインフラストラクチャ|  
|Windows NLB|この機能を使用すると、複数のリモート アクセス サーバーの負荷を分散できます。|  
  

  
