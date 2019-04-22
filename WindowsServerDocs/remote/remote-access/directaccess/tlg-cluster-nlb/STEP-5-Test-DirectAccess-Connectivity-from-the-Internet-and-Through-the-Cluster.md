---
title: 手順 5 DirectAccess 接続をテスト クラスターと、インターネットから
description: このトピックは一部のテスト ラボ ガイド - Windows Server 2016 で Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8399bdfa-809a-45e4-9963-f9b6a631007f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49b3f6f68bf30ff197b51643f9f1b8f36cc76f19
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825973"
---
# <a name="step-5-test-directaccess-connectivity-from-the-internet-and-through-the-cluster"></a>手順 5 DirectAccess 接続をテスト クラスターと、インターネットから

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

CLIENT1 は、DirectAccess のテストの準備ができました。  
  
- インターネットからの DirectAccess の接続をテストします。 CLIENT1 は、シミュレートされたインターネットに接続します。 シミュレートされたインターネットに接続しているときに、クライアントには、パブリック IPv4 アドレスが割り当てられます。 DirectAccess クライアントには、パブリック IPv4 アドレスが割り当てられますが、IPv6 移行テクノロジを使用して、リモート アクセス サーバーへの接続を確立しようとします。  
  
- クラスターによって、DirectAccess クライアント接続をテストします。 クラスターの機能をテストします。 テストを開始する前に、EDGE1 と EDGE2 の両方を少なくとも 5 分間シャットすることをお勧めします。 多くの ARP キャッシュ タイムアウトおよび NLB に関連する変更が含まれますが、この理由があります。 テスト ラボでの NLB の構成を検証するときに患者に構成の変更はすぐに反映されませんまで接続で、一定期間が経過した後にする必要があります。 これは、次のタスクを実行する場合に注意してください。  
  
    > [!TIP]  
    > この手順を実行する前に、Internet Explorer のキャッシュをクリアし、接続のテストと web ページをキャッシュから取得しないいるかどうかを確認する別のリモート アクセス サーバー経由の接続をテストするたびにすることをお勧めします。  
  
## <a name="test-directaccess-connectivity-from-the-internet"></a>インターネットから DirectAccess 接続をテストします。  
  
1.  企業ネットワーク スイッチから CLIENT1 を外し、インターネット スイッチに接続します。 30 秒間待機します。  
  
2.  管理者特権で Windows PowerShell ウィンドウで、次のように入力します。 **ipconfig/flushdns** ENTER キーを押します。 これにより、クライアント コンピューターが、企業ネットワークに接続されているときにまだクライアント DNS キャッシュに存在する名前解決エントリがフラッシュします。  
  
3.  Windows PowerShell ウィンドウで、入力**Get-dnsclientnrptpolicy** ENTER キーを押します。  
  
    出力には、名前解決ポリシー テーブル (NRPT) の現在の設定が表示されます。 これらの設定を指定するすべての接続。 corp.contoso.com を IPv6 アドレスの 2001:db8:1::2、リモート アクセス DNS サーバーで解決できる必要があります。 また、nls.corp.contoso.com という名前が除外されることを示す NRPT エントリがあります。除外リストの名前は、リモート アクセス DNS サーバーから応答されません。 リモート アクセス サーバーへの接続を確認するリモート アクセス DNS サーバーの IP アドレスに ping を実行します。たとえば、2001:db8:1::2 の ping を実行することができます。  
  
4.  Windows PowerShell ウィンドウで、入力**ping app1** ENTER キーを押します。 IPv6 アドレスからの応答は、2001:db8:1::3 この例では、APP1 に表示されます。  
  
5.  Windows PowerShell ウィンドウで、入力**ping app2** ENTER キーを押します。 EDGE1 から割り当てられた NAT64 アドレスから APP2 (この例では fdc9:9f4e:eb1b:7777::a00:4) に返信があります。  
  
    APP2 の ping を実行する機能は、成功した場合は、APP2 が IPv4 唯一のリソースは、NAT64 と DNS64 を使用して接続を確立することができたことを示しているため、重要です。  
  
6.  Windows PowerShell ウィンドウは、次の手順を開いたままにしておきます。  
  
7.  Internet Explorer のアドレス バーに Internet Explorer を開き、入力**https://app1/** ENTER キーを押します。 APP1 の既定の IIS Web サイトが表示されます。  
  
8.  Internet Explorer のアドレス バーに次のように入力します。 **https://app2/** ENTER キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
9. **開始**画面で「**\\\App2\Files**し、ENTER キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。  
  
    これは、SMB を使用して、リソース ドメイン内のリソースを取得する IPv4 のみのサーバーに接続することができたことを示します。  
  
10. **開始**画面で「**wf.msc**、し、ENTER キーを押します。  
  
11. **セキュリティが強化された Windows ファイアウォール**コンソールで、だけであることを確認、**プライベート**または**パブリック プロファイル**がアクティブになっています。 正常に動作する DirectAccess には、Windows ファイアウォールを有効にする必要があります。 Windows ファイアウォールを無効にすると、DirectAccess の接続は機能しません。  
  
12. コンソールの左側のウィンドウで、展開、**監視**ノード、およびクリック、**接続セキュリティ規則**ノード。 アクティブな接続のセキュリティ規則が表示されます。**DirectAccess ポリシー-ClientToCorp**、 **DirectAccess ポリシー-ClientToDNS64NAT64PrefixExemption**、 **DirectAccess ポリシー-ClientToInfra**、および**DirectAccessポリシー ClientToNlaExempt**します。 右を表示するのには、中央のウィンドウのスクロール、 **1 番目の認証方法**と**2 番目の認証方法**列。 最初のルール (ClientToCorp) では、Kerberos V5 を使用して、イントラネット トンネルを確立するために 3 番目の規則 (ClientToInfra) は、インフラストラクチャ トンネルを確立するために NTLMv2 を使用していることを確認します。  
  
13. コンソールの左側のウィンドウで、展開、**セキュリティ アソシエーション**ノード、およびクリック、**メイン モード**ノード。 NTLMv2 を使用して、インフラストラクチャ トンネルのセキュリティ アソシエーションと Kerberos V5 を使用して、イントラネット トンネルのセキュリティ アソシエーションに注意してください。 表示するエントリを右クリックして**ユーザー (Kerberos V5)** として、 **2 番目の認証方法** をクリック**プロパティ**します。 **全般** タブに注意してください、 **2 番目の認証のローカル ID**は**corp \user1**User1 を使用して CORP ドメインに正常に認証できるようにしたことを示すKerberos。  
  
## <a name="test-directaccess-client-connectivity-through-the-cluster"></a>クラスターでの DirectAccess クライアント接続をテストします。  
  
1.  EDGE2 では、正常なシャット ダウンを実行します。  
  
    ネットワーク負荷分散マネージャーを使用して、これらのテストを実行するときに、サーバーの状態を表示することができます。  
  
2.  Client1 で Windows PowerShell ウィンドウで、次のように入力します。 **ipconfig/flushdns** ENTER キーを押します。 これにより、まだクライアント DNS キャッシュに残っている名前解決エントリがフラッシュします。  
  
3.  Windows PowerShell ウィンドウで、APP1 および APP2 に対して ping を実行します。 これらのリソースの両方から応答を受信する必要があります。  
  
4.  **開始**画面で「**\\\app2\files**します。 APP2 コンピューター上の共有フォルダーが表示されます。 APP2 のファイル共有を開くことができますでは、ユーザーの Kerberos 認証を必要とする 2 番目のトンネルが正しく動作していることを示します。  
  
5.  Internet Explorer を開き、web サイトを開きます https://app1/と https://app2/します。 両方の web サイトを開くことができますを確認する最初と 2 つ目の両方のトンネルが機能しているとします。 Internet Explorer を閉じます。  
  
6.  EDGE2 コンピューターを起動します。  
  
7.  EDGE1 では、正常なシャット ダウンを実行します。  
  
8.  5 分間待機し、CLIENT1 に戻ります。 手順 2. ~ 5. を実行します。 CLIENT1 が透過的にフェールオーバーする EDGE2 EDGE1 は使用できなくなった後できたことを確認します。
