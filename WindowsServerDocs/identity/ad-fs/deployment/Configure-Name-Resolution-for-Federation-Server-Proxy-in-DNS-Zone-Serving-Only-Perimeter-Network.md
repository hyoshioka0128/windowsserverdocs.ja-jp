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
ms.openlocfilehash: 451ed2bb2b2da9481d33c6e9e339bb582824a4e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854925"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


名前解決が Active Directory フェデレーションサービス (AD FS) \(のフェデレーションサーバーに対して正常に機能するように、AD FS\) シナリオで、1つ以上のドメインネームシステム \(DNS\) ゾーンが境界ネットワークのみを提供する場合は、次のタスクを完了する必要があります。  
  
-   フェデレーションサーバープロキシ上の hosts ファイルを更新して、フェデレーションサーバーの IP アドレスを追加する必要があります。  
  
-   AD FS ホスト名に対するすべてのクライアント要求をフェデレーションサーバープロキシに解決するように、境界ネットワークの DNS を構成する必要があります。 これを行うには、\) リソースレコード \(ホストをフェデレーションサーバープロキシの境界 DNS に追加します。  
  
> [!NOTE]  
> これらの手順では、フェデレーションサーバーの\) リソースレコード \(ホストが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーの\) リソースレコード \(ホストを作成する方法の詳細については、「 [Add a host &#40;a&#41; Resource record to a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスをホストファイルに追加する  
フェデレーションサーバープロキシがアカウントパートナーの境界ネットワーク内で期待どおりに動作するようにするには、フェデレーションサーバーの DNS ホスト \(名を指すフェデレーションサーバープロキシの hosts ファイルにエントリを追加する必要があります。たとえば、fs.fabrikam.com\) や IP アドレス \(、アカウントパートナーの企業ネットワークの 192.168.1.4\) などです。 このエントリを hosts ファイルに追加すると、フェデレーションサーバープロキシは、アカウントパートナー内のフェデレーションサーバーへのクライアント\-開始された呼び出しを解決するために、それ自体に接続できなくなります。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスを hosts ファイルに追加するには  
  
1.  % Systemroot%\\Winnt\\System32\\Drivers ディレクトリフォルダに移動し、 **hosts**ファイルを見つけます。  
  
2.  メモ帳を起動し、**hosts** ファイルを開きます。  
  
3.  次の例に示すように、アカウントパートナーのフェデレーションサーバーの IP アドレスとホスト名を**ホスト**ファイルに追加します。  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  ファイルを保存し、閉じます。  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>フェデレーションサーバープロキシの境界 DNS に\) リソースレコード \(ホストを追加する  
新しく展開されたフェデレーションサーバープロキシを使用して、インターネット上のクライアントがフェデレーションサーバーに正常にアクセスできるようにするには、まず、境界 DNS で\) リソースレコード \(ホストを作成する必要があります。 このリソースレコードは、アカウントフェデレーションサーバーのホスト名 \(を解決します。たとえば、境界ネットワーク内の 131.107.27.68\) など、アカウントフェデレーションサーバー \(プロキシの IP アドレスには、fs.fabrikam.com\) ます。  
  
> [!NOTE]  
> 境界 DNS ゾーンを制御するには、Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を DNS サーバーサービスと共に実行している DNS サーバーを使用していることを前提としています。  
  
**Administrators**、またはそれと同等のメンバーシップが、この手順を実行するために最低限必要なメンバーシップです。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>\) リソースレコード \(ホストをフェデレーションサーバープロキシの境界 DNS に追加するには  
  
1.  境界ネットワークの DNS サーバーで、の DNS スナップ\-を開きます。 **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DNS]** をクリックします。  
  
2.  コンソールツリーで、該当する前方参照ゾーンを右\-クリックし、[**新しいホスト \(A または AAAA\)** ] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 \(FQDN\) fs.fabrikam.com の場合は、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、 **131.107.27.68**) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

