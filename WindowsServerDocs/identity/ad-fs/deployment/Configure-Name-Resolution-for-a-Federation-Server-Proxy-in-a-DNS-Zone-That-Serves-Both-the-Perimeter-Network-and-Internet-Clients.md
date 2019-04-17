---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: "ネットワークの境界の両方を対象とインターネット クライアント ゾーンの DNS にフェデレーション サーバー プロキシの名前解決を構成します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3b154459163b2142ff1d3aba424a86305d093de4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>ネットワークの境界の両方を対象とインターネット クライアント ゾーンの DNS にフェデレーション サーバー プロキシの名前解決を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

\(AD FS\) シナリオで Active Directory フェデレーション サービスは 1 つまたは複数のドメイン ネーム システム \(DNS\) ゾーンが境界ネットワークとインターネット クライアントの両方を提供するフェデレーション サーバー プロキシの名前解決が正常に機能、次のタスクを完了する必要があります。  
  
-   AD FS のすべてのインターネット クライアント要求のホスト名、フェデレーション サーバー プロキシを解決するのには、制御するインターネット ゾーンに DNS を構成する必要があります。 これを行うには、フェデレーション サーバー プロキシのインターネット DNS ゾーンをホスト \(A\) リソース レコードを追加します。  
  
-   AD FS のすべての着信クライアント要求のホスト名、フェデレーション サーバーを解決するのには、境界ネットワークに DNS を構成する必要があります。 そのために、フェデレーション サーバー プロキシの境界の DNS ゾーンをホスト \(A\) リソース レコードを追加します。  
  
> [!NOTE]  
> 企業ネットワークの DNS にフェデレーション サーバーのホスト \(A\) リソース レコードを既に作成されていると見なされます。 このレコードが存在しない場合は、このレコードを作成し、これらの手順を実行します。 フェデレーション サーバーのホスト \(A\) リソース レコードを作成する方法の詳細については、次を参照してください[ホスト (&) #40; を追加。A & #41 です。リソース レコードを会社の DNS にフェデレーション サーバーに](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)します。  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシのインターネット DNS ゾーンをホスト \(A\) リソース レコードを追加します。  
インターネット上のクライアント コンピュータが新しく展開されるフェデレーション サーバー プロキシを介したフェデレーション サーバーに正常にアクセスできるようには、制御するインターネット DNS ゾーンのホスト \(A\) リソース レコードを作成する必要があります。 このリソース レコードが、アカウント フェデレーション サーバーのホスト名を解決 \ (たとえば、fs.fabrikam.com\) アカウント フェデレーション サーバー プロキシの IP アドレスを \ (たとえば、131.107.27.68\)、境界ネットワークにします。  
  
> [!NOTE]  
> インターネット DNS ゾーンを制御する DNS サーバー サービスと Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行している DNS サーバーを使用するいると見なされます。  
  
メンバーシップ**管理者**、相当するものでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](http://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシのインターネット DNS ゾーンに、ホスト \(A\) リソース レコードを追加するには  
  
1.  インターネット DNS ゾーンの DNS サーバー、DNS スナップインを開きます。  
  
2.  コンソール ツリーで、適切な前方参照ゾーンを右クリックしをクリックして**新しいホスト \(A or AAAA\)**します。  
  
3.  **名**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名の \(FQDN\) fs.fabrikam.com に対する次のように入力します。 **fs**します。  
  
4.  **IP アドレス**、新しいフェデレーション サーバー プロキシ、131.107.27.68 などの IP アドレスを入力します。  
  
5.  をクリックして**ホストの追加**します。  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの境界の DNS ゾーンをホスト \(A\) リソース レコードを追加します。  
インターネット クライアント要求は、フェデレーション サーバー プロキシで正常に処理することができますは、インターネット DNS ゾーンによって解決した後、フェデレーション サーバーに到達できるように、境界 DNS ゾーンのホスト \(A\) リソース レコードを作成する必要があります。 このリソース レコードが、アカウント フェデレーション サーバーのホスト名を解決 \ (たとえば、fs します。 fabrikam.com\)、アカウント フェデレーション サーバーの IP アドレスを \ (たとえば、192.168.1.4\) 企業ネットワークにします。  
  
> [!NOTE]  
> 境界の DNS ゾーンを制御する DNS サーバー サービスと Windows 2000 Server、Windows Server 2003、Windows Server 2008、または Windows Server® 2012 を実行している DNS サーバーを使用するいると見なされます。  
  
メンバーシップ**管理者**、相当するものでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](http://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの境界の DNS ゾーンに、ホスト \(A\) リソース レコードを追加するには  
  
1.  境界ネットワークの DNS サーバーで開き、 **DNS スナップイン**します。  
  
2.  コンソール ツリーで、適切な前方参照ゾーンを右クリックしをクリックして**新しいホスト \(A or AAAA\)**します。  
  
3.  **名**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、FQDN が fs.fabrikam.com、次のように入力します。 **fs**します。  
  
4.  **IP アドレス**テキスト ボックスに、ip アドレスを入力 192.168.1.4 など、企業ネットワーク内のフェデレーション サーバーのアドレスします。  
  
5.  をクリックして**ホストの追加**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

