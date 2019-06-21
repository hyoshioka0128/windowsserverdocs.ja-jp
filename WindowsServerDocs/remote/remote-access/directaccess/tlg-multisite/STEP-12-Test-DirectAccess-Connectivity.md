---
title: 手順 12 テスト DirectAccess の接続
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65ac1c23-3a47-4e58-888d-9dde7fba1586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9c87f1823140fd6c92cf7df1f9d807545b50504e
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281543"
---
# <a name="step-12-test-directaccess-connectivity"></a>手順 12 テスト DirectAccess の接続

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

クライアント コンピューターからの接続をテストするには、インターネットまたはホームネット ネットワークに配置されているときに、前に、適切なグループ ポリシー設定があることを確認の操作を行う必要があります。  
  
- クライアントが適切なグループ ポリシーを持つことを確認するには  
  
- EDGE1 経由でインターネットから DirectAccess 接続をテストします。  
  
- CLIENT2 を Win7_Clients_Site2 セキュリティ グループに移動します。  
  
- 2 EDGE1 経由でインターネットから DirectAccess 接続をテストします。  
  
## <a name="prerequisites"></a>前提条件  
両方のクライアント コンピューターを企業ネットワークのネットワークに接続して、両方のクライアント コンピューターを再起動します。  
  
## <a name="policy"></a>クライアントが適切なグループ ポリシーを確認します  
  
1.  Client1 で、次のようにクリックします**開始**、型**powershell.exe**、を右クリック**powershell**、 をクリック**詳細設定**、をクリックして **。管理者として実行**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
2.  Windows PowerShell ウィンドウで、入力**ipconfig** ENTER キーを押します。  
  
    企業ネットワーク アダプター IPv4 アドレスが 10.0.0 で始まっていることを確認します。  
  
3.  Windows PowerShell ウィンドウで「 **Get-dnsclientnrptpolicy** ENTER キーを押します。 DirectAccess の名前解決ポリシー テーブル (NRPT) エントリが表示されます。  
  
    -   。 corp.contoso.com-これらの設定は、を corp.contoso.com にすべての接続が DirectAccess の DNS サーバーの IPv6 アドレス 2001:db8:1::2 または 2001:db8:2::20、のいずれかで解決することを示します。  
  
    -   nls.corp.contoso.com というこれらの設定は、nls.corp.contoso.com という名前の除外対象があることを示します。  
  
4.  Windows PowerShell ウィンドウは、次の手順を開いたままにしておきます。  
  
5.  Client2 で、次のようにクリックします**開始**、 をクリック**すべてのプログラム**、 をクリック**アクセサリ**、 をクリック**Windows PowerShell**、を右クリック **。Windows PowerShell**、 をクリックし、**管理者として実行**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
6.  Windows PowerShell ウィンドウで、入力**ipconfig** ENTER キーを押します。  
  
    企業ネットワーク アダプター IPv4 アドレスが 10.0.0 で始まっていることを確認します。  
  
7.  Windows PowerShell ウィンドウで、入力**netsh 名前空間は、ポリシーを表示する**ENTER キーを押します。  
  
    出力では、2 つのセクションがあります。  
  
    -   。 corp.contoso.com-これらの設定は、DirectAccess の DNS サーバー、IPv6 アドレスの 2001:db8:1::2 を corp.contoso.com にすべての接続を解決する必要があることを示します。  
  
    -   nls.corp.contoso.com というこれらの設定は、nls.corp.contoso.com という名前の除外対象があることを示します。  
  
8.  Windows PowerShell ウィンドウは、次の手順を開いたままにしておきます。  
  
## <a name="EDGE1"></a>EDGE1 経由でインターネットから DirectAccess 接続をテストします。  
  
1. インターネット ネットワークから 2 EDGE1 を取り外します。  
  
2. Corpnet スイッチから CLIENT1 および CLIENT2 を取り外すし、インターネット スイッチに接続します。 30 秒間待機します。  
  
3. Client1 で Windows PowerShell ウィンドウで、次のように入力します。 **ipconfig/all** ENTER キーを押します。  
  
4. Ipconfig コマンドの出力を確認します。  
  
   クライアント コンピューターでは、インターネットに接続されているようになりましたし、パブリック IPv4 アドレスを持ちます。 DirectAccess クライアントは、パブリック IPv4 アドレスがある、DirectAccess クライアントとリモート アクセス サーバー間、IPv4 インターネット経由で IPv6 メッセージをトンネリングするのに Teredo または IP-HTTPS IPv6 移行テクノロジが使用されます。 Teredo は、推奨される移行テクノロジであることに注意してください。  
  
5. Windows PowerShell ウィンドウで、入力**ipconfig/flushdns** ENTER キーを押します。 これにより、クライアント コンピューターが、企業ネットワークに接続されているときにまだクライアント DNS キャッシュに存在する名前解決エントリがフラッシュします。  
  
6. 次のコマンドを使用して企業ネットワークに接続するクライアント コンピューターが IP-HTTPS を使用することを確認して、Teredo インターフェイスを無効にします。  
  
   ```  
   netsh interface teredo set state disable  
   ```  
  
7. EDGE1 経由で接続していることを確認します。 型**netsh インターフェイス httpstunnel インターフェイスを表示する**ENTER キーを押します。  
  
   出力は、URL を含める必要があります: https://edge1.contoso.com:443/IPHTTPS します。  
  
   > [!TIP]  
   > Client1 で、次の Windows PowerShell コマンドを実行することもできます。**Get NetIPHTTPSConfiguration**します。 使用可能なサーバーの URL の接続と、現在アクティブなプロファイルが出力されます。  
  
8. Windows PowerShell ウィンドウで、入力**ping app1** ENTER キーを押します。 2001:db8:1::3 この例では、APP1 に割り当てられた IPv6 アドレスからの応答を表示する必要があります。  
  
9. Windows PowerShell ウィンドウで、入力**ping 2 app1** ENTER キーを押します。 2001:db8:2::3 この例では、2 APP1 に割り当てられている IPv6 アドレスからの応答を表示する必要があります。  
  
10. Windows PowerShell ウィンドウで、入力**ping app2** ENTER キーを押します。 ここでは、fd APP2 EDGE1 から割り当てられた NAT64 アドレスからの応答が表示**c9:9f4e:eb1b**: 7777::a00:4 します。 太字の値がアドレスを生成する方法のために異なることに注意してください。  
  
    APP2 の ping を実行する機能は、成功した場合は、APP2 が IPv4 唯一のリソースは、NAT64 と DNS64 を使用して接続を確立することができたことを示しているため、重要です。  
  
11. Internet Explorer のアドレス バーに Internet Explorer を開き、入力 **https://app1/** ENTER キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
12. Internet Explorer のアドレス バーに次のように入力します。 **https://2-app1/** ENTER キーを押します。 2 APP1 の既定の web サイトが表示されます。  
  
13. Internet Explorer のアドレス バーに次のように入力します。 **https://app2/** ENTER キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
14. **開始**画面で「<strong>\\\2-App1\Files</strong>し、ENTER キーを押します。 例のテキスト ファイルをダブルクリックします。  
  
    これは、corp2.corp.contoso.com ドメイン EDGE1 を通して接続したときに、ファイル サーバーに接続することができたことを示します。  
  
15. **開始**画面で「<strong>\\\App2\Files</strong>し、ENTER キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して、リソース ドメイン内のリソースを取得する IPv4 のみのサーバーに接続することができたことを示します。  
  
16. **開始**画面で「**wf.msc**、し、ENTER キーを押します。  
  
17. **セキュリティが強化された Windows ファイアウォール**コンソールで、だけであることを確認、**パブリック プロファイル**がアクティブになっています。 正常に動作する DirectAccess には、Windows ファイアウォールを有効にする必要があります。 Windows ファイアウォールを無効にすると、DirectAccess の接続は機能しません。  
  
18. コンソールの左側のウィンドウで、展開、**監視**ノード、およびクリック、**接続セキュリティ規則**ノード。 アクティブな接続のセキュリティ規則が表示されます。**DirectAccess ポリシー-ClientToCorp**、 **DirectAccess ポリシー-ClientToDNS64NAT64PrefixExemption**、 **DirectAccess ポリシー-ClientToInfra**、および**DirectAccessポリシー ClientToNlaExempt**します。 右を表示するのには、中央のウィンドウのスクロール、 **1 番目の認証方法**と**2 番目の認証方法**列。 最初のルール (ClientToCorp) では、Kerberos V5 を使用して、イントラネット トンネルを確立するために 3 番目の規則 (ClientToInfra) は、インフラストラクチャ トンネルを確立するために NTLMv2 を使用していることを確認します。  
  
19. コンソールの左側のウィンドウで、展開、**セキュリティ アソシエーション**ノード、およびクリック、**メイン モード**ノード。 NTLMv2 を使用して、インフラストラクチャ トンネルのセキュリティ アソシエーションと Kerberos V5 を使用して、イントラネット トンネルのセキュリティ アソシエーションに注意してください。 表示するエントリを右クリックして**ユーザー (Kerberos V5)** として、 **2 番目の認証方法** をクリック**プロパティ**します。 **全般** タブに注意してください、 **2 番目の認証のローカル ID**は**corp \user1**User1 を使用して CORP ドメインに正常に認証できるようにしたことを示すKerberos。  
  
20. CLIENT2 で、手順 3 からこの手順を繰り返します。  
  
## <a name="secgroup"></a>CLIENT2 を Win7_Clients_Site2 セキュリティ グループに移動します。  
  
1.  DC1 で、次のようにクリックします。**開始**、型**dsa.msc**、し、ENTER キーを押します。  
  
2.  Active Directory ユーザーとコンピューター コンソールで、開き**corp.contoso.com/Users**  をダブルクリックします**Win7_Clients_Site1**します。  
  
3.  **Win7_Clients_Site1 プロパティ**ダイアログ ボックスで、をクリックして、**メンバー**  タブで、をクリックして**CLIENT2**、 をクリックして**削除**をクリックします **。はい**、 をクリックし、 **OK**。  
  
4.  ダブルクリック**Win7_Clients_Site2**、し、 **Win7_Clients_Site2 プロパティ**ダイアログ ボックスで、をクリックして、**メンバー**  タブ。  
  
5.  をクリックして**追加**、し、 **[ユーザー、連絡先、コンピューター、またはサービス アカウント**ダイアログ ボックスで、をクリックして**オブジェクトの種類**を選択します**コンピューター**、] をクリックし、 **OK**します。  
  
6.  **を選択するオブジェクト名の入力**、型**CLIENT2**、順にクリックします**OK**。  
  
7.  CLIENT2 を再起動し、corp/User1 アカウントを使用してログオンします。  
  
8.  CLIENT2 で、管理者特権の Windows PowerShell ウィンドウを開き型**netsh 名前空間は、ポリシーを表示する**ENTER キーを押します。  
  
    出力では、2 つのセクションがあります。  
  
    -   。 corp.contoso.com-これらの設定は、DirectAccess の DNS サーバー、IPv6 アドレスの 2001:db8:2::20 を corp.contoso.com にすべての接続を解決する必要があることを示します。  
  
    -   nls.corp.contoso.com というこれらの設定は、nls.corp.contoso.com という名前の除外対象があることを示します。  
  
## <a name="DAConnect"></a>2 EDGE1 経由でインターネットから DirectAccess 接続をテストします。  
  
1. 2 EDGE1 をインターネット ネットワークに接続します。  
  
2. インターネット ネットワークから EDGE1 を取り外します。  
  
3. CLIENT1 で管理者特権での Windows PowerShell ウィンドウを開きます。  
  
4. Windows PowerShell ウィンドウで、入力**ipconfig/flushdns** ENTER キーを押します。 これにより、クライアント コンピューターが、企業ネットワークに接続されているときにまだクライアント DNS キャッシュに存在する名前解決エントリがフラッシュします。  
  
5. 2 EDGE1 経由で接続していることを確認します。 型**netsh インターフェイス httpstunnel インターフェイスを表示する**ENTER キーを押します。  
  
   出力は、URL を含める必要があります: https://2-edge1.contoso.com:443/IPHTTPS します。  
  
   > [!TIP]  
   > Client1 で、次のコマンドを実行することもできます。**Get NetIPHTTPSConfiguration**します。 使用可能なサーバーの URL の接続と、現在アクティブなプロファイルが出力されます。  
  
   > [!NOTE]  
   > CLIENT1 は、会社のリソースに接続するサーバーを自動的に変更します。 コマンドの出力では、EDGE1 への接続が表示される場合約 5 分間待機してからやり直してください。  
  
6. Windows PowerShell ウィンドウで、入力**ping app1** ENTER キーを押します。 2001:db8:1::3 この例では、APP1 に割り当てられた IPv6 アドレスからの応答を表示する必要があります。  
  
7. Windows PowerShell ウィンドウで、入力**ping 2 app1** ENTER キーを押します。 2001:db8:2::3 この例では、2 APP1 に割り当てられている IPv6 アドレスからの応答を表示する必要があります。  
  
8. Windows PowerShell ウィンドウで、入力**ping app2** ENTER キーを押します。 ここでは、fd APP2 EDGE1 から割り当てられた NAT64 アドレスからの応答が表示**c9:9f4e:eb1b**: 7777::a00:4 します。 太字の値がアドレスを生成する方法のために異なることに注意してください。  
  
   APP2 の ping を実行する機能は、成功した場合は、APP2 が IPv4 唯一のリソースは、NAT64 と DNS64 を使用して接続を確立することができたことを示しているため、重要です。  
  
9. Internet Explorer のアドレス バーに Internet Explorer を開き、入力 **https://app1/** ENTER キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
10. Internet Explorer のアドレス バーに次のように入力します。 **https://2-app1/** ENTER キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
11. Internet Explorer のアドレス バーに次のように入力します。 **https://app2/** ENTER キーを押します。 APP3 の既定の web サイトが表示されます。  
  
12. **開始**画面で「<strong>\\\App1\Files</strong>し、ENTER キーを押します。 例のテキスト ファイルをダブルクリックします。  
  
    これは、2 EDGE1 を通して接続したときに、corp.contoso.com ドメイン内のファイル サーバーに接続することができたことを示します。  
  
13. **開始**画面で「<strong>\\\App2\Files</strong>し、ENTER キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して、リソース ドメイン内のリソースを取得する IPv4 のみのサーバーに接続することができたことを示します。  
  
14. 手順 3 から CLIENT2 では、この手順を繰り返します。  
  


