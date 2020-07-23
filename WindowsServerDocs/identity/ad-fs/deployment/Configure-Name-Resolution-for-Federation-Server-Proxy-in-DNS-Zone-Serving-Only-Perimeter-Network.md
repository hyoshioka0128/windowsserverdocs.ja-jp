---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: 境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4c00fa371539109a3cb444ebd999f282dc70b771
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953764"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


1つ以上のドメインネームシステムの DNS ゾーンが境界ネットワークのみを提供する Active Directory フェデレーションサービス (AD FS) AD FS シナリオで、フェデレーションサーバーの名前解決が正常に機能するようにするには、 \( \) \( \) 次のタスクを完了する必要があります。  
  
-   フェデレーションサーバープロキシ上の hosts ファイルを更新して、フェデレーションサーバーの IP アドレスを追加する必要があります。  
  
-   AD FS ホスト名に対するすべてのクライアント要求をフェデレーションサーバープロキシに解決するように、境界ネットワークの DNS を構成する必要があります。 これを行うには、ホスト a \( \) リソースレコードをフェデレーションサーバープロキシの境界 DNS に追加します。  
  
> [!NOTE]  
> これらの手順では、 \( \) フェデレーションサーバーのホスト a リソースレコードが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーのホスト a リソースレコードを作成する方法の詳細につい \( \) ては、「 [Add A host &#40;a&#41; resource Record To a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスをホストファイルに追加する  
フェデレーションサーバープロキシがアカウントパートナーの境界ネットワークで期待どおりに動作するようにするには、フェデレーションサーバーの DNS ホスト名を指すフェデレーションサーバープロキシの hosts ファイルにエントリを追加する必要があり \( ます。たとえば、 \) \( \) アカウントパートナーの企業ネットワークの192.168.1.4 にある fs.fabrikam.com や IP アドレスなどです。 このエントリを hosts ファイルに追加すると、フェデレーションサーバープロキシは、 \- アカウントパートナー内のフェデレーションサーバーに対して開始されたクライアントの呼び出しを解決するために、フェデレーションサーバープロキシ自体に接続できなくなります。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスを hosts ファイルに追加するには  
  
1.  % Systemroot% \\ Winnt \\ System32 \\ Drivers ディレクトリフォルダに移動し、 **hosts**ファイルを見つけます。  
  
2.  メモ帳を起動し、**hosts** ファイルを開きます。  
  
3.  次の例に示すように、アカウントパートナーのフェデレーションサーバーの IP アドレスとホスト名を**ホスト**ファイルに追加します。  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  ファイルを保存して閉じます。  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>\( \) フェデレーションサーバープロキシの境界 DNS にホスト a リソースレコードを追加する  
インターネット上のクライアントが、新しく展開されたフェデレーションサーバープロキシを使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、 \( 境界 DNS でホスト a リソースレコードを作成する必要があり \) ます。 このリソースレコードは、アカウントフェデレーションサーバーのホスト名を解決し \( ます。たとえば、fs.fabrikam.com は、 \) \( 境界ネットワーク内の131.107.27.68 など、アカウントフェデレーションサーバープロキシの IP アドレス \) です。  
  
> [!NOTE]  
> 境界 DNS ゾーンを制御するには、Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を DNS サーバーサービスと共に実行している DNS サーバーを使用していることを前提としています。  
  
**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>ホスト a \( \) リソースレコードをフェデレーションサーバープロキシの境界 DNS に追加するには  
  
1.  境界ネットワークの DNS サーバーで、DNS スナップインを開き \- ます。 [**スタート**] をクリックし、[**管理ツール**] をポイントして、[ **DNS**] をクリックします。  
  
2.  コンソールツリーで、 \- 該当する前方参照ゾーンを右クリックし、[**新しいホスト \( A または AAAA \) **] をクリックします。  
  
3.  [**名前**] に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 FQDN fs.fabrikam.com の場合は、 \( \) 「 **fs**」と入力します。  
  
4.  [ **Ip アドレス**] に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、 **131.107.27.68**) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他のリファレンス  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807055(v=ws.11))  
  
