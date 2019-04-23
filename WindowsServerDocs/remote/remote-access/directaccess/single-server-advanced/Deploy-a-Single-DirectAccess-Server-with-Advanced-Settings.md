---
title: 詳細設定を使用した単一の DirectAccess サーバーの展開
description: このトピックは高度な設定を Windows Server 2016 での単一の DirectAccess サーバー展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b211a9ca-1208-4e1f-a0fe-26a610936c30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 260926e4818ef95db85d00af02a4fa87665ad709
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864653"
---
# <a name="deploy-a-single-directaccess-server-with-advanced-settings"></a>詳細設定を使用した単一の DirectAccess サーバーの展開

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、単一の DirectAccess サーバーを使用し、高度な設定で DirectAccess を展開することができます DirectAccess のシナリオの概要を提供します。  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>展開を開始する前に、サポートされない構成、既知の問題、前提条件のリストを参照してください  
次のトピックを使用すると、DirectAccess を展開する前に、前提条件とその他の情報を確認します。  
  
-   [DirectAccess がサポートされていない構成](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [DirectAccess の展開の前提条件](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
このシナリオでは、Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 では、いずれかを実行している 1 台のコンピューターは高度な設定で DirectAccess サーバーとして構成されます。  
  
> [!NOTE]  
> 単純な設定のみを使用して基本的なデプロイを構成する場合は、「 [Deploy a Single DirectAccess Server Using the Getting Started Wizard](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)」を参照してください。 単純なシナリオでは、DirectAccess はウィザードで規定の設定を使用して構成され、証明機関 (CA) または Active Directory セキュリティ グループなどのインフラストラクチャ設定の構成は必要ありません。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
詳細設定を使用して単一の DirectAccess サーバーを設定するには、いくつかの計画と展開の手順を完了する必要があります。  
  
### <a name="prerequisites"></a>前提条件  
開始する前に、次の要件を確認してください。  
  
-   すべてのプロファイルで Windows ファイアウォールが有効になっている必要があります。  
  
-   DirectAccess サーバーは、ネットワーク ロケーション サーバーです。  
  
-   DirectAccess サーバーをインストールするドメインでは、すべてのワイヤレス コンピューターを DirectAccess 対応にします。 DirectAccess を展開すると、現在のドメインのすべてのモバイル コンピューターで DirectAccess が自動的に有効になります。  
  
> [!IMPORTANT]  
> 一部のテクノロジと構成は、DirectAccess を展開した時点ではサポートされていません。  
>   
> -   企業ネットワークで ISATAP (Intra-Site Automatic Tunnel Addressing Protocol) はサポートされていません。 ISATAP を使用している場合は、削除してネイティブ IPv6 を使用する必要があります。  
  
### <a name="planning-steps"></a>計画の手順  
計画は 2 つのフェーズに分かれています。  
  
1.  **DirectAccess インフラストラクチャの計画**: このフェーズでは、DirectAccess 展開を開始する前に設定する必要があるネットワーク インフラストラクチャの計画について説明します。 これには、ネットワークとサーバーのトポロジ、証明書の計画、DNS、Active Directory とグループ ポリシー オブジェクト (GPO) の構成、DirectAccess ネットワーク ロケーション サーバーの計画が含まれます。  
  
2.  **DirectAccess 展開の計画**: このフェーズでは、DirectAccess 展開の準備に必要な計画手順について説明します。 これには、DirectAccess クライアント コンピューター、サーバーとクライアントの認証要件、VPN の設定、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの計画が含まれます。  
  
### <a name="deployment-steps"></a>展開の手順  
展開は 3 つのフェーズに分かれています。  
  
1.  **DirectAccess インフラストラクチャの構成**: このフェーズでは、ネットワークとルーティングの構成、ファイアウォール設定の構成 (必要な場合)、証明書、DNS サーバー、Active Directory と GPO の設定、DirectAccess ネットワーク ロケーション サーバーの構成を行います。  
  
2.  **DirectAccess サーバー設定の構成**: このフェーズでは、DirectAccess クライアント コンピューター、DirectAccess サーバー、インフラストラクチャ サーバー、管理サーバーとアプリケーション サーバーの構成を行います。  
  
3.  **展開の確認**: このフェーズでは、DirectAccess 展開を確認します。  
  
展開の手順の詳細については、「[高度な DirectAccess のインストールと構成](../../../remote-access/directaccess/single-server-advanced/Install-and-Configure-Advanced-DirectAccess.md)」を参照してください。  
  
## <a name="BKMK_APP"></a>実際の適用  
単一の DirectAccess サーバーを展開すると、次のことが実現されます。  
  
-   **簡単操作**: Windows 10、Windows 8.1、Windows 8、および Windows 7 を実行している管理されたクライアント コンピューターは、DirectAccess クライアント コンピューターとして構成できます。 そうしたクライアントは、インターネット上に存在しているときは、VPN 接続にログインしなくても、DirectAccess を経由して内部ネットワーク リソースにアクセスできます。 これらのオペレーティング システムが実行されていないクライアント コンピューターは、VPN 経由で内部ネットワークに接続できます。  
  
-   **簡単な管理**: リモート アクセス管理者は、クライアント コンピューターが企業内部ネットワーク上に存在しない場合でも、インターネット上に存在する DirectAccess クライアント コンピューターを DirectAccess 経由でリモート管理できます。 企業の要件を満たしていないクライアント コンピューターを管理サーバーによって自動的に修正できます。 DirectAccess と VPN は両方とも同じコンソールで管理され、同じウィザードを使用します。 さらに、単一のリモート アクセス管理コンソールから 1 台以上の DirectAccess サーバーを管理できます。  
  
## <a name="BKMK_NEW"></a>役割と機能がこのシナリオに必要な  
次の表に、このシナリオに必要な役割と機能を示します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセスの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールまたは Windows PowerShell を使用します。 この役割には、DirectAccess サービス、ルーティングとリモート アクセス サービス (RRAS) が含まれます。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br/><br/>1. DirectAccess と RRAS VPN。 DirectAccess と VPN は、リモート アクセス管理コンソールで一緒に管理します。<br/>2. RRAS ルーティングします。 RRAS ルーティング機能は、従来のルーティングとリモート アクセス コンソールで管理されます。<br /><br />リモート アクセス サーバーの役割は、次のサーバーの役割や機能に依存しています。<br/><br/> -インターネット インフォメーション サービス (IIS) Web サーバー - この機能は、DirectAccess サーバーおよび既定の web プローブで、ネットワーク ロケーション サーバーを構成するために必要です。<br/> -Windows Internal Database。 DirectAccess サーバーでのローカル アカウンティングに使用されます。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-は、リモート アクセスの役割がインストールされているし、リモート管理コンソールのユーザー インターフェイスと Windows PowerShell コマンドレットをサポートしているときに、既定で DirectAccess サーバーにインストールされます。<br />-は、DirectAccess サーバーの役割が実行されていないサーバーで必要に応じてインストールすることができます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモート アクセス グラフィカル ユーザー インターフェイス (GUI)<br />の Windows PowerShell 用リモート アクセス モジュール<br /><br />次の要素と依存関係があります。<br /><br />グループ ポリシー管理コンソール<br />RAS 接続マネージャー管理キット (CMAK)<br />-   Windows PowerShell 3.0<br />グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   サーバーの要件:  
  
    -   Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 のハードウェア要件を満たすコンピューター。  
  
    -   サーバーには、少なくとも 1 つのネットワーク アダプターがあり、有効にされて内部ネットワークに接続されている必要があります。 アダプターを 2 つ使用する場合は、一方を企業内部ネットワークに接続し、もう一方を外部ネットワーク (インターネットまたはプライベート ネットワーク) に接続します。  
  
    -   IPv4 から IPv6 への移行プロトコルとして Teredo が必要な場合、サーバーの外部アダプターには連続する 2 つのパブリック IPv4 アドレスが必要です。 利用できる IP アドレスが 1 つの場合、移行プロトコルとして使用できるのは IP-HTTPS だけです。  
  
    -   少なくとも 1 つのドメイン コントローラー。 DirectAccess サーバーと DirectAccess クライアントはドメインのメンバーである必要があります。  
  
    -   IP-HTTPS またはネットワーク ロケーション サーバー用の自己署名証明書を使用しない場合、またはクライアントの IPsec 認証にクライアント証明書を使用する場合は、証明機関 (CA) が必要です。 あるいは、公的 CA に証明書を要求できます。  
  
    -   ネットワーク ロケーション サーバーが DirectAccess サーバーに配置されていない場合は、それを実行する別の Web サーバーが必要です。  
  
-   クライアントの要件:  
  
    -   クライアント コンピューターでは、Windows 10、Windows 8、または Windows 7 が実行されている必要があります。  
  
        > [!NOTE]  
        > 次のオペレーティング システムは、DirectAccess クライアントとして使用できます。Windows 10、Windows Server 2012 R2、Windows Server 2012、Windows 8 Enterprise、Windows 7 Enterprise、または Windows 7 Ultimate。  
  
-   インフラストラクチャと管理サーバーの要件:  
  
    -   DirectAccess クライアント コンピューターのリモート管理時に、クライアントは、Windows およびウイルス対策の更新、クライアントのネットワーク アクセス保護 (NAP) 準拠などのサービスのために管理サーバー (ドメイン コントローラー、System Center Configuration サーバー、正常性登録機関 (HRA) サーバーなど) と通信を開始します。 リモート アクセスの展開を開始する前に、必要なサーバーを展開する必要があります。  
  
    -   リモート アクセスでクライアントが NAP に準拠している必要がある場合は、リモート アクセスの展開を開始する前に、NPS および HRS サーバーを展開する必要があります。  
  
    -   VPN が有効になっており、静的アドレス プールを使用しない場合は、VPN クライアントに IP アドレスを自動的に割り当てるために DHCP サーバーが必要です。  
  
## <a name="BKMK_SOFT"></a>ソフトウェアの要件  
このシナリオには、さまざまな要件があります。  
  
-   サーバーの要件:  
  
    -   DirectAccess サーバーはドメイン メンバーである必要があります。 サーバーは、内部ネットワークのエッジに展開することも、エッジ ファイアウォールまたは他のデバイスの内側に配置することもできます。  
  
    -   DirectAccess サーバーがエッジ ファイアウォール内または NAT デバイスの内側に配置されている場合は、DirectAccess サーバーとの間で送受信されるトラフィックを許可するようにデバイスを構成する必要があります。  
  
    -   サーバーにリモート アクセスを展開する担当者には、サーバーに対するローカルの管理者のアクセス許可およびドメイン ユーザーのアクセス許可が必要です。 また、管理者には DirectAccess 展開で使用される GPO に対するアクセス許可も必要です。 DirectAccess 展開をモバイル コンピューターのみに制限する機能を利用するには、ドメイン コントローラーで WMI フィルターを作成するアクセス許可が必要です。  
  
-   リモート アクセス クライアントの要件:  
  
    -   DirectAccess クライアントは、ドメイン メンバーである必要があります。 クライアントが含まれているドメインは、DirectAccess サーバーと同じフォレストに属することや、DirectAccess サーバーのフォレストまたはドメインと双方向の信頼を確立することができます。  
  
    -   DirectAccess クライアントとして構成するコンピューターが属する Active Directory セキュリティ グループが必要です。 DirectAccess クライアントの設定の構成時にセキュリティ グループを指定しなかった場合、既定では、Domain Computers セキュリティ グループのすべてのノート PC にクライアントの GPO が適用されます。  
  
        > [!NOTE]  
        > DirectAccess クライアント コンピューターを含むそれぞれのドメインにセキュリティ グループを作成することをお勧めします。  
  
        > [!IMPORTANT]  
        > Windows 7 クライアントにアクセスできるように、いることを確認して、DirectAccess 展開で Teredo を有効にした場合、クライアントは、Windows 7 SP1 にアップグレードされます。 Windows 7 RTM を使用するクライアントは Teredo で接続できません。 ただし、これらのクライアントでも IP-HTTPS で企業ネットワークに接続することはできます。  
  
## <a name="BKMK_LINKS"></a>参照してください。  
次の表に、関連リソースへのリンクを示します。  
  
|コンテンツの種類|参考資料|  
|--------|-------|  
|**展開**|[Windows Server の DirectAccess 展開パス](../../../remote-access/directaccess/DirectAccess-Deployment-Paths-in-Windows-Server.md)<br /><br />[作業の開始ウィザードを使用して単一の DirectAccess サーバーの展開します。](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|  
|**ツールと設定**|[リモート アクセス PowerShell コマンドレット](https://technet.microsoft.com/library/hh918399.aspx)|  
|**コミュニティ リソース**|[DirectAccess サバイバル ガイド](https://social.technet.microsoft.com/wiki/contents/articles/23210.directaccess-survival-guide.aspx)<br /><br />[DirectAccess の Wiki エントリ](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**関連テクノロジ**|[IPv6 の動作方法](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


