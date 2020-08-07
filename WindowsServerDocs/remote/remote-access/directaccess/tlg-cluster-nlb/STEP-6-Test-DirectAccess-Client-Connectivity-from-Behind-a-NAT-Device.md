---
title: 手順 6 NAT デバイスの背後からの DirectAccess クライアント接続のテスト
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: aded2881-99ed-4f18-868b-b765ab926597
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2ff8b054aef6755b4c98c423471c22fe45aa1866
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951137"
---
# <a name="step-6-test-directaccess-client-connectivity-from-behind-a-nat-device"></a>手順 6 NAT デバイスの背後からの DirectAccess クライアント接続のテスト

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DirectAccess クライアントを NAT デバイスまたは Web プロキシ サーバーの背後からインターネットに接続すると、DirectAccess クライアントでは、リモート アクセス サーバーへの接続に Teredo または IP-HTTPS が使用されます。

NAT デバイスが、リモートアクセスサーバーのパブリック IP アドレスへの発信 UDP ポート3544を有効にすると、Teredo が使用されます。 Teredo を使用できない場合、DirectAccess クライアントは、発信 TCP ポート 443 の IP-HTTPS にフォールバックされます。その結果、従来の SSL ポートで、ファイアウォールまたは Web プロキシ サーバーを経由してアクセスできるようになります。

Web プロキシに認証が必要な場合、IP-HTTPS 接続は失敗します。 また、Web プロキシが発信 SSL 検査を実行している場合も IP-HTTPS 接続は失敗します。これは、HTTPS セッションがリモート アクセス サーバーではなく Web プロキシで中断されるためです。 ここでは、前のセクションの 6to4 接続を使用して接続するときと同じテストを実行します。

両方のクライアント コンピューターで次の手順を実行します。

1. Teredo 接続をテストします。 最初のテストセットは、DirectAccess クライアントが Teredo を使用するように構成されている場合に実行されます。 これは、NAT デバイスで UDP ポート 3544 への発信アクセスを許可する場合の自動設定です。

2. Ip-https 接続をテストします。 2番目のテストセットは、IP-HTTPS を使用するように DirectAccess クライアントが構成されている場合に実行されます。 IP-HTTPS 接続を実行するために、クライアント コンピューターの Teredo を無効にします。

> [!TIP]
> これらの手順を実行する前に Internet Explorer のキャッシュをクリアして、接続をテストし、キャッシュから web サイトページを取得しないようにすることをお勧めします。

## <a name="prerequisites"></a>前提条件

これらのテストを実行する前に、インターネット スイッチから CLIENT1 の接続を外し、ホームネット スイッチに接続します。 現在のネットワークを定義するネットワークの種類を尋ねられたら、[**ホーム ネットワーク**] を選択します。

EDGE1 と EDGE2 がまだ実行されていない場合は、起動します。

## <a name="test-teredo-connectivity"></a>Teredo 接続のテスト

1. CLIENT1 で、管理者特権の Windows PowerShell ウィンドウを開き、「 **ipconfig/all** 」と入力して、enter キーを押します。

2. ipconfig コマンドの出力を確認します。

   CLIENT1 は、NAT デバイスの背後からインターネットに接続されるようになり、プライベート IPv4 アドレスが割り当てられます。 DirectAccess クライアントが NAT デバイスの背後にあり、プライベート IPv4 アドレスが割り当てられている場合、推奨される IPv6 移行テクノロジは Teredo です。 ipconfig コマンドの出力を確認すると、Tunnel adapter Teredo Tunneling Pseudo-Interface というセクション、次に Microsoft Teredo Tunneling Adapter という説明、および Teredo アドレスと一致する 2001: から始まる IP アドレスがあります。 Teredo セクションが表示されない場合、次の **netsh interface Teredo set state enterpriseclient** コマンドを使用して Teredo を有効にし、ipconfig コマンドを再実行します。 Teredo トンネル アダプター用に登録されている既定のゲートウェイは表示されません。

3. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。

   その結果、クライアント コンピューターをインターネットに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。

4. Windows PowerShell ウィンドウで、「 **get-dnsclientnrptpolicy** 」と入力し、enter キーを押します。

   出力には、名前解決ポリシー テーブル (NRPT) の現在の設定が表示されます。 これらの設定は、2001:db8:1::2 という IPv6 アドレスを使用して、.corp.contoso.com へのすべての接続はリモート アクセス DNS サーバーで解決する必要があることを示します。 また、nls.corp.contoso.com という名前が除外されることを示す NRPT エントリがあります。除外リストの名前は、リモート アクセス DNS サーバーから応答されません。 リモート アクセス DNS サーバーの IP アドレスに ping を送信して、リモート アクセス サーバーへの接続を確認することができます。この例では、2001:db8:1::2 に ping を送信できます。

5. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。

6. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 から割り当てられた NAT64 アドレスから APP2 (この例では fdc9:9f4e:eb1b:7777::a00:4) に返信があります。

7. 次の手順については、Windows PowerShell ウィンドウを開いたままにしておきます。

8. Internet explorer を開き、Internet Explorer のアドレスバーに「」と入力し、enter **https://app1/** キーを押します。 APP1 の既定の IIS Web サイトが表示されます。

9. Internet Explorer のアドレスバーに「」と入力し、enter **https://app2/** キーを押します。 APP2 の既定の Web サイトが表示されます。

10. **スタート**画面で「<strong> \\ \App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。

## <a name="test-ip-https-connectivity"></a>IP-HTTPS 接続のテスト

1. 管理者特権の Windows PowerShell ウィンドウを開き、「 **netsh interface teredo set state disabled** 」と入力し、enter キーを押します。 その結果、クライアント コンピューターで Teredo が無効になり、クライアント コンピューターが IP-HTTPS を使用するように構成できます。 コマンドの完了時に、**OK** 応答が表示されます。

2. Windows PowerShell ウィンドウで、「 **ipconfig/all** 」と入力し、enter キーを押します。

3. ipconfig コマンドの出力を確認します。 このコンピューターは、NAT デバイスの背後からインターネットに接続できるようになり、プライベート IPv4 アドレスが割り当てられます。 Teredo は無効になり、DirectAccess クライアントは IP-HTTPS にフォールバックします。 ipconfig コマンドの出力を確認すると、Tunnel adapter iphttpsinterface というセクションと、DirectAccess の設定時に構成したプレフィックスに基づく IP-HTTPS アドレスと一致する 2001:db8:1:100 から始まる IP アドレスが表示されます。 IP-HTTPS トンネル アダプター用に登録されている既定のゲートウェイは表示されません。

4. Windows PowerShell ウィンドウで、「 **ipconfig/flushdns** 」と入力し、enter キーを押します。 その結果、クライアント コンピューターを社内ネットワークに接続すると、まだクライアント DNS キャッシュに残っている名前解決エントリは消去されます。

5. Windows PowerShell ウィンドウで、「 **ping** 」と入力し、enter キーを押します。 APP1 の IPv6 アドレス 2001:db8:1::3 から返信があります。

6. Windows PowerShell ウィンドウで、「 **ping app2** 」と入力し、enter キーを押します。 EDGE1 から割り当てられた NAT64 アドレスから APP2 (この例では fdc9:9f4e:eb1b:7777::a00:4) に返信があります。

7. Internet explorer を開き、Internet Explorer のアドレスバーに「」と入力し、enter **https://app1/** キーを押します。 APP1 の既定の IIS サイトが表示されます。

8. Internet Explorer のアドレスバーに「」と入力し、enter **https://app2/** キーを押します。 APP2 の既定の Web サイトが表示されます。

9. **スタート**画面で「<strong> \\ \App2\Files</strong>」と入力し、enter キーを押します。 [新しいテキスト ドキュメント] ファイルをダブルクリックします。 これは、SMB を使用して IPv4 のみのサーバーに接続し、IPv4 のみのホストのリソースを取得できたことを示します。
