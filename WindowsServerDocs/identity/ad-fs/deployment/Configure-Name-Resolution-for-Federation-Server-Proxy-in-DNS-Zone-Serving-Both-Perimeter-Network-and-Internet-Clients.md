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
ms.sourcegitcommit: 8fbd2d877612a9feb02d7d91ed0372d7cd441d5c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71359835"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>境界ネットワークとインターネット クライアントの両方を対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


Active Directory フェデレーションサービス (AD FS) \(\) AD FS のフェデレーションサーバープロキシに対して名前解決が正常に機能するように、DNS \(ゾーンが境界ネットワークとインターネットクライアントの両方にサービスを提供している場合は、次のタスクを完了する必要があります。\)  
  
-   制御するインターネットゾーンの DNS は、AD FS ホスト名に対するすべてのインターネットクライアント要求をフェデレーションサーバープロキシに解決するように構成する必要があります。 これを実現するには、\) リソースレコード \(ホストをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加します。  
  
-   AD FS ホスト名に対するすべての受信クライアント要求をフェデレーションサーバーに解決するように、境界ネットワークの DNS を構成する必要があります。 これを実現するには、\) リソースレコード \(ホストをフェデレーションサーバープロキシの境界 DNS ゾーンに追加します。  
  
> [!NOTE]  
> フェデレーションサーバーの\) リソースレコード \(ホストが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーの\) リソースレコード \(ホストを作成する方法の詳細については、「 [Add a host &#40;a&#41; Resource record to a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>\) リソースレコード \(ホストをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加する  
インターネット上のクライアントコンピューターが、新しく展開されたフェデレーションサーバープロキシを使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、制御するインターネット DNS ゾーンで\) リソースレコード \(ホストを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバーのホスト名 \(を解決します。たとえば、境界ネットワーク内の 131.107.27.68\) など、アカウントフェデレーションサーバー \(プロキシの IP アドレスには、fs.fabrikam.com\) ます。  
  
> [!NOTE]  
> Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行する DNS サーバーを DNS サーバーサービスと共に使用して、インターネット DNS ゾーンを制御することを前提としています。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>\) リソースレコード \(ホストをフェデレーションサーバープロキシのインターネット DNS ゾーンに追加するには  
  
1.  インターネット DNS ゾーンの dns サーバーで、の DNS スナップ\-を開きます。  
  
2.  コンソールツリーで、該当する前方参照ゾーンを右\-クリックし、[**新しいホスト \(A または AAAA\)** ] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 \(FQDN\) fs.fabrikam.com の場合は、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、131.107.27.68) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>\) リソースレコード \(ホストをフェデレーションサーバープロキシの境界 DNS ゾーンに追加する  
インターネットクライアント要求がフェデレーションサーバープロキシによって正常に処理され、インターネット DNS ゾーンによって解決された後にフェデレーションサーバーに接続できるように、境界 DNS ゾーンで\) リソースレコード \(ホストを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバー \(のホスト名 (たとえば、fs) を解決します。 fabrikam.com は、企業ネットワーク内の 192.168.1.4\) など、アカウントフェデレーション \(サーバーの IP アドレスに\) します。  
  
> [!NOTE]  
> 境界 DNS ゾーンを制御するために、DNS サーバーサービスを使用して windows 2000 Server、Windows Server 2003、Windows Server 2008、または Windows Server®2012を実行している DNS サーバーを使用していることを前提としています。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>\) リソースレコード \(ホストをフェデレーションサーバープロキシの境界 DNS ゾーンに追加するには  
  
1.  境界ネットワークの DNS サーバーで、**の dns スナップ\-** を開きます。  
  
2.  コンソールツリーで、該当する前方参照ゾーンを右\-クリックし、[**新しいホスト \(A または AAAA\)** ] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、FQDN fs.fabrikam.com の場合は、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** ボックスに、企業ネットワーク内のフェデレーションサーバーの ip アドレス (たとえば、192.168.1.4) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

