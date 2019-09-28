---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: 境界ネットワークとインターネット クライアントの両方を対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 118c03ada32d3cd5b198ecd238078984a38df0db
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359835"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>境界ネットワークとインターネット クライアントの両方を対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


これにより、1つ以上のドメインネームシステム \(DNS @ no__t ゾーンが境界ネットワークとインターネットの両方に提供される Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t のシナリオで、フェデレーションサーバープロキシの名前解決が正常に機能するようになります。クライアントでは、次のタスクを完了する必要があります。  
  
-   制御するインターネットゾーンの DNS は、AD FS ホスト名に対するすべてのインターネットクライアント要求をフェデレーションサーバープロキシに解決するように構成する必要があります。 これを実現するには、ホスト \(A @ no__t-1 リソースレコードをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加します。  
  
-   AD FS ホスト名に対するすべての受信クライアント要求をフェデレーションサーバーに解決するように、境界ネットワークの DNS を構成する必要があります。 これを実現するには、ホスト \(A @ no__t-1 リソースレコードをフェデレーションサーバープロキシの境界 DNS ゾーンに追加します。  
  
> [!NOTE]  
> フェデレーションサーバーのホスト \(A @ no__t-1 リソースレコードが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーのホスト \(A @ no__t-1 リソースレコードを作成する方法の詳細については、「 [Add a &#40;Host&#41; a Resource record to a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>フェデレーションサーバープロキシのインターネット DNS ゾーンにホスト \(A @ no__t-1 リソースレコードを追加する  
インターネット上のクライアントコンピューターが、新しく展開されたフェデレーションサーバープロキシを使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、制御するインターネット DNS ゾーンで \(A @ no__t-1 リソースレコードを作成する必要があります。 このリソースレコードは、アカウントのフェデレーション @no__t サーバーのホスト名を解決します。たとえば、no__t @ は、境界ネットワーク内の 131.107.27.68 @ no__t のように、アカウントフェデレーションサーバー @no__t プロキシの IP アドレスに対して解決されます。  
  
> [!NOTE]  
> Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行する DNS サーバーを DNS サーバーサービスと共に使用して、インターネット DNS ゾーンを制御することを前提としています。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>ホスト \(A @ no__t-1 リソースレコードをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加するには  
  
1.  インターネット DNS ゾーンの dns サーバーで、の DNS スナップ @ no__t を開きます。  
  
2.  コンソールツリーで、右 @ no__t をクリックして該当する前方参照ゾーンをクリックし、[**新しいホスト \(a または AAAA @ no__t**] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 \(FQDN @ no__t-1 fs.fabrikam.com には、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、131.107.27.68) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>フェデレーションサーバープロキシの境界 DNS ゾーンにホスト \(A @ no__t-1 リソースレコードを追加する  
インターネットクライアント要求がフェデレーションサーバープロキシによって正常に処理され、インターネット DNS ゾーンによって解決された後、フェデレーションサーバーに接続できるようにするには、境界 DNS ゾーンでホスト \(A @ no__t-1 リソースレコードを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバーのホスト名 (たとえば、fs) を解決します。この名前は、@no__t ます。 fabrikam. com @ no__t は、アカウントフェデレーション @no__t サーバーの IP アドレス (たとえば、企業ネットワークの 192.168.1.4 @ no__t) の IP アドレスに対しては0になります。  
  
> [!NOTE]  
> 境界 DNS ゾーンを制御するために、DNS サーバーサービスを使用して windows 2000 Server、Windows Server 2003、Windows Server 2008、または Windows Server®2012を実行している DNS サーバーを使用していることを前提としています。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>ホスト \(A @ no__t-1 リソースレコードをフェデレーションサーバープロキシの境界 DNS ゾーンに追加するには  
  
1.  境界ネットワークの DNS サーバーで、 **dns スナップ @ no__t-** 1 を開きます。  
  
2.  コンソールツリーで、右 @ no__t をクリックして該当する前方参照ゾーンをクリックし、[**新しいホスト \(a または AAAA @ no__t**] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、FQDN fs.fabrikam.com の場合は、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** ボックスに、企業ネットワーク内のフェデレーションサーバーの ip アドレス (たとえば、192.168.1.4) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

