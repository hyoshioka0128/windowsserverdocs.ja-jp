---
title: Windows Server Essentials での VPN の管理
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bb221a0ef80388fa8b5bffbc38f7cbec56d3f61c
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180868"
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Windows Server Essentials での VPN の管理

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

 仮想プライベート ネットワーク (VPN) 接続を使用すると、自宅や外出先で作業をするユーザーが、インターネットなどのパブリック ネットワークによって提供されるインフラストラクチャを使用して、プライベート ネットワーク上のサーバーにアクセスできるようになります。 サーバー リソースへのアクセスに VPN を使用するには、次の手順を完了します。

-   [サーバーでリモート アクセス用の VPN を有効にする](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)

-   [ネットワーク ユーザーに対する VPN アクセス許可を設定する](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)

-   [クライアント コンピューターをサーバーに接続する](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)

-   [VPN を利用した Windows Server Essentials への接続](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)

##  <a name="enable-vpn-for-remote-access-on-the-server"></a><a name="BKMK_1"></a>サーバーでリモートアクセス用の VPN を有効にする
 次の手順を実行して、Windows Server Essentials でリモート アクセスが有効になるように VPN を構成します。

#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Windows Server Essentials で VPN を有効にするには

1.  ダッシュボードを開きます。

2.  **[設定]** をクリックし、**[Anywhere Access]** タブをクリックします。

3.  **[Configure]\(構成\)** をクリックします。 Anywhere Access のセットアップ ウィザードが表示されます。

4.  **[有効にする Anywhere Access の機能を選択します]** ページで、**[仮想プライベート ネットワーク]** チェック ボックスをオンにします。

5.  指示に従ってウィザードを完了します。

##  <a name="set-vpn-permissions-for-network-users"></a><a name="BKMK_2"></a>ネットワークユーザーの VPN アクセス許可を設定する
 VPN を使用すると、Windows Server Essentials に接続し、サーバーに保存されているすべてのリソースにアクセスすることができます。 これが特に役立つのは、クライアント コンピューターに設定されているネットワーク アカウントを使用して、ホストされている Windows Server Essentials サーバーに VPN 経由で接続できる場合です。 ホストされている Windows Server Essentials サーバーで新しく作成されたユーザー アカウントはすべて、クライアント コンピューターへの初回ログオン時に VPN を使用する必要があります。

#### <a name="to-set-vpn-permissions-for-network-users"></a>ネットワーク ユーザーに対する VPN アクセス許可を設定するには

1.  ダッシュボードを開きます。

2.  ナビゲーション バーで **[ユーザー]** をクリックします。

3.  ユーザー アカウントの一覧から、リモートでデスクトップにアクセスするアクセス許可を付与するユーザー アカウントを選択します。

4.  [**ユーザーアカウント \> タスクの<** ] ウィンドウで、[**プロパティ**] をクリックします。

5.  **<ユーザーアカウントの \> プロパティ**で、[ **Anywhere Access** ] タブをクリックします。

6.  VPN を使用してユーザーがサーバーに接続できるようにするには、 **[Anywhere Access]** タブで、 **[仮想プライベート ネットワーク (VPN) を許可する]**  チェック ボックスをオンにします。

7.  [**適用**] をクリックし、[**OK**] をクリックします。

##  <a name="connect-client-computers-to-the-server"></a><a name="BKMK_Connect"></a>クライアントコンピューターをサーバーに接続する
 Windows Server Essentials を実行しているサーバーでリモート アクセス用の VPN が有効になったら、VPN 接続を使用して、サーバーに保存されているすべてのリソースに接続してアクセスできます。 ただし、まずコンピューターをサーバーに接続する必要があります。 [サーバーにコンピューターを接続] ウィザードを使用してコンピューターをサーバーに接続すると、クライアント コンピューターで VPN ネットワーク接続が自動的に生成されます。この接続を使用して、自宅や外出先での作業中にサーバー リソースにアクセスできます。 コンピューターをサーバーに接続するための詳細な手順については、「 [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。

##  <a name="use-vpn-to-connect-to-windows-server-essentials"></a><a name="BKMK_3"></a>VPN を使用して Windows Server Essentials に接続する
 Windows Server Essentials を実行しているホステッド サーバーに VPN 接続経由で接続するときに使用できるネットワーク アカウントでクライアント コンピューターを設定している場合、そのホステッド サーバーで新しく作成されたユーザー アカウントはすべて、初めてクライアント コンピューターにログオンするとき、VPN を使用する必要があります。 サーバーに接続されているクライアント コンピューターで、次の手順を完了します。

#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>VPN を利用して離れた場所からサーバー リソースにアクセスするには

1.  クライアント コンピューターで Ctrl + Alt + Del キーを押します。

2.  ログオン画面で **[ユーザーの切り替え]** をクリックします。

3.  画面右下隅にあるネットワーク ログオン アイコンをクリックします。

4.  ネットワーク ユーザー名とパスワードを利用し、Windows Server Essentials ネットワークにログオンします。

## <a name="additional-references"></a>その他のリファレンス

-   [リモートで作業する](../use/Work-Remotely-in-Windows-Server-Essentials.md)

-   [Anywhere Access の管理](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
