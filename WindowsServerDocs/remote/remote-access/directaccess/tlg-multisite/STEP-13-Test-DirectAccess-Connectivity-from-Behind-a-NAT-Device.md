---
title: 手順 13 NAT デバイスの背後から DirectAccess 接続のテスト
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 796825c3-5e3e-4745-a921-25ab90b95ede
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 34a65434a0035c60c888170e779496653ad0ab6d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283200"
---
# <a name="step-13-test-directaccess-connectivity-from-behind-a-nat-device"></a>手順 13 NAT デバイスの背後から DirectAccess 接続のテスト

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DirectAccess クライアントを NAT デバイスまたは Web プロキシ サーバーの背後からインターネットに接続すると、DirectAccess クライアントでは、リモート アクセス サーバーへの接続に Teredo または IP-HTTPS が使用されます。 NAT デバイスにより、リモート アクセス サーバーのパブリック IP アドレスに UDP ポート 3544 の送信、Teredo が使用されます。 Teredo を使用できない場合、DirectAccess クライアントは、発信 TCP ポート 443 の IP-HTTPS にフォールバックされます。その結果、従来の SSL ポートで、ファイアウォールまたは Web プロキシ サーバーを経由してアクセスできるようになります。 Web プロキシに認証が必要な場合、IP-HTTPS 接続は失敗します。 また、Web プロキシが発信 SSL 検査を実行している場合も IP-HTTPS 接続は失敗します。これは、HTTPS セッションがリモート アクセス サーバーではなく Web プロキシで中断されるためです。  
  
両方のクライアント コンピューターで次の手順を実行します。  
  
1. Teredo 接続をテストします。 Teredo を使用する DirectAccess クライアントが構成されている場合、最初の一連のテストが実行されます。 これは、NAT デバイスで UDP ポート 3544 への発信アクセスを許可する場合の自動設定です。 まず CLIENT1 でテストを実行し、CLIENT2 で、テストを実行します。  
  
2. IP-HTTPS 接続をテストします。 テストの 2 番目のセットは、IP-HTTPS を使用する DirectAccess クライアントが構成されている場合に実行されます。 IP-HTTPS 接続を実行するために、クライアント コンピューターの Teredo を無効にします。 まず CLIENT1 でテストを実行し、CLIENT2 で、テストを実行します。  
  
## <a name="prerequisites"></a>前提条件  
既に実行されていないと、インターネット サブネットに接続されていることを確認する場合は、EDGE1 と 2 EDGE1 を開始します。  
  
これらのテストを実行する前に、インターネット スイッチから CLIENT1 および CLIENT2 を取り外すし、ホームネット スイッチに接続します。 現在のネットワークを定義するには、選択するネットワークの種類を求められた場合**ホーム ネットワーク**します。  
  
## <a name="TeredoCLIENT1"></a>Teredo 接続をテストします。  
  
1. CLIENT1 で管理者特権での Windows PowerShell ウィンドウを開きます。  
  
2. 有効にする、Teredo アダプター型**netsh インターフェイス teredo 設定状態 enterpriseclient**、し、ENTER キーを押します。  
  
3. Windows PowerShell ウィンドウで、入力**ipconfig/all** ENTER キーを押します。  
  
4. ipconfig コマンドの出力を確認します。  
  
   このコンピューターは、NAT デバイスの背後からインターネットに接続できるようになり、プライベート IPv4 アドレスが割り当てられます。 DirectAccess クライアントが NAT デバイスの背後にあり、プライベート IPv4 アドレスが割り当てられている場合、推奨される IPv6 移行テクノロジは Teredo です。 場合は、ipconfig コマンドの出力を見ると、する必要がありますトンネル アダプターの Teredo トンネリング擬似インターフェイスのセクションと説明を表示し、Microsoft Teredo Tunneling Adapter Teredo と一致 2001:0 で始まる IP アドレスを持つアドレス。 として Teredo のトンネル アダプターのデフォルト ゲートウェイを表示する必要があります ':: '。  
  
5. Windows PowerShell ウィンドウで、入力**ipconfig/flushdns** ENTER キーを押します。  
  
   その結果、クライアント コンピューターをインターネットに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。  
  
6. Windows PowerShell ウィンドウで、入力**ping app1** ENTER キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。  
  
7. Windows PowerShell ウィンドウで、入力**ping app2** ENTER キーを押します。 ここでは、fd APP2 EDGE1 から割り当てられた NAT64 アドレスからの応答が表示**c9:9f4e:eb1b**: 7777::a00:4 します。 太字の値がアドレスを生成する方法のために異なることに注意してください。  
  
8. Windows PowerShell ウィンドウで、入力**ping 2 app1** ENTER キーを押します。 2 APP1 2001:db8:2::3 の IPv6 アドレスからの応答が表示されます。  
  
9. Internet Explorer のアドレス バーに Internet Explorer を開き、入力 **https://2-app1/** ENTER キーを押します。 2 APP1 で、既定の IIS web サイトが表示されます。  
  
10. Internet Explorer のアドレス バーに次のように入力します。 **https://app2/** ENTER キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
11. **開始**画面で「<strong>\\\App2\Files</strong>し、ENTER キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。  
  
12. CLIENT2 で、この手順を繰り返します。  
  
## <a name="IPHTTPS_CLIENT1"></a>IP-HTTPS 接続をテストします。  
  
1. CLIENT1 で開き、管理者特権で Windows PowerShell ウィンドウ、および種類**netsh インターフェイス teredo が無効になっている状態を設定**ENTER キーを押します。 その結果、クライアント コンピューターで Teredo が無効になり、クライアント コンピューターが IP-HTTPS を使用するように構成できます。 コマンドの完了時に、**OK** 応答が表示されます。  
  
2. Windows PowerShell ウィンドウで、入力**ipconfig/all** ENTER キーを押します。  
  
3. ipconfig コマンドの出力を確認します。 このコンピューターは、NAT デバイスの背後からインターネットに接続できるようになり、プライベート IPv4 アドレスが割り当てられます。 Teredo は無効になり、DirectAccess クライアントは IP-HTTPS にフォールバックします。 Ipconfig コマンドの出力を確認するときと 2001:db8:1:1000 または 2001:db8:2:2000 としたプレフィックスに基づく IP-HTTPS アドレスで始まる IP アドレスのトンネル アダプター iphttpsinterface のセクションを参照してください。DirectAccess をセットアップするときに構成されています。 いない IPHTTPSInterface のトンネル アダプターのデフォルト ゲートウェイが表示されます。  
  
4. Windows PowerShell ウィンドウで、入力**ipconfig/flushdns** ENTER キーを押します。 その結果、クライアント コンピューターを社内ネットワークに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。  
  
5. Windows PowerShell ウィンドウで、入力**ping app1** ENTER キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。  
  
6. Windows PowerShell ウィンドウで、入力**ping app2** ENTER キーを押します。 ここでは、fd APP2 EDGE1 から割り当てられた NAT64 アドレスからの応答が表示**c9:9f4e:eb1b**: 7777::a00:4 します。 太字の値がアドレスを生成する方法のために異なることに注意してください。  
  
7. Windows PowerShell ウィンドウで、入力**ping 2 app1** ENTER キーを押します。 2 APP1 2001:db8:2::3 の IPv6 アドレスからの応答が表示されます。  
  
8. Internet Explorer のアドレス バーに Internet Explorer を開き、入力 **https://2-app1/** ENTER キーを押します。 2 APP1 で、既定の IIS web サイトが表示されます。  
  
9. Internet Explorer のアドレス バーに次のように入力します。 **https://app2/** ENTER キーを押します。 APP2 の既定の Web サイトが表示されます。  
  
10. **開始**画面で「<strong>\\\App2\Files</strong>し、ENTER キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。  
  
11. CLIENT2 で、この手順を繰り返します。  
  


