---
title: 作業の開始ウィザードを使用した単一の DirectAccess サーバーの展開
description: このトピックは、作業の開始ウィザードの Windows Server 2016 を使用して単一の DirectAccess サーバー展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb0cf464-0668-40f8-8222-feb6bae6d3d5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: deb220ad5ee83e2849f962c588d6150892d990d6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281791"
---
# <a name="deploy-a-single-directaccess-server-using-the-getting-started-wizard"></a>作業の開始ウィザードを使用した単一の DirectAccess サーバーの展開

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、単一の DirectAccess サーバーを使用し、短い簡単な手順で DirectAccess を展開できる、DirectAccess のシナリオについて説明します。  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>展開を開始する前に、サポートされない構成、既知の問題、前提条件のリストを参照してください  
次のトピックを使用すると、DirectAccess を展開する前に、前提条件とその他の情報を確認します。  
  
-   [DirectAccess のサポートされない構成](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [DirectAccess の展開の前提条件](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
このようなインフラストラクチャ設定を構成する必要はありません、いくつかの簡単なウィザードの手順で既定の設定で DirectAccess サーバーとしてこのシナリオで Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 では、いずれかを実行している 1 台のコンピューターが構成されています。証明機関 (CA) または Active Directory セキュリティ グループ。  
  
> [!NOTE]  
> 設定をカスタマイズして高度な展開を構成する場合は、「 [Deploy a Single DirectAccess Server with Advanced Settings](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」を参照してください。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
基本的な DirectAccess サーバーを設定するには、いくつかの計画と展開手順が必要です。  
  
### <a name="prerequisites"></a>前提条件  
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。  
  
-   すべてのプロファイルで Windows ファイアウォールが有効になっている必要があります。  
  
-   このシナリオは、Windows 10、Windows 8.1 または Windows 8 クライアント コンピューターが実行されている場合にのみサポートされます。  
  
-   企業ネットワーク内での ISATAP はサポートしていません。 ISATAP を使用している場合は、これを削除し、ネイティブ IPv6 を使用する必要があります。  
  
-   公開キー基盤は必要ありません。  
  
-   2 要素認証を展開する場合はサポートされません。 認証にはドメインの資格情報が必要です。  
  
-   現在のドメインのすべてのモバイル コンピューターに DirectAccess を自動的に展開します。  
  
-   インターネットへのトラフィックは、DirectAccess トンネルを通過しません。 強制トンネルの構成はサポートされません。  
  
-   DirectAccess サーバーは、ネットワーク ロケーション サーバーです。  
  
-   ネットワーク アクセス保護 (NAP) はサポートされていません。  
  
-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットを使用しないポリシーの変更はサポートされていません。  
  
-   マルチサイトを展開する、現在または今後は、まず[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。  
  
### <a name="planning-steps"></a>計画の手順  
計画は 2 つのフェーズに分かれています。  
  
1.  DirectAccess インフラストラクチャを計画します。 このフェーズでは、DirectAccess 展開を開始する前に設定する必要があるネットワーク インフラストラクチャの計画について説明します。 これには、ネットワークとサーバーのトポロジ、DirectAccess ネットワーク ロケーション サーバーの計画が含まれます。  
  
2.  DirectAccess 展開を計画します。 このフェーズでは、DirectAccess 展開の準備に必要な計画手順について説明します。 これには、DirectAccess クライアント コンピューター、サーバーとクライアントの認証要件、VPN の設定、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの計画が含まれます。  
  
詳細な計画手順を参照してください。[高度な DirectAccess 展開を計画](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md)します。  
  
### <a name="deployment-steps"></a>展開の手順  
展開は 3 つのフェーズに分かれています。  
  
1.  DirectAccess インフラストラクチャこのフェーズを構成するネットワークを構成し、ルーティング、必要に応じて、証明書、DNS サーバー、Active Directory および GPO 設定、および DirectAccess ネットワークの場所を構成する場合、ファイアウォール設定の構成が含まれています。サーバー。  
  
2.  DirectAccess サーバーの設定を構成します。 このフェーズでは、DirectAccess クライアント コンピューター、DirectAccess サーバー、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの構成を行います。  
  
3.  展開を検証しています。 このフェーズには、必要に応じて、展開が動作していることを確認する手順が含まれています。  
  
詳細な展開手順については、「 [Install and Configure Basic DirectAccess](../../../remote-access/directaccess/single-server-wizard/Install-and-Configure-Basic-DirectAccess.md)」を参照してください。  
  
## <a name="BKMK_APP"></a>実際の適用  
単一のリモート アクセス サーバーを展開すると、次のことが実現されます。  
  
-   アクセスの容易さ。 DirectAccess クライアントとして Windows 10、Windows 8.1、Windows 8、Windows 7、またはを実行している管理されたクライアント コンピューターを構成することができます。 そうしたクライアントは、インターネット上に存在しているときは、VPN 接続にログインしなくても、DirectAccess を経由して内部ネットワーク リソースにアクセスできます。 これらのオペレーティング システムを搭載していないクライアント コンピューターは、従来の VPN 接続を使用して内部ネットワークに接続できます。  
  
-   容易な管理。 リモート アクセス管理者は、クライアント コンピューターが企業内部ネットワーク上に存在しない場合でも、インターネット上に存在する DirectAccess クライアント コンピューターを DirectAccess 経由でリモート管理できます。 企業の要件を満たしていないクライアント コンピューターを管理サーバーによって自動的に修正できます。 DirectAccess と VPN は両方とも同じコンソールで管理され、同じウィザードを使用します。 さらに、単一のリモート アクセス管理コンソールから 1 台以上のリモート アクセス サーバーを管理できます。  
  
## <a name="BKMK_NEW"></a>役割と機能がこのシナリオに含まれる  
次の表に、このシナリオに必要な役割と機能を示します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセスの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールまたは Windows PowerShell を使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービスの両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />1. DirectAccess およびルーティングとリモート アクセス サービス (RRAS) VPN です。 DirectAccess と VPN は、リモート アクセス管理コンソールで一緒に管理します。<br />2. RRAS ルーティングします。 RRAS ルーティング機能は、従来のルーティングとリモート アクセス コンソールで管理されます。<br /><br />リモート アクセス サーバーの役割は、次のサーバーの役割や機能に依存しています。<br /><br />-インターネット インフォメーション サービス (IIS) Web サーバー - この機能は、リモート アクセス サーバーおよび既定の web プローブで、ネットワーク ロケーション サーバーを構成するために必要です。<br />-Windows Internal Database。 リモート アクセス サーバーでのローカル アカウンティングに使用されます。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-は、リモート アクセスの役割がインストールされているし、リモート管理コンソールのユーザー インターフェイスと Windows PowerShell コマンドレットをサポートしているときに、既定でリモート アクセス サーバーにインストールされます。<br />-は、リモート アクセス サーバーの役割が実行されていないサーバーで必要に応じてインストールすることができます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモート アクセス GUI<br />の Windows PowerShell 用リモート アクセス モジュール<br /><br />次の要素と依存関係があります。<br /><br />グループ ポリシー管理コンソール<br />RAS 接続マネージャー管理キット (CMAK)<br />-   Windows PowerShell 3.0<br />グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   サーバーの要件:  
  
    -   Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 のハードウェア要件を満たすコンピューター。  
  
    -   サーバーには、少なくとも 1 つのネットワーク アダプターがあり、有効にされて内部ネットワークに接続されている必要があります。 アダプターを 2 つ使用する場合は、一方を企業内部ネットワークに接続し、もう一方を外部ネットワーク (インターネットまたはプライベート ネットワーク) に接続します。  
  
    -   少なくとも 1 つのドメイン コントローラー。 リモート アクセス サーバーと DirectAccess クライアントはドメインのメンバーである必要があります。  
  
-   クライアントの要件:  
  
    -   クライアント コンピューターでは、Windows 10、Windows 8.1 または Windows 8 が実行されている必要があります。  
  
        > [!IMPORTANT]  
        > 一部またはすべてのクライアント コンピューターが Windows 7 を実行している場合は、高度なセットアップ ウィザードを使用する必要があります。 このドキュメントで説明されている開始セットアップ作業ウィザードは、Windows 7 を実行しているクライアント コンピューターをサポートしていません。 参照してください[詳細設定を使用する単一の DirectAccess サーバーをデプロイ](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)DirectAccess を Windows 7 クライアントを使用する方法についてはします。  
  
        > [!NOTE]  
        > DirectAccess クライアントとして使用できるオペレーティング システムは、Windows 10 Enterprise、Windows 8.1 Enterprise、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows 8 Enterprise、Windows Server 2008 R2、Windows 7 Enterprise、および Windows 7 Ultimate。  
  
-   インフラストラクチャと管理サーバーの要件:  
  
    -   VPN が有効になっていて、静的 IP アドレス プールが構成されていない場合は、VPN クライアントに IP アドレスを自動的に割り当てるために DHCP サーバーを展開する必要があります。  
  
-   Windows Server 2016 を実行している DNS サーバー、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 SP2、または Windows Server 2008 R2 が必要です。  
  
## <a name="BKMK_SOFT"></a>ソフトウェアの要件  
このシナリオには、さまざまな要件があります。  
  
-   サーバーの要件:  
  
    -   リモート アクセス サーバーはドメイン メンバーである必要があります。 サーバーは、内部ネットワークのエッジに展開することも、エッジ ファイアウォールまたは他のデバイスの内側に配置することもできます。  
  
    -   リモート アクセス サーバーがエッジ ファイアウォール内または NAT デバイスの内側に配置されている場合は、リモート アクセス サーバーとの間で送受信されるトラフィックを許可するようにデバイスを構成する必要があります。  
  
    -   サーバーにリモート アクセスを展開する担当者には、サーバーに対するローカルの管理者のアクセス許可およびドメイン ユーザーのアクセス許可が必要です。 また、管理者には DirectAccess 展開で使用される GPO に対するアクセス許可も必要です。 DirectAccess 展開をモバイル コンピューターのみに制限する機能を利用するには、ドメイン コントローラーで WMI フィルターを作成するアクセス許可が必要です。  
  
-   リモート アクセス クライアントの要件:  
  
    -   DirectAccess クライアントは、ドメイン メンバーである必要があります。 クライアントが含まれているドメインは、リモート アクセス サーバーと同じフォレストに属することや、リモート アクセス サーバーのフォレストと双方向の信頼を確立することができます。  
  
    -   DirectAccess クライアントとして構成するコンピューターが属する Active Directory セキュリティ グループが必要です。 DirectAccess クライアントの設定の構成時にセキュリティ グループを指定しなかった場合、既定では、Domain Computers セキュリティ グループのすべてのノート PC にクライアントの GPO が適用されます。 DirectAccess クライアントとして使用できるオペレーティング システムは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows 8 Enterprise、Windows 7 Enterprise、および Windows 7 Ultimate。  
  
## <a name="BKMK_LINKS"></a>参照してください。  
次の表に、関連リソースへのリンクを示します。  
  
|コンテンツの種類|参考資料|  
|--------|-------|  
|**TechNet 上のリモート アクセス**|[リモート アクセス TechCenter](https://technet.microsoft.com/network/bb545655.aspx)|  
|**ツールと設定**|[リモート アクセス PowerShell コマンドレット](https://technet.microsoft.com/library/hh918399.aspx)|  
|**コミュニティ リソース**|[DirectAccess の Wiki エントリ](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**関連テクノロジ**|[IPv6 の動作方法](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


