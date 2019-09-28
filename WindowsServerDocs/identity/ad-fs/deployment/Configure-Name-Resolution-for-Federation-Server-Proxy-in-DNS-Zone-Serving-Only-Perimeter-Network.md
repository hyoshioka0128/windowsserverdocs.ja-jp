---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: 境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: de4627f2e03e6432f4e678cd9ca932819cb483d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408433"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>境界ネットワークのみを対象とする DNS ゾーンでフェデレーション サーバー プロキシの名前解決を構成する


1つ以上のドメインネームシステム \(DNS @ no__t ゾーンが境界ネットワークのみを提供する Active Directory フェデレーションサービス (AD FS) @no__t 0AD FS @ no__t のシナリオで、フェデレーションサーバーの名前解決が正常に機能するようにするには、次のようにします。タスクを完了する必要があります。  
  
-   フェデレーションサーバープロキシ上の hosts ファイルを更新して、フェデレーションサーバーの IP アドレスを追加する必要があります。  
  
-   AD FS ホスト名に対するすべてのクライアント要求をフェデレーションサーバープロキシに解決するように、境界ネットワークの DNS を構成する必要があります。 これを行うには、ホスト \(A @ no__t-1 リソースレコードをフェデレーションサーバープロキシの境界 DNS に追加します。  
  
> [!NOTE]  
> この手順では、フェデレーションサーバーのホスト \(A @ no__t-1 リソースレコードが、企業ネットワークの DNS に既に作成されていることを前提としています。 このレコードがまだ存在しない場合は、このレコードを作成してから、次の手順を実行します。 フェデレーションサーバーのホスト \(A @ no__t-1 リソースレコードを作成する方法の詳細については、「 [Add a &#40;Host&#41; a Resource record to a federation server](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)」を参照してください。  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスをホストファイルに追加する  
フェデレーションサーバープロキシは、アカウントパートナーの境界ネットワークで期待どおりに動作することができます。フェデレーションサーバーの DNS ホスト名を指すフェデレーションサーバープロキシの hosts ファイルにエントリを追加する必要があります。たとえば、@no__t no__t @ と IP address \(for たとえば、アカウントパートナーの企業ネットワークの 192.168.1.4 @ no__t-3) を参照しているとします。 このエントリを hosts ファイルに追加すると、フェデレーションサーバープロキシは、アカウントパートナー内のフェデレーションサーバーに対してクライアント @ no__t から開始された呼び出しを解決するために、それ自体に接続できなくなります。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>フェデレーションサーバーの IP アドレスを hosts ファイルに追加するには  
  
1.  % Systemroot% \\Winnt @ no__t-1System32 @ no__t-2Drivers ディレクトリフォルダーに移動し、 **hosts**ファイルを見つけます。  
  
2.  メモ帳を起動し、 **hosts**ファイルを開きます。  
  
3.  次の例に示すように、アカウントパートナーのフェデレーションサーバーの IP アドレスとホスト名を**ホスト**ファイルに追加します。  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  ファイルを保存し、閉じます。  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>フェデレーションサーバープロキシの境界 DNS にホスト \(A @ no__t-1 リソースレコードを追加する  
インターネット上のクライアントが、新しく展開されたフェデレーションサーバープロキシを使用してフェデレーションサーバーに正常にアクセスできるようにするには、まず、境界 DNS のホスト \(A @ no__t-1 リソースレコードを作成する必要があります。 このリソースレコードは、アカウントのフェデレーション @no__t サーバーのホスト名を解決します。たとえば、no__t @ は、境界ネットワーク内の 131.107.27.68 @ no__t のように、アカウントフェデレーションサーバー @no__t プロキシの IP アドレスに対して解決されます。  
  
> [!NOTE]  
> 境界 DNS ゾーンを制御するには、Windows 2000 Server、Windows Server 2003、または Windows Server 2008 を DNS サーバーサービスと共に実行している DNS サーバーを使用していることを前提としています。  
  
メンバーシップ **管理者**, 、または同等の権限は、この手順を実行するために必要な最小値。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>フェデレーションサーバープロキシの境界 DNS にホスト \(A @ no__t-1 リソースレコードを追加するには  
  
1.  境界ネットワークの DNS サーバーで、DNS スナップを開きます @ no__t-0in です。 **[スタート]** をクリックし、 **[管理ツール]** をポイントして、 **[DNS]** をクリックします。  
  
2.  コンソールツリーで、右 @ no__t をクリックして該当する前方参照ゾーンをクリックし、[**新しいホスト \(a または AAAA @ no__t**] をクリックします。  
  
3.  **[名前]** に、フェデレーションサーバーのコンピューター名のみを入力します。 たとえば、完全修飾ドメイン名 \(FQDN @ no__t-1 fs.fabrikam.com には、「 **fs**」と入力します。  
  
4.  **[Ip アドレス]** に、新しいフェデレーションサーバープロキシの ip アドレス (たとえば、 **131.107.27.68**) を入力します。  
  
5.  **[ホストの追加]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバー プロキシの名前解決の要件](https://technet.microsoft.com/library/dd807055.aspx)  
  

