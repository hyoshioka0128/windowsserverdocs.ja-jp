---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: フェデレーション サーバー プロキシの役割用にコンピューターを構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2a89bab2fd1af1a1d7234da29f2025b4b12d6774
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861803"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

後で必要な証明書を持つコンピューターを構成して、フェデレーション サービス プロキシ役割サービスがインストールされているは、フェデレーション サーバー プロキシにするコンピューターを構成する準備が完了したら。 コンピューターがフェデレーション サーバー プロキシの役割を実行できるようにするには、以下の手順を使用します。  
  
> [!IMPORTANT]  
> この手順を使用して、フェデレーション サーバー プロキシ コンピューターを構成する前に行うこと、すべての手順に従っていることを確認して[チェックリスト。A Federation Server Proxy の構成設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)記載されている順序で。 少なくとも 1 台のフェデレーション サーバーが展開され、フェデレーション サーバー プロキシの構成を認証するために必要なすべての資格情報が実装されていることを確認します。 Secure Sockets Layer を構成することも必要があります。 \(SSL\)既定の Web サイト、またはこのウィザードでのバインドは開始されません。 フェデレーション サーバー プロキシが機能できるようにするには、これらすべてのタスクを完了する必要があります。  
  
コンピューターのセットアップが終了したら、フェデレーション サーバー プロキシが期待どおりに機能していることを確認します。 詳細については、「 [Verify That a Federation Server Proxy Is Operational](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)」を参照してください。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成するには  
  
1.  AD FS フェデレーション サーバー構成ウィザードを開始する 2 つの方法はあります。 ウィザードを開始するには、次のいずれかを実行します。  
  
    -   **開始**画面で「**AD FS フェデレーション サーバー プロキシ構成ウィザード**、し、ENTER キーを押します。  
  
    -   いつでもにセットアップ ウィザードが開き、完全な Windows のエクスプ ローラーと、移動、 **c:\\Windows\\ADFS**フォルダー、およびし倍\- をクリックして**FspConfigWizard.exe**.  
  
2.  いずれかの方法を使ってウィザードを開始し、**[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[フェデレーション サービス名の指定]** ページの **[フェデレーション サービス名]** に、このコンピューターがプロキシの役割で動作するフェデレーション サービスを表す名前を入力します。  
  
4.  具体的なネットワーク要件に基づいて、フェデレーション サービスに要求を転送するのに HTTP プロキシ サーバーを使用する必要があるかどうかを判断します。 必要がある場合は、**[このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する]** チェック ボックスをオンにし、**[HTTP プロキシ サーバー アドレス]** にプロキシ サーバーのアドレスを入力します。次に、**[接続のテスト]** をクリックして接続を確認し、**[次へ]** をクリックします。  
  
5.  メッセージに従って、このフェデレーション サーバー プロキシとフェデレーション サービスとの間に信頼関係を確立するために必要な資格情報を指定します。  
  
    既定では、フェデレーション サービスまたはローカル BUILTIN のメンバーによって使用されるサービス アカウントのみ\\Administrators グループにフェデレーション サーバー プロキシを承認できます。  
  
6.  **[設定の適用の準備完了]** ページで、詳細を確認します。 設定が正しいと思われる場合は、**[次へ]** をクリックして、これらのプロキシ設定を使ってこのコンピューターの構成を開始します。  
  
7.  **[構成結果]** ページで、結果を確認します。 すべての構成手順が終了したら、 **[閉じる]**  をクリックしてウィザードを終了します。  
  
    Microsoft 管理コンソールがない\(MMC\)スナップ\-のフェデレーション サーバーれてを管理するために使用します。 組織内の各フェデレーション サーバーのれての設定を構成するには、Windows PowerShell コマンドレットを使用します。  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>構成別の TCP\/プロキシ操作用の IP ポート  
既定では、HTTPS トラフィックにフェデレーション サーバーとの通信用の HTTP トラフィック用にポート 80 の TCP ポート 443 を使用する、フェデレーション サーバー プロキシ サービスが構成されています。 異なるポートを構成するには (HTTPS に TCP ポート 444、HTTP にポート 81 など)、次のタスクを実行する必要があります。  
  
> [!NOTE]  
> 最初に代替 TCP で動作する AD FS をデプロイするかどうか\/IP ポートでは、まず、フェデレーション サーバーとフェデレーション サーバー プロキシ コンピューターの両方での HTTP および HTTPS の IIS プロトコル バインドでポートを変更する必要があります。 これは、初期構成用 AD FS 構成ウィザードを実行する前に発生する必要があります。 インターネット インフォメーション サービスを構成する場合は\(IIS\)最初に、代替、TCP\/ウィザードときに、IP ポート設定が検出された\-ベースの構成が、AD FS 内で発生し、次の手順はありませんいる。 後でポート設定を変更する場合は、IIS プロトコル バインドを最初に更新してから、次に示す手順を実行してポート設定を適切に更新します。 IIS バインドの編集の詳細については、次を参照してください。[記事 149605](https://go.microsoft.com/fwlink/?LinkId=190275)マイクロソフト サポート技術情報でします。  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>代替 TCP を構成する\/を使用するフェデレーション サーバー プロキシの IP ポート  
  
1.  既定以外のポートを使用するようにフェデレーション サーバーを構成します。  
  
    これを行うには、含めることによって、既定以外のポート番号を指定、 *HttpsPort*と*HttpPort*オプションの一部として、**設定\-ADFSProperties**コマンドレット。 たとえば、これらのポートを構成するには、フェデレーション サーバーのコンピューターに Windows PowerShell セッションで次のコマンドを使用します。  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  既定以外のポートを使用するフェデレーション サーバー プロキシを構成します。  
  
    これを行うには、含めることによって、既定以外のポート番号を指定、 *HttpsPort*と*HttpPort*オプションの一部として、**設定\-ADFSProxyProperties**コマンドレット。 たとえば、これらのポートを構成するには、フェデレーション サーバーのコンピューターに Windows PowerShell セッションで次のコマンドを使用します。  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > エンドポイントの Url は、フェデレーション サーバー プロキシ サービスの既定では有効になっていません。 新しいフェデレーション サーバーのインストールを構成する場合はフェデレーション サーバー プロキシ サービスのエンドポイントを最初に有効にする必要があります。 この手順の例を参照するすべてのエンドポイントを有効にしたにプロキシを AD FS 管理スナップインで選択する前提となりますが、\-でを選択し、**プロキシを有効にする**します。  
  
3.  そのため、フェデレーション サーバー プロキシでの IIS インストールを更新する Security Assertion Markup Language \(SAML\)と WS\-エンドポイントが更新されたポート番号を反映するように構成されている信頼します。 これを行うで systemdrive % にある Web.config ファイルは、次の変更にメモ帳を使用できる\\inetpub\\adfs\\%.*ls\\フェデレーション サーバー プロキシ コンピューターにします。 たとえば、sts1.contoso.com という名前のフェデレーション サーバーがあり、新しいポート番号が 444 と仮定を参照し、フェデレーション サーバー プロキシ コンピューターでメモ帳で Web.config ファイルを開き、次のセクションを探します、としてポート番号を変更以下に示す、および保存してメモ帳を終了します。  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  アクセス制御リストにフェデレーション サーバー プロキシ サービスのユーザー アカウントを追加\(ACL\)関連するエンドポイント url。 例では、ポート番号が 1234 と AD FSfederation サーバー プロキシの実行に使用されるユーザー アカウントでサービスが組み込み\-ネットワーク サービス アカウントで、コマンド プロンプトで次のコマンドを入力します。  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    フェデレーション サーバーと、フェデレーション サーバー プロキシ コンピューターの両方で、前のコマンドを実行する必要があります。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシを設定します。](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

