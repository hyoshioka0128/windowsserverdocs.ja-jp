---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: "境界ネットワークのみを提供する DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32b8e3cc133ce95872881115608bb8cfb17b2427
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>境界ネットワークのみを提供する DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

\(AD FS\) シナリオで Active Directory フェデレーション サービスは 1 つまたは複数のドメイン ネーム システム \(DNS\) ゾーンが境界ネットワークのみを提供するフェデレーション サーバーの名前解決が正常に機能、次のタスクを完了する必要があります。  
  
-   フェデレーション サーバーの IP アドレスを追加するフェデレーション サーバー プロキシで hosts ファイルを更新する必要があります。  
  
-   AD FS のすべてのクライアント要求のホスト名、フェデレーション サーバー プロキシを解決するのには、境界ネットワークに DNS を構成する必要があります。 これを行うには、フェデレーション サーバー プロキシの境界 DNS をホスト \(A\) リソース レコードを追加します。  
  
> [!NOTE]  
> これらの手順では、企業ネットワークの DNS にフェデレーション サーバーのホスト \(A\) リソース レコードを既に作成されていると想定します。 このレコードが存在しない場合は、このレコードを作成し、これらの手順を実行します。 フェデレーション サーバーのホスト \(A\) リソース レコードを作成する方法の詳細については、次を参照してください[ホスト (&) #40; を追加。A & #41 です。リソース レコードを会社の DNS にフェデレーション サーバーに](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)します。  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hosts ファイルにフェデレーション サーバーの IP アドレスを追加します。  
フェデレーション サーバー プロキシがアカウント パートナーの境界ネットワークで期待どおりに動作できるようにそのフェデレーション サーバーの DNS ホスト名を指しているフェデレーション サーバー プロキシで hosts ファイルにエントリを追加する必要があります \ (たとえば、fs.fabrikam.com\) と IP アドレス \ (たとえば、192.168.1.4\)、アカウント パートナーの企業ネットワークにします。 このエントリを hosts ファイルに追加すると、フェデレーション サーバー プロキシは、アカウント パートナーのフェデレーション サーバーにクライアントによって開始された呼び出しを解決するために接続できなくなります。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>Hosts ファイルにフェデレーション サーバーの IP アドレスを追加するには  
  
1.  %Systemroot%\\Winnt\\System32\\Drivers ディレクトリ フォルダーに移動し、検索、**ホスト**ファイル。  
  
2.  メモ帳を起動し、開きます、**ホスト**ファイル。  
  
3.  アカウント パートナーで IP アドレスとのフェデレーション サーバーのホスト名を追加、**ホスト**ファイル、次の例に示すようにします。  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  保存して、ファイルを閉じます。  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの境界の DNS にホスト \(A\) リソース レコードを追加します。  
インターネット上のクライアントが新しく展開されるフェデレーション サーバー プロキシを介したフェデレーション サーバーに正常にアクセスできるようには、境界 DNS にホスト \(A\) リソース レコードを作成する必要があります。 このリソース レコードが、アカウント フェデレーション サーバーのホスト名を解決 \ (たとえば、fs.fabrikam.com\) アカウント フェデレーション サーバー プロキシの IP アドレスを \ (たとえば、131.107.27.68\)、境界ネットワークにします。  
  
> [!NOTE]  
> 使用している DNS サーバー、DNS サーバー サービスでは、Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を実行している境界の DNS ゾーンを制御することが前提です。  
  
メンバーシップ**管理者**、相当するものでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>フェデレーション サーバー プロキシの境界の DNS にホスト \(A\) リソース レコードを追加するには  
  
1.  境界ネットワークの DNS サーバー、DNS スナップインを開きます。 をクリックして**開始**、] をポイント**管理ツール**、] をクリックし、 **DNS**します。  
  
2.  コンソール ツリーで、適切な前方参照ゾーンを右クリックしをクリックして**新しいホスト \(A or AAAA\)**します。  
  
3.  **名**、フェデレーション サーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名の \(FQDN\) fs.fabrikam.com に対する次のように入力します。 **fs**します。  
  
4.  **IP アドレス**、たとえば、新しいフェデレーション サーバー プロキシの IP アドレスを入力**131.107.27.68**します。  
  
5.  をクリックして**ホストの追加**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

