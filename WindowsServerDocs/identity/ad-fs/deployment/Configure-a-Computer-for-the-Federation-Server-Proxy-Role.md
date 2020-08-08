---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: フェデレーション サーバー プロキシの役割用にコンピューターを構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.author: billmath
ms.openlocfilehash: 06bccb135963d5b5bc754e895843a4d75153c120
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963123"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成する

必要な証明書を使用してコンピューターを構成し、フェデレーションサービスプロキシの役割サービスをインストールしたら、コンピューターをフェデレーションサーバープロキシになるように構成することができます。 コンピューターがフェデレーション サーバー プロキシの役割を実行できるようにするには、以下の手順を使用します。

> [!IMPORTANT]
> この手順を使用してフェデレーションサーバープロキシコンピューターを構成する前に、「[チェックリスト: フェデレーションサーバープロキシを](Checklist--Setting-Up-a-Federation-Server-Proxy.md)一覧表示されている順序で設定する」の手順をすべて実行していることを確認してください。 少なくとも 1 台のフェデレーション サーバーが展開され、フェデレーション サーバー プロキシの構成を認証するために必要なすべての資格情報が実装されていることを確認します。 また、 \( 既定の Web サイトで Secure Sockets Layer SSL バインドを構成する必要があり \) ます。構成しないと、このウィザードは開始されません。 フェデレーション サーバー プロキシが機能できるようにするには、これらすべてのタスクを完了する必要があります。

コンピューターのセットアップが終了したら、フェデレーション サーバー プロキシが期待どおりに機能していることを確認します。 詳細については、「[フェデレーション サーバー プロキシが正常に動作していることを確認する](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)」を参照してください。

この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。

### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>フェデレーション サーバー プロキシの役割用にコンピューターを構成するには

1.  AD FS フェデレーション サーバー構成ウィザードを開始するには 2 つの方法があります。 ウィザードを開始するには、次のいずれかを実行します。

    -   [**スタート**] 画面で、「**AD FS フェデレーションサーバープロキシ構成ウィザード**」と入力し、enter キーを押します。

    -   セットアップウィザードが完了したら、Windows エクスプローラーを開き、 **C: \\ windows \\ ADFS**フォルダーに移動して、 \- [ **FspConfigWizard.exe**] をダブルクリックします。

2.  いずれかの方法を使用してウィザードを開始し、[**ようこそ**] ページで [**次へ**] をクリックします。

3.  [**フェデレーション サービス名の指定**] ページの [**フェデレーション サービス名**] に、このコンピューターがプロキシ ロールで動作するフェデレーション サービスを示す名前を入力します。

4.  具体的なネットワーク要件に基づいて、フェデレーション サービスに要求を転送するのに HTTP プロキシ サーバーを使用する必要があるかどうかを判断します。 必要がある場合は、[**このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する**] チェック ボックスをオンにし、[**HTTP プロキシ サーバー アドレス**] にプロキシ サーバーのアドレスを入力し、[**接続をテスト**] をクリックして接続を検証してから、[**次へ**] をクリックします。

5.  メッセージに従って、このフェデレーション サーバー プロキシとフェデレーション サービスとの間に信頼関係を確立するために必要な資格情報を指定します。

    既定では、フェデレーションサービスによって使用されるサービスアカウント、またはローカルの BUILTIN Administrators グループのメンバーだけ \\ が、フェデレーションサーバープロキシを承認できます。

6.  [**設定の適用準備**] ページで、詳細を確認します。 設定が正しい場合は、[**次へ**] をクリックして、これらのプロキシ設定によるこのコンピューターの構成を開始します。

7.  **[構成結果]** ページで作業内容を確認します。 すべての構成手順が終了したら、 **[閉じる]**  をクリックしてウィザードを終了します。

    \( \) \- フェデレーションサーバー proxys の管理に使用する Microsoft 管理コンソール MMC スナップインはありません。 組織内の各フェデレーションサーバー proxys の設定を構成するには、Windows PowerShell コマンドレットを使用します。

## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>\/プロキシ操作用の代替 TCP IP ポートの構成
既定では、フェデレーションサーバープロキシサービスは、HTTPS トラフィックに TCP ポート443を使用するように構成されています。また、フェデレーションサーバーとの通信には、HTTP トラフィック用のポート80を使用するように構成されています。 異なるポートを構成するには (HTTPS に TCP ポート 444、HTTP にポート 81 など)、次のタスクを実行する必要があります。

> [!NOTE]
> 代替の TCP IP ポートで動作する AD FS を最初に展開する場合は、 \/ まず、フェデレーションサーバーとフェデレーションサーバープロキシコンピューターの両方で HTTP および HTTPS 用に IIS プロトコルバインドのポートを変更する必要があります。 これは、初期構成のために AD FS 構成ウィザードを実行する前に実行する必要があります。 インターネットインフォメーションサービス \( IIS \) を最初に構成する場合、 \/ AD FS 内でウィザードベースの構成が行われると代替の TCP IP ポート設定が検出されますが、 \- 次の手順は必要ありません。 後でポート設定を変更する場合は、IIS プロトコル バインドを最初に更新してから、次に示す手順を実行してポート設定を適切に更新します。 IIS バインディングの編集の詳細については、Microsoft サポート技術情報の[記事 149605](https://go.microsoft.com/fwlink/?LinkId=190275)を参照してください。

#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>\/フェデレーションサーバープロキシで使用する代替 TCP IP ポートを構成するには

1.  既定以外のポートを使用するようにフェデレーション サーバーを構成します。

    これを行うには、 **Set \- set-adfsproperties**コマンドレットの一部として*Httpsport*オプションと*httpsport*オプションを指定して、既定以外のポート番号を指定します。 たとえば、これらのポートを構成するには、フェデレーションサーバーコンピューターの Windows PowerShell セッションで次のコマンドを使用します。

    ```
    Set-ADFSProperties -HttpsPort 444
    Set-ADFSProperties -HttpPort 81
    ```

2.  既定以外のポートを使用するようにフェデレーションサーバープロキシを構成します。

    これを行うには、 **Set \- ADFSProxyProperties**コマンドレットの一部として*Httpsport*オプションと*httpsport*オプションを指定して、既定以外のポート番号を指定します。 たとえば、これらのポートを構成するには、フェデレーションサーバーコンピューターの Windows PowerShell セッションで次のコマンドを使用します。

    ```
    Set-ADFSProxyProperties -HttpsPort 444
    Set-ADFSProxyProperties -HttpPort 81
    ```

    > [!NOTE]
    > エンドポイント Url は、フェデレーションサーバープロキシサービスでは既定で有効になっていません。 新しいフェデレーションサーバーのインストールを構成する場合は、最初にフェデレーションサーバープロキシサービスエンドポイントを有効にする必要があります。 たとえば、この手順の例で参照されているすべてのエンドポイントで、プロキシ用に有効にしたことを前提としています。そのためには、AD FS 管理スナップインで選択し、 \- [**プロキシで有効に**する] を選択します。

3.  フェデレーションサーバープロキシで IIS のインストールを更新して、更新された \( \) ポート番号を反映するように Security Assertion Markup Language SAML と ws-trust の \- エンドポイントが構成されるようにします。 これを行うには、メモ帳を使用して、Web.config ファイル内の次のように変更します。このファイルは、 \\ \\ \\ \\ フェデレーションサーバープロキシコンピューターの systemdrive% inetpub adfs ls にあります。 たとえば、sts1.contoso.com という名前のフェデレーションサーバーがあり、新しいポート番号が444であると仮定した場合、フェデレーションサーバープロキシコンピューターのメモ帳で Web.config ファイルを参照して開き、次のセクションを見つけて、下に強調表示されているポート番号を変更し、メモ帳を保存して終了します。

    ```
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />
    ```

4.  フェデレーションサーバープロキシサービスのユーザーアカウントを、 \( 関連するエンドポイント url のアクセス制御リスト ACL に追加し \) ます。 たとえば、ポート番号が1234で、AD FSfederation サーバープロキシサービスを実行するために使用されるユーザーアカウントが組み込みの Network Service アカウントである場合は、 \- コマンドプロンプトで次のコマンドを入力します。

    ```
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"

    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"
    ```

    前のコマンドは、フェデレーションサーバーとフェデレーションサーバープロキシコンピューターの両方で実行する必要があります。

## <a name="additional-references"></a>その他の参照情報
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)


