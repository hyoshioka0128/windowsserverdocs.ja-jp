---
title: 手順 2. 基本的な DirectAccess 展開を計画する
description: このトピックは、「Windows Server 2016 用はじめにウィザードを使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 546d722ed5e69f8c157e67c5eee728f5f5156abb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819335"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>手順 2. 基本的な DirectAccess 展開を計画する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

DirectAccess インフラストラクチャを計画した後、基本的な設定を使用して DirectAccess を1台のサーバーに展開する次の手順は、はじめにウィザードの設定を計画することです。  
  
|タスク|説明|  
|----|--------|  
|クライアント展開の計画|既定では、はじめにウィザードは、WMI フィルターをクライアント設定の GPO に適用して、ドメイン内のすべてのラップトップコンピューターおよびノートブックコンピューターに DirectAccess を展開します。|  
|DirectAccess サーバーの展開の計画|DirectAccess サーバーの展開方法を計画します。|  
  
## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>クライアント展開の計画  
クライアントの展開の計画時には 2 つの決定事項があります。  
  
1.  DirectAccess をモバイル コンピューターのみから使用できるようにするか、すべてのコンピューターから使用できるようにするか  
  
    はじめにウィザードで DirectAccess クライアントを構成するときに、指定したセキュリティグループのモバイルコンピューターのみに DirectAccess を使用した接続を許可するように選択できます。 モバイルコンピューターへのアクセスを制限すると、directaccess は、指定されたセキュリティグループ内のモバイルコンピューターのみに DirectAccess クライアント GPO が適用されるように、WMI フィルターを自動的に構成します。 DirectAccess 管理者には、この設定を有効にするために、グループポリシー WMI フィルターを作成または変更するためのアクセス許可が必要です。  
  
2.  どのセキュリティ グループに DirectAccess クライアント コンピューターを含めるか  
  
    DirectAccess 設定は DirectAccess クライアント GPO に含まれます。 GPO は、はじめにウィザードで指定したセキュリティグループの一部であるコンピューターに適用されます。 サポートされる任意のドメインに含まれるセキュリティ グループを指定できます。 DirectAccess を構成する前に、セキュリティグループを作成する必要があります。 DirectAccess の展開を完了した後で、コンピューターをセキュリティグループに追加できますが、別のドメインに存在するクライアントコンピューターをセキュリティグループに追加しても、クライアント GPO はこれらのクライアントに適用されません。 たとえば、ドメイン A に DirectAccess クライアント用の SG1 を作成し、後でドメイン B のクライアントをこのグループに追加した場合、クライアント GPO はドメイン B のクライアントに適用されません。この問題を回避するには、クライアント コンピューターを含むドメインごとに、新しいクライアント セキュリティ グループを作成します。 または新しいセキュリティ グループを作成しない場合は、新しいドメインに対して、新しい GPO の名前で Add-DAClient コマンドレットを実行します。  
  
## <a name="planning-for-directaccess-server-deployment"></a><a name="bkmk_2_2_server"></a>DirectAccess サーバーの展開の計画  
DirectAccess サーバーの展開を計画する際には、いくつかの決定を行う必要があります。  
  
-   **ネットワークトポロジ**-DirectAccess サーバーを展開するときに使用できるトポロジは2つあります。  
  
    -   **2**つのアダプター-2 つのネットワークアダプターがある場合、DirectAccess は、インターネットに直接接続された1つのネットワークアダプターを使用して構成でき、もう一方は内部ネットワークに接続されます。 または、サーバーをファイアウォールやルーターなどの境界デバイスの内側にインストールします。 この構成では、一方のネットワーク アダプターを境界ネットワークに接続し、他方を内部ネットワークに接続します。  
  
    -   **単一のネットワークアダプター** -この構成では、DirectAccess サーバーは、ファイアウォールやルーターなどのエッジデバイスの内側にインストールされます。 ネットワーク アダプターは内部ネットワークに接続します。  
  
-   **ネットワークアダプター** -directaccess ウィザードは、directaccess サーバーで構成されているネットワークアダプターを自動的に検出します。 **[レビュー]** ページで正しいアダプターが選択されていることを確認できます。  
  
-   **Ip-https 証明書**-この展開には PKI は必要ないため、ウィザードによって、Ip-https およびネットワークロケーションサーバー (証明書が存在しない場合) の自己署名入り証明書が自動的にプロビジョニングされ、Kerberos プロキシが自動的に有効になります。 また、このウィザードでは、IPv4 専用環境でのプロトコル変換のために NAT64 と DNS64 が有効になります。 ウィザードでは、構成の適用が完了したら、クリックして **閉じる**します。  
  
-   **Windows 7 クライアント**-はじめにウィザードを使用して windows 7 クライアントのサポートを有効にすることはできません。 これは、高度なセットアップウィザードで有効にすることができます。 詳細については、「[単一の DirectAccess サーバーを拡張設定で展開する](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)」を参照してください。  
  
-   **Vpn の構成**-DirectAccess を構成する前に、リモートクライアントへの VPN アクセスを提供するかどうかを決定します。 組織内に DirectAccess 接続をサポートしていないクライアントコンピューターがある場合 (管理されていない場合、または DirectAccess がサポートされていないオペレーティングシステムを実行している場合) は、VPN アクセスを提供する必要があります。 はじめにウィザードでは、DHCP を使用して VPN IP アドレスの割り当てを構成し、Active Directory を使用して VPN クライアントを認証するように構成します。  
  
-   **強制トンネリング**-強制トンネリングを使用する予定がある場合、または今後追加する可能性がある場合は、 [[詳細設定を使用して単一の DirectAccess サーバーを展開](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)する] を使用して2つのトンネル構成を展開する必要があります。 セキュリティ上の考慮事項により、単一のトンネル構成での強制トンネリングはサポートされていません。  
  
## <a name="previous-step"></a><a name="BKMK_Links"></a>前の手順  
  
-   [手順 1: 基本的な DirectAccess インフラストラクチャを計画する](da-basic-plan-s1-infrastructure.md)  
  


