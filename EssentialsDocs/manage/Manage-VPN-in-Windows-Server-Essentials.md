---
title: "Windows Server Essentials での VPN を管理します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 08a08a13d696371420bdfdf89f54320c787636b0
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Windows Server Essentials での VPN を管理します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象: 
  
 仮想プライベート ネットワーク (VPN) 接続では、インターネットなどのパブリック ネットワークによって提供されるインフラストラクチャを使用して、プライベート ネットワーク上のサーバーにアクセスするは、自宅や外出先で作業しているユーザーが有効にします。 使用するには VPN サーバーのリソースにアクセスするためには、次の操作を行う必要があります。  
  
-   [リモート アクセス サーバーでの VPN を有効にします。](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [ネットワーク ユーザーに対する VPN アクセス許可を設定します。](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [クライアント コンピューターをサーバーに接続します。](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [VPN を使用して、Windows Server Essentials に接続するには](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="BKMK_1"></a>リモート アクセス サーバーでの VPN を有効にします。  
 リモート アクセスを有効にする Windows Server Essentials で VPN を構成するのには、次の手順を実行します。  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Windows Server Essentials で VPN を有効にするには  
  
1.  ダッシュ ボードを開きます。  
  
2.  をクリックして**設定**、クリックして、**Anywhere Access** ] タブ。  
  
3.  をクリックして**構成**します。 セットアップ Anywhere Access ウィザードが表示されます。  
  
4.  **Anywhere Access 機能の選択を有効にする**] ページで、[、**仮想プライベート ネットワーク**チェック ボックスをオンします。  
  
5.  ウィザードを完了するための手順に従います。  
  
##  <a name="BKMK_2"></a>ネットワーク ユーザーに対する VPN アクセス許可を設定します。  
 VPN を使用して、Windows Server Essentials に接続し、サーバーに保存されているすべてのリソースにアクセスすることができます。 これは、VPN 接続経由でホスト型 Windows Server Essentials サーバーに接続するために使用するネットワーク アカウントで設定されているクライアント コンピューターがある場合に特に便利です。 ホスト型 Windows Server Essentials サーバー上のすべての新しく作成されたユーザー アカウントは、最初に、クライアント コンピューターにログオンする VPN を使用する必要があります。  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>ネットワーク ユーザーに対する VPN アクセス許可を設定するには  
  
1.  ダッシュ ボードを開きます。  
  
2.  ナビゲーション バーをクリックして**ユーザー**します。  
  
3.  ユーザー アカウントの一覧では、デスクトップにリモートでアクセスするアクセス許可を付与するユーザー アカウントを選択します。  
  
4.  **< ユーザー Account\ > タスク**] ウィンドウで、をクリックして**プロパティ**します。  
  
5.  **< ユーザー Account\ > プロパティ**、] をクリックして、**Anywhere Access** ] タブ。  
  
6.  **Anywhere Access** ] タブで、VPN を使用して、サーバーに接続するユーザーを許可するように、選択、**許可仮想プライベート ネットワーク (VPN)**チェック ボックスをオンします。  
  
7.  をクリックして**適用**、] をクリックし、**OK**します。  
  
##  <a name="BKMK_Connect"></a>クライアント コンピューターをサーバーに接続します。  
 リモート アクセス用の Windows Server Essentials を実行しているサーバー上で有効にすると、VPN に接続し、サーバーに保存されているすべてのリソースにアクセス、VPN 接続を使用することができます。 ただし、コンピューターをサーバーに初めて接続する必要があります。 サーバー ウィザードへの接続 [マイ コンピューターを使用してコンピューターをサーバーに接続するときに VPN ネットワーク接続がクライアント コンピューターで自動的に生成し、自宅や外出先で作業中にサーバー リソースにアクセスするために使用することができます。 コンピューターをサーバーに接続する方法の詳細な手順については、次を参照してください。[コンピューター、サーバーに接続](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  
  
##  <a name="BKMK_3"></a>VPN を使用して、Windows Server Essentials に接続するには  
 すべての新しく作成されたユーザー アカウント、VPN 接続経由 Windows Server Essentials を実行しているホスト サーバーへの接続に使用できるネットワーク アカウントで設定されているクライアント コンピューターがある場合、ホストされているサーバーは、最初に、クライアント コンピューターにログオンする VPN を使用する必要があります。 サーバーに接続されているクライアント コンピューターから、次の手順を完了します。  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>サーバーのリソースにリモート アクセスに VPN を使用するには  
  
1.  キーを押して Ctrl + Alt +、クライアント コンピューターで削除します。  
  
2.  をクリックして**ユーザーの切り替え**ログオン画面でします。  
  
3.  画面の右下隅にあるネットワーク ログオン アイコンをクリックします。  
  
4.  ネットワーク ユーザー名とパスワードを使用して、Windows Server Essentials ネットワークにログオンします。  
  
## <a name="see-also"></a>参照してください。  
  
-   [リモート操作します。](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Anywhere Access を管理します。](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)
