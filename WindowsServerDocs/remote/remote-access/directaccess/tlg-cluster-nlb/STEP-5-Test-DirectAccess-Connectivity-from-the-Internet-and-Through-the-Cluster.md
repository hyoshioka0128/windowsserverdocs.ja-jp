---
title: 手順 5. インターネットとクラスターを使用した DirectAccess 接続のテスト
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1b5708e51b2653444fb3eb636baac6a165dfc55d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404847"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>手順 5. インターネットとクラスターを使用した DirectAccess 接続のテスト

>適用先:Windows Server (半期チャネル)、Windows Server 2016

CLIENT1 は、DirectAccess テストの準備ができました。  
  
- インターネットからの DirectAccess 接続をテストします。 CLIENT1 をシミュレートされたインターネットに接続します。 シミュレートされたインターネットに接続されている場合、クライアントにはパブリック IPv4 アドレスが割り当てられます。 DirectAccess クライアントにパブリック IPv4 アドレスが割り当てられると、IPv6 移行テクノロジを使用してリモートアクセスサーバーへの接続を確立しようとします。  
  
- クラスターを介して DirectAccess クライアント接続をテストします。 クラスター機能をテストします。 テストを開始する前に、少なくとも5分間 EDGE1 と EDGE2 の両方をシャットダウンすることをお勧めします。 これにはさまざまな理由があります。これには、ARP キャッシュのタイムアウトや NLB に関連する変更が含まれます。 テストラボで NLB 構成を検証するときは、しばらく時間が経過するまで、構成の変更が接続にすぐに反映されないため、しばらくお待ちください。 これは、次のタスクを実行するときに注意する必要があります。  
  
    > [!TIP]  
    > この手順を実行する前に Internet Explorer のキャッシュをクリアし、別のリモートアクセスサーバーを介して接続をテストして、接続をテストしていること、および web ページがキャッシュから取得されていないことを確認することをお勧めします。  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>インターネットからの DirectAccess 接続をテストする  
  
1. CLIENT1 をネットワークスイッチから取り外し、インターネットスイッチに接続します。 30秒間待機します。  
  
2. 管理者特権の Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 これにより、クライアントコンピューターが企業ネットワークに接続されたときに、クライアント DNS キャッシュに存在する可能性のある名前解決エントリがフラッシュされます。  
  
3. Windows PowerShell ウィンドウで、「 **get-dnsclientnrptpolicy** 」と入力し、enter キーを押します。  
  
   出力には、名前解決ポリシー テーブル (NRPT) の現在の設定が表示されます。 これらの設定は、IPv6 アドレス 2001: db8: 1:: 2 を使用して、corp.contoso.com へのすべての接続をリモートアクセス DNS サーバーで解決する必要があることを示しています。 また、nls.corp.contoso.com という名前が除外されることを示す NRPT エントリがあります。除外リストの名前は、リモート アクセス DNS サーバーから応答されません。 リモートアクセス DNS サーバーの IP アドレスに対して ping を実行し、リモートアクセスサーバーへの接続を確認することができます。たとえば、2001: db8: 1:: 2 に ping を実行できます。  
  
4. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 この場合は 2001: db8: 1:: 3 という IPv6 アドレスからの応答が表示されます。  
  
5. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 から割り当てられた NAT64 アドレスから APP2 (この例では fdc9:9f4e:eb1b:7777::a00:4) に返信があります。  
  
   APP2 に ping を実行する機能は重要です。成功は、APP2 が IPv4 専用のリソースであるため、NAT64/DNS64 を使用して接続を確立できたことを示しているからです。  
  
6. 次の手順については、Windows PowerShell ウィンドウを開いたままにしておきます。  
  
7. Internet explorer を開き、Internet Explorer のアドレスバーに **https://app1/** を入力して、enter キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
8. Internet Explorer のアドレスバーに「 **https://app2/** 」と入力し、enter キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
9. **スタート**画面で、「<strong>\\ \ App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して IPv4 のみのサーバーに接続し、リソースドメイン内のリソースを取得できることを示しています。  
  
10. **スタート**画面で「**wf**」と入力し、enter キーを押します。  
  
11. セキュリティが強化された**Windows ファイアウォール**コンソールで、**プライベート**プロファイルまたは**パブリックプロファイル**のみがアクティブになっていることに注意してください。 DirectAccess が正しく機能するためには、Windows ファイアウォールが有効になっている必要があります。 Windows ファイアウォールが無効になっている場合、DirectAccess 接続は機能しません。  
  
12. コンソールの左側のウィンドウで、 **[監視]** ノードを展開し、 **[接続セキュリティの規則]** ノードをクリックします。 アクティブな接続セキュリティ規則が表示されます。**Directaccess ポリシー-ClientToCorp**、 **Directaccess ポリシー-ClientToDNS64NAT64PrefixExemption**、 **Directaccess ポリシー-Clienttocorp**、および**directaccess ポリシー-clienttonla免除**。 中央のペインを右にスクロールすると、 **1 番目の [認証方法**] 列と **[2 番目の認証方法]** 列が表示されます。 最初のルール (ClientToCorp) が Kerberos V5 を使用してイントラネットトンネルを確立し、3番目のルール (clienttocorp) が NTLMv2 を使用してインフラストラクチャトンネルを確立することに注意してください。  
  
13. コンソールの左側のウィンドウで、 **[セキュリティアソシエーション]** ノードを展開し、 **[メインモード]** ノードをクリックします。 「インフラストラクチャトンネルのセキュリティアソシエーション」では、NTLMv2 と、Kerberos V5 を使用したイントラネットトンネルセキュリティの関連付けに注意してください。 **2 番目の認証方法**として **[ユーザー (Kerberos V5)]** と表示されているエントリを右クリックし、 **[プロパティ]** をクリックします。 **[全般]** タブで、 **2 番目の認証ローカル ID**が**CORP\User1**であることを確認します。これは、User1 が Kerberos を使用して CORP ドメインに対して正常に認証できたことを示します。  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>クラスターを使用した DirectAccess クライアント接続のテスト  
  
1. EDGE2 で正常なシャットダウンを実行します。  
  
   これらのテストの実行時に、ネットワーク負荷分散マネージャーを使用してサーバーの状態を表示できます。  
  
2. CLIENT1 の Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 これにより、クライアント DNS キャッシュにまだ存在する可能性がある名前解決エントリがフラッシュされます。  
  
3. Windows PowerShell ウィンドウで、APP2 と ping を行います。 両方のリソースから応答を受信する必要があります。  
  
4. **スタート**画面で、「<strong>\\ \ app2\files</strong>」と入力します。 APP2 コンピューターに共有フォルダーが表示されます。 APP2 でファイル共有を開く機能は、ユーザーに対して Kerberos 認証を必要とする2番目のトンネルが正常に機能していることを示します。  
  
5. Internet Explorer を開き、web サイト https://app1/ と https://app2/ を開きます。 両方の web サイトを開く機能により、1番目と2番目のトンネルが稼働していることが確認されます。 Internet Explorer を閉じます。  
  
6. EDGE2 コンピューターを起動します。  
  
7. EDGE1 で、正常なシャットダウンを実行します。  
  
8. 5分間待ってから CLIENT1 に戻ります。 手順2-5 を実行します。 これにより、EDGE1 が使用不能になった後に CLIENT1 が EDGE2 に透過的にフェールオーバーできることが確認されます。
