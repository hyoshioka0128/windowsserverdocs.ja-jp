---
title: 手順 12. DirectAccess 接続のテスト
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 85aff4ae9e117359f8827abb15dce47728a30da4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857285"
---
# <a name="step-12-test-directaccess-connectivity"></a>手順 12. DirectAccess 接続のテスト

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

クライアントコンピューターがインターネットまたは Homenet ネットワークに配置されている場合に、そのコンピューターからの接続をテストするには、グループポリシー設定が正しいことを確認する必要があります。  
  
- クライアントに適切なグループポリシーがあることを確認するには  
  
- EDGE1 を使用してインターネットからの DirectAccess 接続をテストする  
  
- Win7_Clients_Site2 セキュリティグループへの変更の移動  
  
- 2-EDGE1 を使用してインターネットからの DirectAccess 接続をテストする  
  
## <a name="prerequisites"></a>前提条件  
両方のクライアントコンピューターを企業ネットワークネットワークに接続し、両方のクライアントコンピューターを再起動します。  
  
## <a name="verify-clients-have-the-correct-group-policy"></a><a name="policy"></a>クライアントに適切なグループポリシーがあることを確認する  
  
1.  CLIENT1 で、 **[スタート]** をクリックし、「 **powershell**」と入力して、 **[powershell]** を右クリックし、 **[詳細設定]** 、 **[管理者として実行]** の順にクリックします。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示された場合、表示された操作が目的の操作であることを確認して、 **[はい]** をクリックします。  
  
2.  Windows PowerShell ウィンドウで、「 **ipconfig** 」と入力し、enter キーを押します。  
  
    ネットワークアダプターの IPv4 アドレスが10.0.0 で始まることを確認します。  
  
3.  Windows PowerShell ウィンドウで、「 **get-dnsclientnrptpolicy** 」と入力し、enter キーを押します。 DirectAccess の名前解決ポリシー テーブル (NRPT) エントリが表示されます。  
  
    -   corp.contoso.com-これらの設定は、corp.contoso.com へのすべての接続を、IPv6 アドレス 2001: db8: 1:: 2 または 2001: db8: 2::20 で、いずれかの DirectAccess DNS サーバーで解決する必要があることを示します。  
  
    -   nls.corp.contoso.com-これらの設定は、nls.corp.contoso.com という名前の除外があることを示します。  
  
4.  次の手順については、Windows PowerShell ウィンドウを開いたままにしておきます。  
  
5.  次に、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[アクセサリ]** 、 **[windows powershell]** の順にクリックし、 **[windows powershell]** を右クリックして **[管理者として実行]** をクリックします。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示された場合、表示された操作が目的の操作であることを確認して、 **[はい]** をクリックします。  
  
6.  Windows PowerShell ウィンドウで、「 **ipconfig** 」と入力し、enter キーを押します。  
  
    ネットワークアダプターの IPv4 アドレスが10.0.0 で始まることを確認します。  
  
7.  Windows PowerShell ウィンドウで、「 **netsh namespace show policy** 」と入力し、enter キーを押します。  
  
    出力には、次の2つのセクションがあります。  
  
    -   . corp.contoso.com-これらの設定は、IPv6 アドレス 2001: db8: 1:: 2 を使用して、corp.contoso.com へのすべての接続を DirectAccess DNS サーバーで解決する必要があることを示します。  
  
    -   nls.corp.contoso.com-これらの設定は、nls.corp.contoso.com という名前の除外があることを示します。  
  
8.  次の手順については、Windows PowerShell ウィンドウを開いたままにしておきます。  
  
## <a name="test-directaccess-connectivity-from-the-internet-through-edge1"></a><a name="EDGE1"></a>EDGE1 を使用してインターネットからの DirectAccess 接続をテストする  
  
1. インターネットネットワークから EDGE1 を抜いてください。  
  
2. CLIENT1 とユーザーをネットワークスイッチから抜いて、インターネットスイッチに接続します。 30秒間待機します。  
  
3. CLIENT1 の Windows PowerShell ウィンドウで、「 **ipconfig/all** 」と入力し、enter キーを押します。  
  
4. Ipconfig コマンドの出力を確認します。  
  
   クライアントコンピューターがインターネットに接続され、パブリック IPv4 アドレスを持つようになります。 DirectAccess クライアントにパブリック IPv4 アドレスがある場合は、Teredo または IP-HTTPS IPv6 移行テクノロジを使用して、DirectAccess クライアントとリモートアクセスサーバー間の IPv4 インターネット経由で IPv6 メッセージをトンネリングします。 Teredo が推奨される移行テクノロジであることに注意してください。  
  
5. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 これにより、クライアントコンピューターが企業ネットワークに接続されたときに、クライアント DNS キャッシュに存在する可能性のある名前解決エントリがフラッシュされます。  
  
6. 次のコマンドを使用して、クライアントコンピューターが企業ネットワークに接続するために ip-https を使用するように、Teredo インターフェイスを無効にします。  
  
   ```  
   netsh interface teredo set state disable  
   ```  
  
7. EDGE1 経由で接続されていることを確認します。 「 **Netsh interface httpstunnel show** interface」と入力し、enter キーを押します。  
  
   出力には、URL: https://edge1.contoso.com:443/IPHTTPSが含まれている必要があります。  
  
   > [!TIP]  
   > CLIENT1 では、次の Windows PowerShell コマンドを実行することもできます: **NetIPHTTPSConfiguration**。 出力には、使用可能なサーバー URL 接続と現在アクティブなプロファイルが表示されます。  
  
8. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 この場合は、"2001: db8: 1:: 3" に割り当てられた IPv6 アドレスからの応答が表示されます。  
  
9. Windows PowerShell ウィンドウで、「 **ping 2-** Windows」と入力し、enter キーを押します。 2-3 に割り当てられた IPv6 アドレスからの応答が表示されます。この例では、2001: db8: 2:: 3 です。  
  
10. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 によって割り当てられた NAT64 アドレスからの応答が APP2 に表示されます。この例では、fd**c9: 9f4e: eb1b**: 7777:: a00: 4 です。 太字の値は、アドレスが生成される方法によって異なることに注意してください。  
  
    APP2 に ping を実行する機能は重要です。成功は、APP2 が IPv4 専用のリソースであるため、NAT64/DNS64 を使用して接続を確立できたことを示しているからです。  
  
11. Internet explorer を開き、Internet Explorer のアドレスバーに「 **https://app1/** 」と入力して、enter キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
12. Internet Explorer のアドレスバーに「 **https://2-app1/** 」と入力し、enter キーを押します。 2-3 の既定の web サイトが表示されます。  
  
13. Internet Explorer のアドレスバーに「 **https://app2/** 」と入力し、enter キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
14. **スタート**画面で、「<strong>\\\2-App1\Files</strong>」と入力し、enter キーを押します。 サンプルテキストファイルをダブルクリックします。  
  
    これは、EDGE1 経由で接続されているときに、corp2.corp.contoso.com ドメイン内のファイルサーバーに接続できることを示しています。  
  
15. **スタート**画面で、「<strong>\\\App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して IPv4 のみのサーバーに接続し、リソースドメイン内のリソースを取得できることを示しています。  
  
16. **スタート**画面で「**wf**」と入力し、enter キーを押します。  
  
17. セキュリティが強化された**Windows ファイアウォール**コンソールで、**パブリックプロファイル**のみがアクティブになっていることに注意してください。 DirectAccess が正しく機能するためには、Windows ファイアウォールが有効になっている必要があります。 Windows ファイアウォールが無効になっている場合、DirectAccess 接続は機能しません。  
  
18. コンソールの左側のウィンドウで、 **[監視]** ノードを展開し、 **[接続セキュリティの規則]** ノードをクリックします。 アクティブな接続セキュリティ規則 ( **Directaccess ポリシー-ClientToCorp**、 **Directaccess ポリシー-ClientToDNS64NAT64PrefixExemption**、 **Directaccess ポリシー-Clienttocorp**、および**directaccess ポリシー-clienttonla免除**) が表示されます。 中央のペインを右にスクロールすると、 **1 番目の [認証方法**] 列と **[2 番目の認証方法]** 列が表示されます。 最初のルール (ClientToCorp) が Kerberos V5 を使用してイントラネットトンネルを確立し、3番目のルール (clienttocorp) が NTLMv2 を使用してインフラストラクチャトンネルを確立することに注意してください。  
  
19. コンソールの左側のウィンドウで、 **[セキュリティアソシエーション]** ノードを展開し、 **[メインモード]** ノードをクリックします。 「インフラストラクチャトンネルのセキュリティアソシエーション」では、NTLMv2 と、Kerberos V5 を使用したイントラネットトンネルセキュリティの関連付けに注意してください。 **2 番目の認証方法**として **[ユーザー (Kerberos V5)]** と表示されているエントリを右クリックし、 **[プロパティ]** をクリックします。 **[全般]** タブで、 **2 番目の認証ローカル ID**が**CORP\User1**であることを確認します。これは、User1 が Kerberos を使用して CORP ドメインに対して正常に認証できたことを示します。  
  
20. この手順を、手順 3. で実行します。  
  
## <a name="move-client2-to-the-win7_clients_site2-security-group"></a><a name="secgroup"></a>Win7_Clients_Site2 セキュリティグループへの変更の移動  
  
1.  DC1 で **[スタート]** をクリックし、「 **dsa.msc**」と入力して、enter キーを押します。  
  
2.  Active Directory ユーザーとコンピューター コンソールで、 **corp.contoso.com/Users**を開き、**Win7_Clients_Site1** をダブルクリックします。  
  
3.  **[Win7_Clients_Site1 のプロパティ]** ダイアログボックスで、 **[メンバー]** タブをクリックし **、[** 削除]、 **[削除]** 、 **[はい]** の順にクリックして、 **[OK]** をクリックします。  
  
4.  **Win7_Clients_Site2**をダブルクリックし、Win7_Clients_Site2 の **[プロパティ]** ダイアログボックスで **[メンバー]** タブをクリックします。  
  
5.  **[追加]** をクリックし、 **[ユーザー、連絡先、コンピューター、またはサービスアカウントの選択]** ダイアログボックスで、 **[オブジェクトの種類]** をクリックし、 **[コンピューター]** を選択して、[ **OK]** をクリックします。  
  
6.  **[選択するオブジェクト名を入力してください**] ボックスに **「「」と入力し**、 **[OK]** をクリックします。  
  
7.  それを再起動し、corp/User1 アカウントを使用してログオンします。  
  
8.  その後、管理者特権の Windows PowerShell ウィンドウを開き、「 **netsh namespace show policy** 」と入力し、enter キーを押します。  
  
    出力には、次の2つのセクションがあります。  
  
    -   . corp.contoso.com-これらの設定は、corp.contoso.com へのすべての接続を、IPv6 アドレス 2001: db8: 2::20 と共に、DirectAccess DNS サーバーで解決する必要があることを示します。  
  
    -   nls.corp.contoso.com-これらの設定は、nls.corp.contoso.com という名前の除外があることを示します。  
  
## <a name="test-directaccess-connectivity-from-the-internet-through-2-edge1"></a><a name="DAConnect"></a>2-EDGE1 を使用してインターネットからの DirectAccess 接続をテストする  
  
1. 2 ~ EDGE1 をインターネットネットワークに接続します。  
  
2. インターネットネットワークから EDGE1 を取り外します。  
  
3. CLIENT1 で、管理者特権の Windows PowerShell ウィンドウを開きます。  
  
4. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 これにより、クライアントコンピューターが企業ネットワークに接続されたときに、クライアント DNS キャッシュに存在する可能性のある名前解決エントリがフラッシュされます。  
  
5. EDGE1 を使用して接続していることを確認します。 「 **Netsh interface httpstunnel show** interface」と入力し、enter キーを押します。  
  
   出力には、URL: https://2-edge1.contoso.com:443/IPHTTPSが含まれている必要があります。  
  
   > [!TIP]  
   > CLIENT1 では、次のコマンドも実行できます: **NetIPHTTPSConfiguration**。 出力には、使用可能なサーバー URL 接続と現在アクティブなプロファイルが表示されます。  
  
   > [!NOTE]  
   > CLIENT1 は、企業リソースへの接続に使用するサーバーを自動的に変更します。 コマンドの出力に EDGE1 への接続が表示されている場合は、約5分間待ってから、もう一度やり直してください。  
  
6. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 この場合は、"2001: db8: 1:: 3" に割り当てられた IPv6 アドレスからの応答が表示されます。  
  
7. Windows PowerShell ウィンドウで、「 **ping 2-** Windows」と入力し、enter キーを押します。 2-3 に割り当てられた IPv6 アドレスからの応答が表示されます。この例では、2001: db8: 2:: 3 です。  
  
8. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 によって割り当てられた NAT64 アドレスからの応答が APP2 に表示されます。この例では、fd**c9: 9f4e: eb1b**: 7777:: a00: 4 です。 太字の値は、アドレスが生成される方法によって異なることに注意してください。  
  
   APP2 に ping を実行する機能は重要です。成功は、APP2 が IPv4 専用のリソースであるため、NAT64/DNS64 を使用して接続を確立できたことを示しているからです。  
  
9. Internet explorer を開き、Internet Explorer のアドレスバーに「 **https://app1/** 」と入力して、enter キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
10. Internet Explorer のアドレスバーに「 **https://2-app1/** 」と入力し、enter キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
11. Internet Explorer のアドレスバーに「 **https://app2/** 」と入力し、enter キーを押します。 APP3 の既定の web サイトが表示されます。  
  
12. **スタート**画面で、「<strong>\\\App1\Files</strong>」と入力し、enter キーを押します。 サンプルテキストファイルをダブルクリックします。  
  
    これは、EDGE1 経由で接続されている場合に、corp.contoso.com ドメイン内のファイルサーバーに接続できたことを示しています。  
  
13. **スタート**画面で、「<strong>\\\App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して IPv4 のみのサーバーに接続し、リソースドメイン内のリソースを取得できることを示しています。  
  
14. 手順 3. の手順を繰り返します。  
  


