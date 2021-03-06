---
title: 手順 2 は、クラスター サーバーを準備します。
description: このトピックでは、Windows Server 2016 でのクラスターでのリモート アクセスの展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d68abb-6914-42e0-91e8-803933cf785e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 10a40b30acbf022ed34f454d753884cb8c5c97d4
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281207"
---
# <a name="step-2-prepare-cluster-servers"></a>手順 2 は、クラスター サーバーを準備します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

クラスターの展開を構成する前に、クラスターに追加するその他のサーバーを準備します。  
  
|タスク|説明|  
|----|--------|  
|[2.1 は、リモート アクセス インフラストラクチャを構成します。](#BKMK_config)|クラスターに追加する各サーバーで、サーバーのトポロジ、IP アドレスの指定、ルーティング、および転送を構成します。 仮想マシンの負荷分散されたクラスターを構成する場合は、MAC アドレスのスプーフィングを使用する仮想マシンを構成する必要があります。<br /><br />さらに、各サーバーを同じドメインに参加し、すべてのサーバーを同じサブネットに接続します。|  
|[2.2、リモート アクセスの役割をインストールします。](#BKMK_Install)|クラスターに追加する各追加サーバー リモート アクセスの役割をインストールします。|  
|[2.3 NLB をインストールします。](#BKMK_NLB)|デプロイされているリモート アクセス サーバーおよびクラスターに追加する各追加のサーバーでは、NLB 機能をインストールします。 外部のロード バランサーを使用する場合に、この手順は必要ないことに注意してください。|  
  
## <a name="BKMK_config"></a>2.1 は、リモート アクセス インフラストラクチャを構成します。  
リモート アクセス クラスターを構成するのには、サーバーのトポロジ、IP アドレスの指定、ルーティング、および転送を構成する必要があります、クラスターの一部を形成するすべてのサーバーにします。  
  
### <a name="to-configure-the-remote-access-infrastructure"></a>リモート アクセス インフラストラクチャを構成するには  
  
1.  それぞれの最初のリモート アクセス サーバーとして同じトポロジを使用したクラスターを構成するサーバーを構成します。  
  
2.  それぞれの適切な IP アドレス指定、ルーティング、および転送先の最初のリモート アクセス サーバーの構成に基づいたを持つクラスターに含まれるサーバーを構成します。 クラスター内のすべてのサーバーを同じサブネットに接続する必要があることに注意してください。  
  
3.  それぞれの最初のリモート アクセス サーバーと同じドメインにクラスターを構成するサーバーを参加させます。  
  
## <a name="BKMK_Install"></a>2.2、リモート アクセスの役割をインストールします。  
リモート アクセス クラスターを構成するのには、クラスターの一部を形成するすべてのサーバーにリモート アクセスの役割をインストールする必要があります。  
  
### <a name="to-install-the-remote-access-role-on-always-on-vpn-servers"></a>Always On VPN サーバーにリモート アクセスの役割をインストールするには  
  
1.  サーバー マネージャー コンソールで、DirectAccess サーバー上で、 **ダッシュ ボード**, 、 をクリックして **役割と機能の追加**します。  
  
2.  **[次へ]** を 3 回クリックして、サーバーの役割を選択する画面に移動します。  
  
3.  **サーバーの役割の選択**ダイアログ ボックスで選択**リモート アクセス**、順にクリックします**次**します。  
  
4.  クリックして**次**3 回です。  
  
5.  **役割サービスの選択**ダイアログ ボックスで選択**DirectAccess と VPN (RAS)**  をクリックし、**機能の追加**します。  
  
6.  選択**ルーティング**を選択します**Web アプリケーション プロキシ**、 をクリックして**機能の追加**、順にクリックします**次**します。  
  
7. **[次へ]** をクリックし、 **[インストール]** をクリックします。  
  
8.  **[インストールの進行状況]** ダイアログで、インストールが正常に完了したことを確認し、 **[閉じる]** をクリックします。  
  
9.  すべてのサーバー クラスターのメンバーにするには、この手順を繰り返します。  
  
## <a name="BKMK_NLB"></a>2.3 NLB をインストールします。  
リモート アクセス クラスターを構成するのには、クラスターの一部を形成するすべてのサーバーに、ネットワーク負荷分散機能をインストールする必要があります。  
  
> [!NOTE]  
> 外部ロード バランサーを使用する場合、この手順は必要ありません。  
  
#### <a name="to-install-the-nlb-role"></a>NLB の役割をインストールするには  
  
1.  サーバー マネージャー コンソールで、DirectAccess サーバー上で、 **ダッシュ ボード**, 、 をクリックして **役割と機能の追加**します。  
  
2.  をクリックして **次** 4 回サーバー機能の選択 画面を取得します。  
  
3.  **機能の選択**  ダイアログ ボックスで選択 **ネットワーク負荷分散**, 、 をクリックして **機能の追加**, 、 をクリックして **次**, 、 をクリックし、 **インストール**します。  
  
4.  **[インストールの進行状況]** ダイアログで、インストールが正常に完了したことを確認し、 **[閉じる]** をクリックします。  
  
5.  すべてのサーバー クラスターのメンバーにするには、この手順を繰り返します。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [手順 3:負荷分散クラスターを構成します。](Step-3-Configure-a-Load-Balanced-Cluster.md)  
  


