---
title: 手順 2 のインストールと構成 ROUTER1
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc20b1a0-540d-4531-a176-50b87c071600
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6a771b5eb8587d23bc67a7e7769264251afdb5bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838513"
---
# <a name="step-2-install-and-configure-router1"></a>手順 2 のインストールと構成 ROUTER1

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このマルチサイトのテスト ラボ ガイドでルーター コンピューターは、企業ネットワークと 2 Corpnet サブネット間で、IPv4 と IPv6 のブリッジを提供し、IP-HTTPS および Teredo トラフィックのルーターとして機能します。  
  
- ROUTER1 のオペレーティング システムをインストールします。 
  
- TCP/IP のプロパティを構成して、コンピューターの名前  
  
- ファイアウォールを無効にします。
  
- ルーティングおよび転送を構成します。
  
## <a name="install-the-operating-system-on-router1"></a>ROUTER1 のオペレーティング システムをインストールします。  
最初に、Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 をインストールします。  
  
### <a name="to-install-the-operating-system-on-router1"></a>ROUTER1 にオペレーティング システムをインストールするには  
  
1.  Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 (完全インストール) のインストールを開始します。  
  
2.  手順に従ってインストールを完了し、ローカルの Administrator アカウントの強力なパスワードを指定します。 ローカルの Administrator アカウントを使用してログオンします。  
  
3.  ROUTER1 をインターネットにアクセスできるネットワークに接続し、Windows Update の Windows Server 2016、Windows Server 2012 R2 または Windows Server 2012 では、最新の更新プログラムをインストールし、インターネットから切断を実行します。  
  
4.  ROUTER1 を企業ネットワークと 2 Corpnet サブネットに接続します。  
  
## <a name="configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP のプロパティを構成して、コンピューターの名前  
ルーターの TCP/IP 設定を構成し、ROUTER1 に、コンピューターの名前を変更します。  
  
### <a name="to-configure-tcpip-properties-and-rename-the-computer"></a>TCP/IP のプロパティを構成して、コンピューターの名前を変更するには  
  
1.  サーバー マネージャー コンソールで、次のようにクリックします。**ローカル サーバー**、し、**プロパティ**エリア、次へ を**ワイヤード (イーサネット) 接続**、リンクをクリックします。  
  
2.  **ネットワーク接続**ウィンドウで、企業ネットワークに接続されているネットワーク アダプターを右クリックし、をクリックして**の名前を変更**、型**Corpnet**、ENTER キーを押します。  
  
3.  右クリック**Corpnet**、 をクリックし、**プロパティ**します。  
  
4.  **[インターネット プロトコル バージョン 4 (TCP/IPv4)]** をクリックし、**[プロパティ]** をクリックします。  
  
5.  **[次の IP アドレスを使う]** をクリックします。 **IP アドレス**、型**10.0.0.254**します。 **サブネット マスク**、型**255.255.255.0**、 をクリックし、 **OK**。  
  
6.  **[インターネット プロトコル バージョン 6 (TCP/IPv6)]** をクリックし、 **[プロパティ]** をクリックします。  
  
7.  クリックして**次の IPv6 アドレスを使用して、** します。 **IPv6 アドレス**、型**2001:db8:1::fe**します。 **サブネット プレフィックス長**、型**64**、順にクリックします**OK**します。  
  
8.  **Corpnet プロパティ** ダイアログ ボックスをクリックして**閉じる**します。  
  
9. **ネットワーク接続**ウィンドウで、2-企業ネットワークに接続されているネットワーク アダプターを右クリックし、をクリックして**の名前を変更**、型**2 Corpnet**、ENTER キーを押します。  
  
10. 右クリック**2 Corpnet**、 をクリックし、**プロパティ**します。  
  
11. **[インターネット プロトコル バージョン 4 (TCP/IPv4)]** をクリックし、**[プロパティ]** をクリックします。  
  
12. **[次の IP アドレスを使う]** をクリックします。 **IP アドレス**、型**10.2.0.254**します。 **サブネット マスク**、型**255.255.255.0**、 をクリックし、 **OK**。  
  
13. **[インターネット プロトコル バージョン 6 (TCP/IPv6)]** をクリックし、 **[プロパティ]** をクリックします。  
  
14. クリックして**次の IPv6 アドレスを使用して、** します。 **IPv6 アドレス**、型**2001:db8:2::fe**します。 **サブネット プレフィックス長**、型**64**、順にクリックします**OK**します。  
  
15. **2 Corpnet プロパティ** ダイアログ ボックスをクリックして**閉じる**します。  
  
16. **[ネットワーク接続]** ウィンドウを閉じます。  
  
17. サーバー マネージャー コンソールで**ローカル サーバー**の**プロパティ**エリア、次へ を**コンピューター名**リンクをクリックします。  
  
18. **[システムのプロパティ]** ダイアログ ボックスの **[コンピューター名]** タブで **[変更]** をクリックします。  
  
19. **コンピューター名/ドメイン名の変更** ダイアログ ボックスで**コンピューター名**、型**ROUTER1**、順にクリックします**OK**します。  
  
20. コンピューターを再起動するよう求めるメッセージが表示されたら、**[OK]** をクリックします。  
  
21. **[システムのプロパティ]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
22. コンピューターを再起動するよう求めるメッセージが表示されたら、 **[今すぐ再起動する]** をクリックします。  
  
23. コンピューターが再起動したら、ローカルの Administrator アカウントでログオンします。  
  
## <a name="turn-off-the-firewall"></a>ファイアウォールを無効にします。  
このコンピューターが、企業ネットワークと 2 Corpnet サブネット間のルーティングを提供することのみ構成されています。そのため、ファイアウォールをオフにする必要があります。  
  
### <a name="to-turn-off-the-firewall"></a>ファイアウォールを無効にするには  
  
1.  **開始**画面で「**wf.msc**、し、ENTER キーを押します。  
  
2.  セキュリティが強化された Windows ファイアウォールでの**アクション**ウィンドウで、をクリックして**プロパティ**。  
  
3.  **セキュリティが強化された Windows ファイアウォール** ダイアログ ボックスで、**ドメイン プロファイル** タブの **ファイアウォールの状態**、 をクリックして**オフ**します。  
  
4.  **セキュリティが強化された Windows ファイアウォール** ダイアログ ボックスで、**プライベート プロファイル** タブの **ファイアウォールの状態**、 をクリックして**オフ**します。  
  
5.  **セキュリティが強化された Windows ファイアウォール** ダイアログ ボックスで、**パブリック プロファイル** タブの **ファイアウォールの状態**、 をクリックして**オフ**、し、クリックして**OK**します。  
  
6.  セキュリティが強化された Windows ファイアウォールを閉じます。  
  
## <a name="configure-routing-and-forwarding"></a>ルーティングおよび転送を構成します。  
ルーティングおよび転送 Corpnet」および「2 Corpnet サブネットの間でサービスを提供するには、ネットワーク インターフェイスで転送有効にしをサブネット間の静的ルートを構成する必要があります。  
  
### <a name="to-configure-static-routes"></a>静的ルートを構成するには  
  
1.  **開始**画面で「**cmd.exe**、し、ENTER キーを押します。  
  
2.  次のコマンドを使用して両方のネットワーク アダプターの IPv4 と IPv6 の両方のインターフェイスでの転送を有効にします。 各コマンドを入力した後 ENTER キーを押します。  
  
    ```  
    netsh interface IPv4 set interface Corpnet forwarding=enabled  
    netsh interface IPv4 set interface 2-Corpnet forwarding=enabled  
    netsh interface IPv6 set interface Corpnet forwarding=enabled  
    netsh interface IPv6 set interface 2-Corpnet forwarding=enabled  
    ```  
  
3.  IP-HTTPS は、企業ネットワークと 2 Corpnet サブネット間でルーティングを有効にします。  
  
    ```  
    netsh interface IPv6 add route 2001:db8:1:1000::/59 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:db8:2:2000::/59 2-Corpnet 2001:db8:2::20  
    ```  
  
4.  Teredo は、企業ネットワークと 2 Corpnet サブネット間でルーティングを有効にします。  
  
    ```  
    netsh interface IPv6 add route 2001:0:836b:2::/64 Corpnet 2001:db8:1::2  
    netsh interface IPv6 add route 2001:0:836b:14::/64 2-Corpnet 2001:db8:2::20  
    ```  
  
5.  コマンド プロンプト ウィンドウを閉じます。
