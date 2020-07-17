---
title: 手順1基本的な DirectAccess インフラストラクチャを構成する
description: このトピックは、「Windows Server 2016 用はじめにウィザードを使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: ba4de2a4-f237-4b14-a8a7-0b06bfcd89ad
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 622e8e0f6b4b692cc9bec5bfebeca3336e1e77a1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819525"
---
# <a name="step-1-configure-the-basic-directaccess-infrastructure"></a>手順1基本的な DirectAccess インフラストラクチャを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPv4 と IPv6 の混在環境で単一の DirectAccess サーバーを使用して、基本的な DirectAccess 展開に必要なインフラストラクチャを構成する方法について説明します。 展開の手順を開始する前に、計画で説明した手順を完了していることを確認します [基本的な DirectAccess 展開を計画](../../../remote-access/directaccess/single-server-wizard/Plan-a-Basic-DirectAccess-Deployment.md)します。  
  
|タスク|説明|  
|----|--------|  
|サーバーのネットワーク設定を構成する|DirectAccess サーバーでサーバーのネットワーク設定を構成します。|  
|企業ネットワークでルーティングを構成する|企業ネットワークで、トラフィックが適切にルーティングされるようにルーティングを構成します。|  
|ファイアウォールを構成する|必要に応じて、追加のファイアウォールを構成します。|  
|DNS サーバーを構成する|DirectAccess サーバーの DNS 設定を構成します。|  
|Active Directory を構成する|クライアント コンピューターと DirectAccess サーバーを Active Directory ドメインに追加します。|  
|GPO を構成する|必要に応じて、GPO を展開用に構成します。|  
|セキュリティ グループを構成する|DirectAccess クライアント コンピューターを含むセキュリティ グループと、展開で必要な他の任意のセキュリティ グループを構成します。|  
  
> [!NOTE]  
> このトピックには、説明する手順の一部を自動化するために使用できるサンプルの Windows PowerShell コマンドレットが含まれます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="configure-server-network-settings"></a><a name="ConfigNetworkSettings"></a>サーバーのネットワーク設定を構成する  
IPv4 と IPv6 を使用した環境での単一サーバーの展開には次のネットワーク インフラストラクチャ設定が必要です。 すべての IP アドレスは、Windows の **[ネットワークと共有センター]** の **[アダプターの設定の変更**] を使用して構成されます。  
  
-   エッジ トポロジ  
  
    -   インターネットに接続された 1 つのパブリック静的 IPv4 または IPv6 アドレス。  
  
        > [!NOTE]  
        > Teredo には、連続する 2 つのパブリック IPv4 アドレスが必要です。 Teredo を使用していない場合は、単一の静的パブリック IPv4 アドレスを構成できます。  
  
    -   単一の内部静的 IPv4 または IPv6 アドレス。  
  
-   NAT デバイスの内側 (2 つのネットワーク アダプター)  
  
    -   単一の内部ネットワークに接続された静的 IPv4 または IPv6 アドレス。  
  
    -   境界ネットワークに接続された単一の静的 IPv4 または IPv6 アドレス。  
  
-   NAT デバイスの内側 (1 つのネットワーク アダプター)  
  
    -   単一の静的 IPv4 または IPv6 アドレス。  
  
> [!NOTE]  
> DirectAccess サーバーに 2 つ以上のネットワーク アダプター (一方はドメイン プロファイルに分類され、他方はパブリック/プライベート プロファイルに分類される) がある場合に、単一の NIC トポロジを使用したい場合は、次のことを推奨します。  
>   
> 1.  2 番目の NIC と追加の NIC もドメイン プロファイルに分類されていることを確認します。  
> 2.  何らかの理由で 2 つ目の NIC をドメイン プロファイルに構成できない場合、次の Windows PowerShell コマンドを使用して、手動で DirectAccess IPsec ポリシーのスコープをすべてのプロファイルに設定する必要があります。  
>   
>     ```  
>     $gposession = Open-NetGPO -PolicyStore <Name of the server GPO>  
>     Set-NetIPsecRule -DisplayName <Name of the IPsec policy> -GPOSession $gposession -Profile Any  
>     Save-NetGPO -GPOSession $gposession  
>     ```  
>   
>     IPsec ポリシーの名前は、DirectAccess DaServerToInfra と DirectAccess DaServerToCorp です。  
  
## <a name="configure-routing-in-the-corporate-network"></a><a name="ConfigRouting"></a>企業ネットワークでルーティングを構成する  
次のように、企業ネットワークでルーティングを構成します。  
  
-   組織でネィティブ IPv6 が展開されている場合、内部ネットワーク上のルーターがリモート アクセス サーバー経由で IPv6 トラフィックをルーティングするようにルートを追加します。  
  
-   リモート アクセス サーバー上で組織の IPv4 および IPv6 ルートを手動で構成します。 組織 (/48) の IPv6 プレフィックスが付いたすべてのトラフィックが内部ネットワークに転送されるように、公開されたルートを追加します。 さらに、IPv4 トラフィックの場合、IPv4 トラフィックが内部ネットワークに転送されるように、明示的なルートを追加します。  
  
## <a name="configure-firewalls"></a><a name="ConfigFirewalls"></a>ファイアウォールを構成する  
展開で追加のファイアウォールを使用し、リモート アクセス サーバーが IPv4 インターネット上にある場合は、次のインターネットに接続するファイアウォール例外をリモート アクセス トラフィックに適用します。  
  
-   6to4 トラフィックの IP プロトコル 41 の受信および送信します。  
  
-   IP-HTTPS の伝送制御プロトコル (TCP) 宛先ポート 443 と TCP 発信元ポート 443 が送信されます。 リモート アクセス サーバーに単一のネットワーク アダプターがあり、ネットワーク ロケーション サーバーがリモート アクセス サーバー上にある場合は、TCP ポート 62000 も必要です。  
  
    > [!NOTE]  
    > この除外は、リモート アクセス サーバー上で構成する必要があります。 その他すべての除外はエッジ ファイアウォール上で構成する必要があります。  
  
> [!NOTE]  
> Teredo トラフィックと 6to4 トラフィックの場合、これらの例外は、リモート アクセス サーバー上のインターネットに接続された両方の連続するパブリック IPv4 アドレスに適用する必要があります。 IP-HTTPS の場合、サーバーの外部名が解決されるアドレスに対してのみ例外を適用する必要があります。  
  
追加のファイアウォールを使用し、リモート アクセス サーバーが IPv6 インターネット上にある場合は、次のインターネットに接続するファイアウォール例外をリモート アクセス トラフィックに適用します。  
  
-   IP プロトコル 50  
  
-   UDP 宛先ポート 500 の受信と、UDP 発信元ポート 500 の送信。  
  
追加のファイアウォールを使用する場合は、次の内部ネットワーク ファイアウォール例外をリモート アクセス トラフィックに適用します。  
  
-   ISATAP-プロトコル 41 の受信と送信  
  
-   すべての IPv4/IPv6 トラフィックに対する TCP/UDP  
  
## <a name="configure-the-dns-server"></a><a name="ConfigDNS"></a>DNS サーバーを構成する  
展開内の内部ネットワークのネットワーク ロケーション サーバー Web サイトの DNS エントリを手動で構成する必要があります。  
  
### <a name="to-create-the-network-location-server-and-ncsi-probe-dns-records"></a><a name="NLS_DNS"></a>ネットワークロケーションサーバーと NCSI プローブ DNS レコードを作成するには  
  
1.  内部ネットワークの DNS サーバー上で実行 **dnsmgmt.msc** ENTER キーを押します。  
  
2.  **[DNS マネージャー]** コンソールの左側のウィンドウで、ドメインの前方参照ゾーンを展開します。 ドメインを右クリックし、 **[新しいホスト (A または AAAA)]** をクリックします。  
  
3.  **[新しいホスト]** ダイアログ ボックスで、[**名前 (空欄の場合は親ドメインを使用)]** ボックスに、ネットワーク ロケーション サーバー Web サイトの DNS 名を入力します (これは DirectAccess クライアントがネットワーク ロケーション サーバーに接続するために使用する名前です)。 **[IP アドレス]** ボックスにネットワーク ロケーション サーバーの IPv4 アドレスを入力して、 **[ホストの追加]** をクリックします。 **[DNS]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
4.  **[新しいホスト]** ダイアログ ボックスで、[**名前 (空欄の場合は親ドメインを使用)]** ボックスに、Web プローブの DNS 名を入力します (既定の Web プローブの名前は directaccess-webprobehost です)。 **[IP アドレス]** ボックスに Web プローブの IPv4 アドレスを入力して、 **[ホストの追加]** をクリックします。 directaccess-corpconnectivityhost と手動で作成した接続検証方法について、このプロセスを繰り返します。 **[DNS]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
5.  **[完了]** をクリックします。  
  
windows PowerShell の ![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
```  
Add-DnsServerResourceRecordA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv4Address <network_location_server_IPv4_address>  
Add-DnsServerResourceRecordAAAA -Name <network_location_server_name> -ZoneName <DNS_zone_name> -IPv6Address <network_location_server_IPv6_address>  
```  
  
次の DNS エントリも構成する必要があります。  
  
-   **IP-HTTPS サーバー** - DirectAccess クライアントは、インターネットからリモート アクセス サーバーの DNS 名を解決できる必要があります。  
  
-   **CRL 失効確認** の DirectAccess は DirectAccess クライアントとリモート アクセス サーバー間の IP-HTTPS 接続、DirectAccess クライアントとネットワーク ロケーション サーバー間での HTTPS ベースの接続、証明書の失効確認を使用します。 どちらの場合も、DirectAccess クライアントは、CRL 配布ポイントの場所の解決とアクセスができる必要があります。  
  
## <a name="configure-active-directory"></a><a name="ConfigAD"></a>Active Directory の構成  
リモート アクセス サーバーとすべての DirectAccess クライアント コンピューターは Active Directory ドメインに参加している必要があります。 DirectAccess クライアント コンピューターは、次のいずれかのドメインの種類のメンバーである必要があります。  
  
-   リモート アクセス サーバーと同じフォレストに属するドメイン。  
  
-   リモート アクセス サーバー フォレストと双方向の信頼を持つフォレストに属するドメイン。  
  
-   リモート アクセス サーバー ドメインへの双方向の信頼を持つドメイン。  
  
#### <a name="to-join-the-remote-access-server-to-a-domain"></a>リモート アクセス サーバーをドメインに追加するには  
  
1.  サーバー マネージャーで **[ローカル サーバー]** をクリックします。 詳細ウィンドウで、 **[コンピューター名]** の横にあるリンクをクリックします。  
  
2.  **[システムのプロパティ]** ダイアログボックスで、 **[コンピューター名]** タブをクリックします。 **[コンピューター名]** タブで、 **[変更]** をクリックします。  
  
3.  サーバーをドメインに追加するときにコンピューター名も変更する場合は、 **[コンピューター名]** にコンピューター名を入力します。 **[次のメンバー]** で **[ドメイン]** をクリックし、サーバーの追加先のドメイン名 (corp.contoso.com など) 入力し、 **[OK]** をクリックします。  
  
4.  ユーザー名とパスワードを求めるメッセージが表示されたら、ドメインにコンピューターを追加する権限を持つユーザーのユーザー名とパスワードを入力し、 **[OK]** をクリックします。  
  
5.  ドメインへの参加を知らせるダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
6.  コンピューターを再起動するよう求めるメッセージが表示されたら、 **[OK]** をクリックします。  
  
7.  **[システムのプロパティ]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
8.  コンピューターを再起動するよう求めるメッセージが表示されたら、 **[今すぐ再起動する]** をクリックします。  
  
#### <a name="to-join-client-computers-to-the-domain"></a>クライアント コンピューターをドメインに参加させるには  
  
1.  実行 **explorer.exe**します。  
  
2.  コンピューター アイコンを右クリックし、**プロパティ** をクリックします。  
  
3.  **[システム]** ページで、 **[システムの詳細設定]** をクリックします。  
  
4.  **[システムのプロパティ]** ダイアログ ボックスの **[コンピューター名]** タブで **[変更]** をクリックします。  
  
5.  サーバーをドメインに追加するときにコンピューター名も変更する場合は、 **[コンピューター名]** にコンピューター名を入力します。 **[次のメンバー]** で **[ドメイン]** をクリックし、サーバーの追加先のドメイン名 (corp.contoso.com など) 入力し、 **[OK]** をクリックします。  
  
6.  ユーザー名とパスワードを求めるメッセージが表示されたら、ドメインにコンピューターを追加する権限を持つユーザーのユーザー名とパスワードを入力し、 **[OK]** をクリックします。  
  
7.  ドメインへの参加を知らせるダイアログ ボックスが表示されたら、 **[OK]** をクリックします。  
  
8.  コンピューターを再起動するよう求めるメッセージが表示されたら、 **[OK]** をクリックします。  
  
9. **システムのプロパティ** ダイアログ ボックスで、閉じる をクリックします。 指示に従い、 **[今すぐ再起動する]** をクリックします。  
  
windows PowerShell の ![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
以下の Add-Computer コマンドを入力した後に、ドメイン資格情報を指定する必要があります。  
  
```  
Add-Computer -DomainName <domain_name>  
Restart-Computer  
```  
  
## <a name="configure-gpos"></a><a name="ConfigGPOs"></a>Gpo を構成する  
リモート アクセスを展開する 2 つのグループ ポリシー オブジェクトの最小値を必要とします。 1 つのグループ ポリシー オブジェクトは、リモート アクセス サーバーの設定を格納し、DirectAccess クライアント コンピューターの設定が含まれています。 リモート アクセスを構成するときに、ウィザードは自動的に必要なグループ ポリシー オブジェクトを作成します。 ただし、名前付け規則を実施する組織、またはグループ ポリシー オブジェクトを作成または更新に必要なアクセス許可がないは、リモート アクセスを構成する前に、作成する必要があります。  
  
グループ ポリシー オブジェクトを作成するを参照してください。 [を作成し、グループ ポリシー オブジェクトを編集](https://technet.microsoft.com/library/cc754740.aspx)します。  
  
> [!IMPORTANT]  
> 管理者は、次の手順を使用して組織単位に、DirectAccess グループ ポリシー オブジェクトを手動でリンクできます。  
>   
> 1.  DirectAccess を構成する前に、作成した GPO を各組織単位にリンクします。  
> 2.  DirectAccess を構成し、クライアント コンピューターのセキュリティ グループを指定します。  
> 3.  管理者はグループ ポリシー オブジェクトをドメインにリンクするアクセス許可を持っている場合と持っていない場合があります。 どちらの場合も、グループ ポリシー オブジェクトは自動的に構成されます。 GPO が既に OU にリンクされている場合、リンクは削除されません。 また、GPO もドメインにリンクされません。 サーバー GPO の場合、OU にサーバー コンピューター オブジェクトが含まれているか、GPO がドメインのルートにリンクされている必要があります。  
> 4.  DirectAccess ウィザードの実行前に OU へのリンクが行われていない場合、構成の完了後に、管理者は DirectAccess グループ ポリシー オブジェクトを必要な組織単位にリンクできます。 ドメインへのリンクは削除できます。 手順は、グループ ポリシー オブジェクトを組織単位にリンク [ここで](https://technet.microsoft.com/library/cc732979.aspx)  
  
> [!NOTE]  
> グループ ポリシー オブジェクトは、手動で作成されている場合ことは、グループ ポリシー オブジェクトが使用できないこと、DirectAccess 構成中に。 グループ ポリシー オブジェクトは、管理コンピューターに最も近いドメイン コント ローラーにレプリケートするされていない可能性があります。 この場合、管理者はレプリケーションが完了するまで待つか、レプリケーションを強制的に実行できます。

> [!Warning]
> Directaccess セットアップウィザード以外の任意の方法を使用して directaccess を構成する (DirectAccess グループポリシーオブジェクトを直接変更する、サーバーまたはクライアントの既定のポリシー設定を手動で変更するなど) ことはサポートされていません。
  
## <a name="configure-security-groups"></a><a name="ConfigSGs"></a>セキュリティグループの構成  
クライアント コンピューターのグループ ポリシー オブジェクトに含まれる DirectAccess 設定は、リモート アクセスを構成するときに指定したセキュリティ グループのメンバーであるコンピューターにのみ適用されます。  
  
### <a name="to-create-a-security-group-for-directaccess-clients"></a><a name="Sec_Group"></a>DirectAccess クライアントのセキュリティグループを作成するには  
  
1.  実行 **dsa.msc**します。 **[Active Directory ユーザーとコンピューター]** コンソールの左側のウィンドウで、セキュリティ グループを含むドメインを展開し、 **[Users]** を右クリックし、 **[新規作成]** をクリックして、 **[グループ]** をクリックします。  
  
2.  **[新しいオブジェクト - グループ]** ダイアログ ボックスで、 **[グループ名]** の下にセキュリティ グループの名前を入力します。  
  
3.  **[グループのスコープ]** の下で **[グローバル]** をクリックし、 **[グループの種類]** の下で **[セキュリティ]** をクリックし、 **[OK]** をクリックします。  
  
4.  DirectAccess クライアント コンピューター セキュリティ グループをダブルクリックし、プロパティー ダイアログ ボックスで、 **[メンバー]** タブをクリックします。  
  
5.  **[メンバー]** タブで **[追加]** をクリックします。  
  
6.  **[ユーザー、連絡先、コンピューター、サービス アカウントまたはグループの選択]** ダイアログ ボックスで、DirectAccess 用に有効にするクライアント コンピューターを選択し、 **[OK]** をクリックします。  
  
windows PowerShell の ![](../../../media/Step-1-Configure-the-DirectAccess-Infrastructure/PowerShellLogoSmall.gif)**Windows powershell の同等のコマンド**  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
```  
New-ADGroup -GroupScope global -Name <DirectAccess_clients_group_name>  
Add-ADGroupMember -Identity DirectAccess_clients_group_name -Members <computer_name>  
```  
  
## <a name="next-step"></a><a name="BKMK_Links"></a>次のステップ  
  
-   [手順 2: 基本的な DirectAccess サーバーを構成する](da-basic-configure-s2-server.md)  
  


