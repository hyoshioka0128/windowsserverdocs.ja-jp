---
title: 手順 13 NAT デバイスの背後からの DirectAccess 接続をテストする
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9422f3840899edc7dad6b51dd42a95eafb3856a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860345"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>手順 13 NAT デバイスの背後からの DirectAccess 接続をテストする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

DirectAccess クライアントを NAT デバイスまたは Web プロキシ サーバーの背後からインターネットに接続すると、DirectAccess クライアントでは、リモート アクセス サーバーへの接続に Teredo または IP-HTTPS が使用されます。 NAT デバイスが、リモートアクセスサーバーのパブリック IP アドレスへの発信 UDP ポート3544を有効にすると、Teredo が使用されます。 Teredo を使用できない場合、DirectAccess クライアントは、発信 TCP ポート 443 の IP-HTTPS にフォールバックされます。その結果、従来の SSL ポートで、ファイアウォールまたは Web プロキシ サーバーを経由してアクセスできるようになります。 Web プロキシに認証が必要な場合、IP-HTTPS 接続は失敗します。 また、Web プロキシが発信 SSL 検査を実行している場合も IP-HTTPS 接続は失敗します。これは、HTTPS セッションがリモート アクセス サーバーではなく Web プロキシで中断されるためです。  
  
両方のクライアント コンピューターで次の手順を実行します。  
  
1. Teredo 接続をテストします。 最初のテストセットは、DirectAccess クライアントが Teredo を使用するように構成されている場合に実行されます。 これは、NAT デバイスで UDP ポート 3544 への発信アクセスを許可する場合の自動設定です。 まず CLIENT1 でテストを実行し、その後、そのテストを実行します。  
  
2. Ip-https 接続をテストします。 2番目のテストセットは、IP-HTTPS を使用するように DirectAccess クライアントが構成されている場合に実行されます。 IP-HTTPS 接続を実行するために、クライアント コンピューターの Teredo を無効にします。 まず CLIENT1 でテストを実行し、その後、そのテストを実行します。  
  
## <a name="prerequisites"></a>前提条件  
EDGE1 と EDGE1 がまだ実行されていない場合は開始し、インターネットサブネットに接続されていることを確認します。  
  
これらのテストを実行する前に、インターネットスイッチから CLIENT1 とを取り外し、Homenet スイッチに接続します。 現在のネットワークを定義するネットワークの種類を確認するメッセージが表示されたら、 **[ホームネットワーク]** を選択します。  
  
## <a name="test-teredo-connectivity"></a><a name="TeredoCLIENT1"></a>Teredo 接続をテストする  
  
1. CLIENT1 で、管理者特権の Windows PowerShell ウィンドウを開きます。  
  
2. Teredo アダプターを有効にし、「 **netsh interface Teredo set state enterpriseclient**」と入力して、enter キーを押します。  
  
3. Windows PowerShell ウィンドウで、「 **ipconfig/all** 」と入力し、enter キーを押します。  
  
4. ipconfig コマンドの出力を確認します。  
  
   このコンピューターは、NAT デバイスの背後からインターネットに接続できるようになり、プライベート IPv4 アドレスが割り当てられます。 DirectAccess クライアントが NAT デバイスの背後にあり、プライベート IPv4 アドレスが割り当てられている場合、推奨される IPv6 移行テクノロジは Teredo です。 Ipconfig コマンドの出力を見ると、トンネルアダプター Teredo トンネリング擬似インターフェイスに関するセクションと、「Microsoft Teredo トンネリングアダプター」という説明が表示されます。 IP アドレスは、2001:0 で始まり、Teredo と一致している必要があります。先. Teredo トンネルアダプターの既定のゲートウェイが ':: ' と表示されます。  
  
5. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。  
  
   その結果、クライアント コンピューターをインターネットに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。  
  
6. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。  
  
7. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 によって割り当てられた NAT64 アドレスからの応答が APP2 に表示されます。この例では、fd**c9: 9f4e: eb1b**: 7777:: a00: 4 です。 太字の値は、アドレスが生成される方法によって異なることに注意してください。  
  
8. Windows PowerShell ウィンドウで、「 **ping 2-** Windows」と入力し、enter キーを押します。 IPv6 アドレス (2-3、2001: db8: 2:: 3) からの応答が表示されます。  
  
9. Internet explorer を開き、Internet Explorer のアドレスバーに「 **https://2-app1/** 」と入力して、enter キーを押します。 2-3 に既定の IIS web サイトが表示されます。  
  
10. Internet Explorer のアドレスバーに「 **https://app2/** 」と入力し、enter キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
11. **スタート**画面で、「<strong>\\\App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。  
  
12. この手順を連続で繰り返します。  
  
## <a name="test-ip-https-connectivity"></a><a name="IPHTTPS_CLIENT1"></a>Ip-https 接続のテスト  
  
1. CLIENT1 で、管理者特権の Windows PowerShell ウィンドウを開き、「 **netsh interface teredo set state disabled** 」と入力し、enter キーを押します。 その結果、クライアント コンピューターで Teredo が無効になり、クライアント コンピューターが IP-HTTPS を使用するように構成できます。 コマンドの完了時に、**OK** 応答が表示されます。  
  
2. Windows PowerShell ウィンドウで、「 **ipconfig/all** 」と入力し、enter キーを押します。  
  
3. ipconfig コマンドの出力を確認します。 このコンピューターは、NAT デバイスの背後からインターネットに接続できるようになり、プライベート IPv4 アドレスが割り当てられます。 Teredo は無効になり、DirectAccess クライアントは IP-HTTPS にフォールバックします。 Ipconfig コマンドの出力を見ると、[トンネルアダプター iphttpsinterface] のセクションに、2001: db8: 1: 1000 または 2001: db8: 2: 2000 と一致する IP アドレスが表示されます。これは、次のプレフィックスに基づいた ip-https アドレスです。DirectAccess のセットアップ時に構成されます。 IPHTTPSInterface トンネルアダプターの既定のゲートウェイは表示されません。  
  
4. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 その結果、クライアント コンピューターを社内ネットワークに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。  
  
5. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。  
  
6. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 によって割り当てられた NAT64 アドレスからの応答が APP2 に表示されます。この例では、fd**c9: 9f4e: eb1b**: 7777:: a00: 4 です。 太字の値は、アドレスが生成される方法によって異なることに注意してください。  
  
7. Windows PowerShell ウィンドウで、「 **ping 2-** Windows」と入力し、enter キーを押します。 IPv6 アドレス (2-3、2001: db8: 2:: 3) からの応答が表示されます。  
  
8. Internet explorer を開き、Internet Explorer のアドレスバーに「 **https://2-app1/** 」と入力して、enter キーを押します。 2-3 に既定の IIS web サイトが表示されます。  
  
9. Internet Explorer のアドレスバーに「 **https://app2/** 」と入力し、enter キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
10. **スタート**画面で、「<strong>\\\App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。  
  
11. この手順を連続で繰り返します。  
  


