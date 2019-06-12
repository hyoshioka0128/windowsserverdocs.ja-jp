---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: 境界ネットワークとインターネット クライアントの両方を対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: cef87e725db7068ac4ed93524e09a25de95ec276
ms.sourcegitcommit: 9a4ab3a0d00b06ff16173aed616624c857589459
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2019
ms.locfileid: "66828516"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>境界ネットワークとインターネット クライアントの両方を対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


Active の Directory フェデレーション サービスでフェデレーション サーバー プロキシの名前解決が正常に作業できるように\(AD FS\)シナリオを 1 つまたは複数のドメイン名システム\(DNS\)ゾーン機能両方、境界ネットワークとインターネット クライアントでは、次のタスクを完了する必要があります。  
  
-   AD FS 用のすべてのインターネット クライアント要求のホスト名、フェデレーション サーバー プロキシを解決するのを制御するインターネット ゾーンで DNS を構成する必要があります。 これを実現するには、ホストを追加する\(A\)をフェデレーション サーバー プロキシのインターネットの DNS ゾーンにリソース レコード。  
  
-   AD FS のすべての着信クライアント要求のホスト名、フェデレーション サーバーを解決するのには、境界ネットワークで DNS を構成する必要があります。 これを実現するには、ホストを追加する\(A\)をフェデレーション サーバー プロキシの境界の DNS ゾーンにリソース レコード。  
  
> [!NOTE]  
> ように仮定ホスト\(A\)リソース レコードのフェデレーション サーバーは、企業で既に作成されているネットワーク DNS。 このレコードが存在しない場合は、このレコードを作成し、これらの手順を実行します。 ホストを作成する方法の詳細についての\(A\) 、フェデレーション サーバーのリソース レコードを参照してください[ホストを追加する&#40;A&#41;をフェデレーション サーバーの会社の DNS リソース レコード](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)します。  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>ホストの追加\(A\)をフェデレーション サーバー プロキシのインターネットの DNS ゾーンにリソース レコード  
ホストを作成する必要があります最初に、インターネット上のクライアント コンピューターが、新しく展開されるフェデレーション サーバー プロキシを介してフェデレーション サーバーに正常にアクセスできるように\(A\)を制御するインターネット DNS ゾーン内のリソース レコード。 このリソース レコードは、アカウント フェデレーション サーバーのホスト名を解決\(fs.fabrikam.com など\)、アカウント フェデレーション サーバー プロキシの IP アドレスに\(など 131.107.27.68\)で、境界ネットワーク。  
  
> [!NOTE]  
> インターネット DNS ゾーンを制御するための DNS サーバー サービスが Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行している DNS サーバーを使用するいると見なされます。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>ホストを追加する\(A\)をフェデレーション サーバー プロキシのインターネットの DNS ゾーンにリソース レコード  
  
1.  インターネット DNS ゾーンの DNS サーバー、DNS スナップインを開きます\-でします。  
  
2.  コンソール ツリーで、右\-、適切な前方参照ゾーンをクリックし、クリックして**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名\(FQDN\) fs.fabrikam.com、型**fs**します。  
  
4.  **IP アドレス**、新しいフェデレーション サーバー プロキシ、131.107.27.68 などの IP アドレスを入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>ホストの追加\(A\)をフェデレーション サーバー プロキシの境界の DNS ゾーンにリソース レコード  
インターネット クライアント要求は、フェデレーション サーバー プロキシが正常に処理できるし、は、インターネット DNS ゾーンで解決した後、フェデレーション サーバーに到達、ようにする前に、ホストを作成する必要があります\(A\)境界内のリソース レコードDNS ゾーンです。 このリソース レコードは、アカウント フェデレーション サーバーのホスト名を解決\(fs など。 fabrikam.com\)アカウント フェデレーション サーバーの IP アドレスに\(例: 192.168.1.4\)企業ネットワークにします。  
  
> [!NOTE]  
> 境界の DNS ゾーンを制御するための DNS サーバー サービスが Windows 2000 Server、Windows Server 2003、Windows Server 2008、または Windows Server® 2012 を実行している DNS サーバーを使用するいると見なされます。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>ホストを追加する\(A\)をフェデレーション サーバー プロキシの境界の DNS ゾーンにリソース レコード  
  
1.  境界ネットワークの DNS サーバーを開き、 **DNS スナップ\-で**します。  
  
2.  コンソール ツリーで、右\-、適切な前方参照ゾーンをクリックし、クリックして**新しいホスト\(A または AAAA\)** します。  
  
3.  **名前**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、FQDN fs.fabrikam.com では、次のように入力します。 **fs**します。  
  
4.  **IP アドレス**テキスト ボックスに、ip アドレスの入力例: 192.168.1.4 で、企業ネットワーク内のフェデレーション サーバーのアドレスします。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

