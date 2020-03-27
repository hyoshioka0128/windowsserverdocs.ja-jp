---
title: 作業の開始ウィザードを使用した単一の DirectAccess サーバーの展開
description: このトピックは、「Windows Server 2016 用はじめにウィザードを使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb0cf464-0668-40f8-8222-feb6bae6d3d5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c37ed120b811cd86dd70580d31cff18f2c330677
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309062"
---
# <a name="deploy-a-single-directaccess-server-using-the-getting-started-wizard"></a>作業の開始ウィザードを使用した単一の DirectAccess サーバーの展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、単一の DirectAccess サーバーを使用し、短い簡単な手順で DirectAccess を展開できる、DirectAccess のシナリオについて説明します。  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>展開を開始する前に、サポートされない構成、既知の問題、前提条件のリストを参照してください  
DirectAccess を展開する前に、次のトピックを使用して、前提条件とその他の情報を確認できます。  
  
-   [DirectAccess のサポートされない構成](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [DirectAccess の展開の前提条件](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>シナリオの説明  
このシナリオでは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 のいずれかを実行している1台のコンピューターを、ウィザードの簡単な手順で既定の設定を使用して DirectAccess サーバーとして構成します。たとえば、インフラストラクチャの設定を構成する必要はありません。証明機関 (CA) または Active Directory セキュリティグループとして。  
  
> [!NOTE]  
> 設定をカスタマイズして高度な展開を構成する場合は、「 [Deploy a Single DirectAccess Server with Advanced Settings](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」を参照してください。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
基本的な DirectAccess サーバーを設定するには、いくつかの計画と展開の手順を実行する必要があります。  
  
### <a name="prerequisites"></a>前提条件  
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。  
  
-   すべてのプロファイルで Windows ファイアウォールが有効になっている必要があります。  
  
-   このシナリオは、クライアントコンピューターで Windows 10、Windows 8.1、または Windows 8 が実行されている場合にのみサポートされます。  
  
-   企業ネットワーク内での ISATAP はサポートしていません。 ISATAP を使用している場合は、これを削除し、ネイティブ IPv6 を使用する必要があります。  
  
-   公開キー基盤は必要ありません。  
  
-   2 要素認証を展開する場合はサポートされません。 認証にはドメインの資格情報が必要です。  
  
-   現在のドメインのすべてのモバイル コンピューターに DirectAccess を自動的に展開します。  
  
-   インターネットへのトラフィックは、DirectAccess トンネルを通過しません。 強制トンネルの構成はサポートされません。  
  
-   DirectAccess サーバーは、ネットワーク ロケーション サーバーです。  
  
-   ネットワーク アクセス保護 (NAP) はサポートされていません。  
  
-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットを使用しないポリシーの変更はサポートされていません。  
  
-   現在、または今後、マルチサイトを展開するには、まず、[詳細設定を使用して単一の DirectAccess サーバーを展開](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。  
  
### <a name="planning-steps"></a>計画の手順  
計画は 2 つのフェーズに分かれています。  
  
1.  DirectAccess インフラストラクチャの計画。 このフェーズでは、DirectAccess 展開を開始する前に設定する必要があるネットワーク インフラストラクチャの計画について説明します。 これには、ネットワークとサーバーのトポロジ、DirectAccess ネットワーク ロケーション サーバーの計画が含まれます。  
  
2.  DirectAccess 展開の計画。 このフェーズでは、DirectAccess 展開の準備に必要な計画手順について説明します。 これには、DirectAccess クライアント コンピューター、サーバーとクライアントの認証要件、VPN の設定、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの計画が含まれます。  
  
詳細な計画手順については、「[高度な DirectAccess 展開を計画する](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md)」を参照してください。  
  
### <a name="deployment-steps"></a>展開の手順  
展開は 3 つのフェーズに分かれています。  
  
1.  DirectAccess インフラストラクチャの構成-このフェーズには、ネットワークとルーティングの構成、ファイアウォール設定の構成 (必要な場合)、証明書、DNS サーバー、Active Directory と GPO 設定、および DirectAccess ネットワークの場所の構成が含まれます。server.  
  
2.  DirectAccess サーバーの設定を構成しています。 このフェーズでは、DirectAccess クライアント コンピューター、DirectAccess サーバー、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの構成を行います。  
  
3.  デプロイを検証しています。 このフェーズには、展開が必要に応じて動作していることを確認するための手順が含まれています。  
  
詳細な展開手順については、「 [Install and Configure Basic DirectAccess](../../../remote-access/directaccess/single-server-wizard/Install-and-Configure-Basic-DirectAccess.md)」を参照してください。  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>実用的なアプリケーション  
単一のリモート アクセス サーバーを展開すると、次のことが実現されます。  
  
-   簡単にアクセスできます。 Windows 10、Windows 8.1、Windows 8、または Windows 7 を実行する管理されたクライアントコンピューターを DirectAccess クライアントとして構成できます。 そうしたクライアントは、インターネット上に存在しているときは、VPN 接続にログインしなくても、DirectAccess を経由して内部ネットワーク リソースにアクセスできます。 これらのオペレーティング システムを搭載していないクライアント コンピューターは、従来の VPN 接続を使用して内部ネットワークに接続できます。  
  
-   簡単に管理できます。 リモート アクセス管理者は、クライアント コンピューターが企業内部ネットワーク上に存在しない場合でも、インターネット上に存在する DirectAccess クライアント コンピューターを DirectAccess 経由でリモート管理できます。 企業の要件を満たしていないクライアント コンピューターを管理サーバーによって自動的に修正できます。 DirectAccess と VPN は両方とも同じコンソールで管理され、同じウィザードを使用します。 さらに、単一のリモート アクセス管理コンソールから 1 台以上のリモート アクセス サーバーを管理できます。  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>このシナリオに含まれる役割と機能  
次の表に、このシナリオに必要な役割と機能を示します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセスの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールまたは Windows PowerShell を使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービスの両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />1. DirectAccess およびルーティングとリモートアクセスサービス (RRAS) VPN。 DirectAccess と VPN は、リモートアクセス管理コンソールで一緒に管理されます。<br />2. RRAS ルーティング。 RRAS ルーティング機能は、従来のルーティングとリモートアクセスコンソールで管理されます。<br /><br />リモート アクセス サーバーの役割は、次のサーバーの役割や機能に依存しています。<br /><br />-インターネットインフォメーションサービス (IIS) Web サーバー: この機能は、リモートアクセスサーバー上のネットワークロケーションサーバーと既定の Web プローブを構成するために必要です。<br />-Windows Internal Database。 リモート アクセス サーバーでのローカル アカウンティングに使用されます。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-リモートアクセスの役割をインストールするときに、リモートアクセスサーバーに既定でインストールされ、リモート管理コンソールのユーザーインターフェイスと Windows PowerShell コマンドレットをサポートします。<br />-必要に応じて、リモートアクセスサーバーの役割を実行していないサーバーにインストールできます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモートアクセス GUI<br />-Windows PowerShell 用リモートアクセスモジュール<br /><br />次の要素と依存関係があります。<br /><br />-グループポリシー管理コンソール<br />-RAS 接続マネージャー管理キット (CMAK)<br />-Windows PowerShell 3.0<br />-グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   サーバーの要件:  
  
    -   Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 のハードウェア要件を満たすコンピューター。  
  
    -   サーバーには、少なくとも 1 つのネットワーク アダプターがあり、有効にされて内部ネットワークに接続されている必要があります。 アダプターを 2 つ使用する場合は、一方を企業内部ネットワークに接続し、もう一方を外部ネットワーク (インターネットまたはプライベート ネットワーク) に接続します。  
  
    -   少なくとも 1 つのドメイン コントローラー。 リモート アクセス サーバーと DirectAccess クライアントはドメインのメンバーである必要があります。  
  
-   クライアントの要件:  
  
    -   クライアントコンピューターでは、Windows 10、Windows 8.1、または Windows 8 が実行されている必要があります。  
  
        > [!IMPORTANT]  
        > 一部またはすべてのクライアントコンピューターで Windows 7 を実行している場合は、セットアップの詳細ウィザードを使用する必要があります。 このドキュメントに記載されているはじめにセットアップウィザードでは、Windows 7 を実行しているクライアントコンピューターはサポートされません。 DirectAccess で Windows 7 クライアントを使用する方法については[、詳細設定を使用した単一の Directaccess サーバーの展開](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)に関する説明を参照してください。  
  
        > [!NOTE]  
        > DirectAccess クライアントとして使用できるオペレーティングシステムは、Windows 10 Enterprise、Windows 8.1 Enterprise、Windows Server 2016、Windows Server 2012 R2、windows Server 2012、Windows 8 Enterprise、Windows Server 2008 R2、Windows 7 Enterprise、およびの各オペレーティングシステムのみです。Windows 7 Ultimate。  
  
-   インフラストラクチャと管理サーバーの要件:  
  
    -   VPN が有効になっていて、静的 IP アドレス プールが構成されていない場合は、VPN クライアントに IP アドレスを自動的に割り当てるために DHCP サーバーを展開する必要があります。  
  
-   Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 SP2、または Windows Server 2008 R2 を実行している DNS サーバーが必要です。  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件  
このシナリオには、さまざまな要件があります。  
  
-   サーバーの要件:  
  
    -   リモート アクセス サーバーはドメイン メンバーである必要があります。 サーバーは、内部ネットワークのエッジに展開することも、エッジ ファイアウォールまたは他のデバイスの内側に配置することもできます。  
  
    -   リモート アクセス サーバーがエッジ ファイアウォール内または NAT デバイスの内側に配置されている場合は、リモート アクセス サーバーとの間で送受信されるトラフィックを許可するようにデバイスを構成する必要があります。  
  
    -   サーバーにリモート アクセスを展開する担当者には、サーバーに対するローカルの管理者のアクセス許可およびドメイン ユーザーのアクセス許可が必要です。 また、管理者には DirectAccess 展開で使用される GPO に対するアクセス許可も必要です。 DirectAccess 展開をモバイル コンピューターのみに制限する機能を利用するには、ドメイン コントローラーで WMI フィルターを作成するアクセス許可が必要です。  
  
-   リモート アクセス クライアントの要件:  
  
    -   DirectAccess クライアントは、ドメイン メンバーである必要があります。 クライアントが含まれているドメインは、リモート アクセス サーバーと同じフォレストに属することや、リモート アクセス サーバーのフォレストと双方向の信頼を確立することができます。  
  
    -   DirectAccess クライアントとして構成するコンピューターが属する Active Directory セキュリティ グループが必要です。 DirectAccess クライアントの設定の構成時にセキュリティ グループを指定しなかった場合、既定では、Domain Computers セキュリティ グループのすべてのノート PC にクライアントの GPO が適用されます。 DirectAccess クライアントとして使用できるオペレーティングシステムは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows 8 Enterprise、Windows 7 Enterprise、および Windows 7 Ultimate だけです。  
  
## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目  
次の表に、関連リソースへのリンクを示します。  
  
|コンテンツの種類|参照|  
|--------|-------|  
|**TechNet のリモートアクセス**|[リモートアクセス TechCenter](https://technet.microsoft.com/network/bb545655.aspx)|  
|**ツールと設定**|[リモートアクセスの PowerShell コマンドレット](https://technet.microsoft.com/library/hh918399.aspx)|  
|**コミュニティ リソース**|[DirectAccess の Wiki エントリ](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**関連テクノロジ**|[IPv6 のしくみ](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


