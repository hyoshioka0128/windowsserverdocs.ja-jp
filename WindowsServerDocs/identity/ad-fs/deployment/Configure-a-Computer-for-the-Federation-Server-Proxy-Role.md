---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: Configure a Computer for the Federation Server Proxy Role
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2a89bab2fd1af1a1d7234da29f2025b4b12d6774
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>Configure a Computer for the Federation Server Proxy Role

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

必要な証明書を使用してコンピューターを構成して、フェデレーション サービス プロキシ役割サービスをインストールした後は、フェデレーション サーバー プロキシにするコンピューターを構成する準備ができたらします。 コンピューターは、フェデレーション サーバー プロキシの役割で動作できるように、次の手順を使用することができます。  
  
> [!IMPORTANT]  
> フェデレーション サーバー プロキシ コンピューターを構成するこの手順を使用する前にすべての手順を実行したこと確認[チェックリスト: 設定をフェデレーション サーバー プロキシの](Checklist--Setting-Up-a-Federation-Server-Proxy.md)示されている順序でします。 その 1 つ以上のフェデレーション サーバーが展開されていることを確認し、フェデレーション サーバー プロキシ構成を承認するため、すべての必要な資格情報のことが実装されているようにしてください。 既定の Web サイトで Secure Sockets Layer \(SSL\) バインドを構成することも必要があります。または、このウィザードは開始されません。 このフェデレーション サーバー プロキシが機能する前に、これらすべてのタスクを完了する必要があります。  
  
コンピューターのセットアップが完了したら、フェデレーション サーバー プロキシが期待どおりに動作していることを確認します。 詳細については、次を参照してください。[いることを確認、フェデレーション サーバー プロキシが正常に動作](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)します。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割のコンピューターを構成するには  
  
1.  AD FS フェデレーション サーバー構成ウィザードを開始する 2 つの方法はあります。 ウィザードを開始するには、次のいずれかの操作を行います。  
  
    -   **開始**画面で「**AD FS フェデレーション サーバー プロキシ構成ウィザード**、し、Enter キーを押します。  
  
    -   いつでも、セットアップ ウィザードが完了したら、開いているエクスプ ローラーと、移動、**C:\\Windows\\ADFS**フォルダー、およびし、ダブルクリック**FspConfigWizard.exe**します。  
  
2.  いずれかの方法を使用して、ウィザードを開始し、[、**ようこそ**] ページで [**次**します。  
  
3.  **フェデレーション サービス名の指定**ページで、**フェデレーション サービス名**がプロキシの役割をこのコンピューターが機能するフェデレーション サービスを表す名前を入力します。  
  
4.  特定のネットワーク要件に基づいて、要求を転送する、フェデレーション サービスに HTTP プロキシ サーバーを使用する必要があるかどうかを決定します。 場合は、選択、**このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用して**下にあるチェック ボックスをオン**HTTP プロキシ サーバー アドレス**プロキシ サーバーのアドレスを入力] をクリックして**接続のテスト**接続を確認し、[ **[次へ]**します。  
  
5.  メッセージが表示されたら、このフェデレーション サーバー プロキシとフェデレーション サービスの間の信頼を確立するために必要な資格情報を指定します。  
  
    既定では、フェデレーション サービスまたはローカル促しますメンバーによって使用されるサービス アカウントのみがフェデレーション サーバー プロキシを承認できます。  
  
6.  **設定を適用する準備が**] ページで、詳細を確認します。 正しい設定が表示されます場合、] をクリックして**次**これらプロキシの設定でこのコンピューターの構成を開始します。  
  
7.  **構成結果**] ページで、結果を確認します。 すべての構成手順が完了したら、クリックして**閉じる**ウィザードを終了します。  
  
    Microsoft 管理コンソール \(MMC\) snap\ がありません-でフェデレーション サーバー proxys を管理するのに使用します。 組織内のフェデレーション サーバー proxys ごとに設定を構成するには、Windows PowerShell コマンドレットを使用します。  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>プロキシ操作用に代替 TCP/IP ポートを構成します。  
既定では、フェデレーション サーバー プロキシ サービスが HTTPS トラフィックと、フェデレーション サーバーとの通信に HTTP トラフィック用ポート 80 の TCP ポート 443 を使用するように構成します。 HTTPS に TCP ポート 444、HTTP にポート 81 などの別のポートを構成するには、次のタスクを完了する必要があります。  
  
> [!NOTE]  
> 最初に代替 TCP/IP ポートで動作する AD FS を展開する場合は、フェデレーション サーバーとフェデレーション サーバー プロキシ コンピューターの両方で HTTP と HTTPS の IIS プロトコル バインドでポートを変更する必要があります。 これは、初期構成用の AD FS 構成ウィザードを実行する前に発生する必要があります。 インターネット インフォメーション サービス \(IIS\) を最初に構成する場合、wizard\ ベースの構成が、AD FS 内で発生し、次の手順は必要ありませんに代替 TCP/IP ポート設定が検出されます。 後でポート設定を変更する場合は、IIS プロトコル バインドを更新します。まず、ポート設定を更新し、次の手順を使用して適切にします。 IIS バインドの編集の詳細については、次を参照してください。[記事 149605](https://go.microsoft.com/fwlink/?LinkId=190275)、Microsoft サポート技術情報でします。  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>使用するフェデレーション サーバー プロキシ用に代替 TCP/IP ポートを構成するには  
  
1.  既定以外のポートを使用するフェデレーション サーバーを構成します。  
  
    これを行うには、既定以外のポート番号を含めることによって指定、*HttpsPort*と*HttpPort*オプションの一部として、**になって ADFSProperties**コマンドレット。 たとえば、これらのポートを構成するのには、フェデレーション サーバー コンピューター上の Windows PowerShell セッションで、次のコマンドを使用します。  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  既定以外のポートを使用するフェデレーション サーバー プロキシを構成します。  
  
    これを行うには、既定以外のポート番号を含めることによって指定、*HttpsPort*と*HttpPort*オプションの一部として、**になって ADFSProxyProperties**コマンドレット。 たとえば、これらのポートを構成するのには、フェデレーション サーバー コンピューター上の Windows PowerShell セッションで、次のコマンドを使用します。  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > エンドポイントの Url は、フェデレーション サーバー プロキシ サービスに対して既定では無効です。 場合は、新しいフェデレーション サーバーのインストールを構成する必要がありますを有効にしたフェデレーション サーバー プロキシ サービスのエンドポイント最初します。 たとえば、ことが前提にこの手順の例を参照するすべてのエンドポイントを有効にすることにプロキシして AD FS 管理スナップインで選択し、[**プロキシで有効にする**します。  
  
3.  フェデレーション サーバー プロキシで IIS インストールを更新して、Security Assertion Markup Language \(SAML\) と WS\ 信頼エンドポイントが更新されたポート番号を反映するように構成されているようにします。 これを行うには、systemdrive%\\inetpub\\adfs\\ls\\ フェデレーション サーバー プロキシ コンピューター上にある Web.config ファイルで次の変更をメモ帳を使用できます。 たとえば、sts1.contoso.com をという名前のフェデレーション サーバーがあり、新しいポート番号が 444 するものと仮定を参照しフェデレーション サーバー プロキシ コンピューターに、Web.config ファイルをメモ帳で開きます、次のセクションで、下、強調表示されているポート番号を変更しし、保存してメモ帳を終了します。  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  フェデレーション サーバー プロキシ サービスのユーザー アカウントを追加するアクセス制御に関連するエンドポイント Url の \(ACL\) を一覧表示します。 たとえば、ポート番号が 1234 で AD FSfederation サーバー プロキシ サービスを実行するために使用するユーザー アカウントが組み込みの Network Service アカウント場合は、コマンド プロンプトで次のコマンドを入力します。  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    上記のコマンドは、フェデレーション サーバーとフェデレーション サーバー プロキシ コンピューターの両方で実行する必要があります。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

