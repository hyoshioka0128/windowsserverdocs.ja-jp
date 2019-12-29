---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: フェデレーション サーバー プロキシの役割用にコンピューターを構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d47f7d3985aa779276f0712347eb9030857cefdb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359789"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成する

必要な証明書を使用してコンピューターを構成し、フェデレーションサービスプロキシの役割サービスをインストールしたら、コンピューターをフェデレーションサーバープロキシになるように構成することができます。 コンピューターがフェデレーション サーバー プロキシの役割を実行できるようにするには、以下の手順を使用します。  
  
> [!IMPORTANT]  
> この手順を使用してフェデレーションサーバープロキシコンピューターを構成する前に、「[チェックリスト: フェデレーションサーバープロキシを](Checklist--Setting-Up-a-Federation-Server-Proxy.md)一覧表示されている順序で設定する」の手順をすべて実行していることを確認してください。 少なくとも 1 台のフェデレーション サーバーが展開され、フェデレーション サーバー プロキシの構成を認証するために必要なすべての資格情報が実装されていることを確認します。 また、既定の Web サイトで Secure Sockets Layer \(SSL\) バインドを構成する必要があります。構成しないと、このウィザードは開始されません。 フェデレーション サーバー プロキシが機能できるようにするには、これらすべてのタスクを完了する必要があります。  
  
コンピューターのセットアップが終了したら、フェデレーション サーバー プロキシが期待どおりに機能していることを確認します。 詳細については、「 [Verify That a Federation Server Proxy Is Operational](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)」を参照してください。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成するには  
  
1.  AD FS フェデレーションサーバー構成ウィザードを開始するには、次の2つの方法があります。 ウィザードを開始するには、次のいずれかを実行します。  
  
    -   **[スタート]** 画面で、「**AD FS フェデレーションサーバープロキシ構成ウィザード**」と入力し、enter キーを押します。  
  
    -   セットアップウィザードが完了したら、いつでもエクスプローラーを開き、 **C:\\windows\\ADFS**フォルダーに移動して、 **[Fspconfigwizard .exe]** をダブル\-クリックします。  
  
2.  いずれかの方法を使ってウィザードを開始し、 **[ようこそ]** ページで **[次へ]** をクリックします。  
  
3.  **[フェデレーション サービス名の指定]** ページの **[フェデレーション サービス名]** に、このコンピューターがプロキシの役割で動作するフェデレーション サービスを表す名前を入力します。  
  
4.  具体的なネットワーク要件に基づいて、フェデレーション サービスに要求を転送するのに HTTP プロキシ サーバーを使用する必要があるかどうかを判断します。 必要がある場合は、 **[このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する]** チェック ボックスをオンにし、 **[HTTP プロキシ サーバー アドレス]** にプロキシ サーバーのアドレスを入力します。次に、 **[接続のテスト]** をクリックして接続を確認し、 **[次へ]** をクリックします。  
  
5.  メッセージに従って、このフェデレーション サーバー プロキシとフェデレーション サービスとの間に信頼関係を確立するために必要な資格情報を指定します。  
  
    既定では、フェデレーションサービスによって使用されるサービスアカウント、または組み込みの BUILTIN\\Administrators グループのメンバーだけが、フェデレーションサーバープロキシを承認できます。  
  
6.  **[設定の適用の準備完了]** ページで、詳細を確認します。 設定が正しいと思われる場合は、 **[次へ]** をクリックして、これらのプロキシ設定を使ってこのコンピューターの構成を開始します。  
  
7.  **[構成結果]** ページで、結果を確認します。 すべての構成手順が終了したら、 **[閉じる]**  をクリックしてウィザードを終了します。  
  
    Microsoft 管理コンソール \(MMC\) スナップ\-を使用して、フェデレーションサーバー proxys を管理することはできません。 組織内の各フェデレーションサーバー proxys の設定を構成するには、Windows PowerShell コマンドレットを使用します。  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>プロキシ操作用の代替 TCP\/IP ポートの構成  
既定では、フェデレーションサーバープロキシサービスは、HTTPS トラフィックに TCP ポート443を使用するように構成されています。また、フェデレーションサーバーとの通信には、HTTP トラフィック用のポート80を使用するように構成されています。 異なるポートを構成するには (HTTPS に TCP ポート 444、HTTP にポート 81 など)、次のタスクを実行する必要があります。  
  
> [!NOTE]  
> 代替の TCP\/IP ポートで動作する AD FS を最初に展開する場合は、まず、フェデレーションサーバーとフェデレーションサーバープロキシコンピューターの両方で HTTP および HTTPS 用に IIS プロトコルバインドのポートを変更する必要があります。 これは、初期構成のために AD FS 構成ウィザードを実行する前に実行する必要があります。 最初にインターネットインフォメーションサービス \(IIS\) を構成すると、\-内でウィザード AD FS ベースの構成が行われたときに代替 TCP\/IP ポートの設定が検出されますが、次の手順は必要ありません。 後でポート設定を変更する場合は、IIS プロトコル バインドを最初に更新してから、次に示す手順を実行してポート設定を適切に更新します。 IIS バインディングの編集の詳細については、Microsoft サポート技術情報の[記事 149605](https://go.microsoft.com/fwlink/?LinkId=190275)を参照してください。  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>フェデレーションサーバープロキシで使用する代替 TCP\/IP ポートを構成するには  
  
1.  既定以外のポートを使用するようにフェデレーション サーバーを構成します。  
  
    これを行うには、 **Set\-set-adfsproperties**コマンドレットの一部として*Httpsport*オプションと*httpsport*オプションを指定して、既定以外のポート番号を指定します。 たとえば、これらのポートを構成するには、フェデレーションサーバーコンピューターの Windows PowerShell セッションで次のコマンドを使用します。  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  既定以外のポートを使用するようにフェデレーションサーバープロキシを構成します。  
  
    これを行うには、 **Set\-ADFSProxyProperties**コマンドレットの一部として*Httpsport*オプションと*httpsport*オプションを指定して、既定以外のポート番号を指定します。 たとえば、これらのポートを構成するには、フェデレーションサーバーコンピューターの Windows PowerShell セッションで次のコマンドを使用します。  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > エンドポイント Url は、フェデレーションサーバープロキシサービスでは既定で有効になっていません。 新しいフェデレーションサーバーのインストールを構成する場合は、最初にフェデレーションサーバープロキシサービスエンドポイントを有効にする必要があります。 たとえば、この手順の例で参照されているすべてのエンドポイントでプロキシに対して有効にしたことを前提としています。そのためには、の [AD FS 管理スナップイン]\-で選択し、[**プロキシで有効に**する] を選択します。  
  
3.  フェデレーションサーバープロキシで IIS のインストールを更新して、Security Assertion Markup Language \(SAML\) と WS\-の信頼エンドポイントが更新されたポート番号を反映するように構成されるようにします。 これを行うで systemdrive % にある Web.config ファイルは、次の変更にメモ帳を使用できる\\inetpub\\adfs\\%.ls\\フェデレーション サーバー プロキシ コンピューターにします。 たとえば、sts1.contoso.com という名前のフェデレーションサーバーがあり、新しいポート番号が444であると仮定した場合、フェデレーションサーバープロキシコンピューターのメモ帳で Web.config ファイルを参照して開き、次のセクションを見つけて、ポート番号を変更します。下に強調表示されているので、メモ帳を保存して終了します。  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  フェデレーションサーバープロキシサービスのユーザーアカウントを、関連するエンドポイント Url のアクセス制御リスト \(ACL\) に追加します。 たとえば、ポート番号が1234で、AD FSfederation サーバープロキシサービスを実行するために使用されるユーザーアカウントがネットワークサービスアカウントに構築された\-の場合は、コマンドプロンプトで次のコマンドを入力します。  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    前のコマンドは、フェデレーションサーバーとフェデレーションサーバープロキシコンピューターの両方で実行する必要があります。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

