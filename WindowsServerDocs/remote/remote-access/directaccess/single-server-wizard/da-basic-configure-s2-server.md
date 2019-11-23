---
title: 手順 2. 基本的な DirectAccess サーバーを構成する
description: このトピックは、「Windows Server 2016 用はじめにウィザードを使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82bf5fed-93b3-4fa6-8e71-522146eccdb1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a21e5799824c968b29c719585ca16b6b45a9ef37
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404919"
---
# <a name="step-2-configure-the-basic-directaccess-server"></a>手順 2. 基本的な DirectAccess サーバーを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、基本的な DirectAccess の展開に必要なクライアントおよびサーバー設定を構成する方法について説明します。 展開の手順を開始する前に、計画で説明した手順を完了していることを確認します [基本的な DirectAccess 展開を計画](Plan-a-Basic-DirectAccess-Deployment.md)します。  
  
|タスク|説明|  
|----|--------|  
|リモート アクセスの役割をインストールする|リモート アクセスの役割をインストールします。|  
|作業の開始ウィザードを使用して DirectAccess を構成する|新しい作業の開始ウィザードでは、構成操作が大幅に簡略化されます。 このウィザードを使用すると、複雑な DirectAccess をいくつかの簡単な手順で自動的にセットアップできます。 また、Kerberos プロキシが自動的に構成されるため、内部 PKI を展開する必要がなくなり、管理者にとってシームレスなエクスペリエンスが実現されます。|  
|DirectAccess 構成を使用したクライアントの更新|DirectAccess の設定を受け取るには、イントラネット接続時に、クライアントでグループ ポリシーを更新する必要があります。|  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_Role"></a>リモートアクセスの役割をインストールする  
リモート アクセスを展開するには、組織でリモート アクセス サーバーとして機能するサーバーにリモート アクセスの役割をインストールする必要があります。  
  
#### <a name="to-install-the-remote-access-role"></a>リモート アクセスの役割をインストールするには  
  
1.  サーバー マネージャー コンソールでのリモート アクセス サーバー上で、 **ダッシュ ボード**, 、 をクリックして **役割と機能の追加**します。  
  
2.  **[次へ]** を 3 回クリックして、サーバーの役割を選択する画面に移動します。  
  
3.  **[サーバーの役割の選択]** ダイアログで、 **[リモート アクセス]** を選択し、 **[次へ]** をクリックします。  
  
4.  **[機能の選択]** ダイアログで、 **[次へ]** をクリックします。  
  
5.  をクリックして **次**, 、し、 **役割サービスの選択** ダイアログ ボックスで、 をクリックして、 **DirectAccess と VPN (RAS)** チェック ボックスをオンします。  
  
6.  をクリックして **機能の追加**, 、 をクリックして **次**, 、 をクリックし、 **インストール**します。  
  
7.  **[インストールの進行状況]** ダイアログで、インストールが正常に完了したことを確認し、 **[閉じる]** をクリックします。  
  
windows PowerShell の ![](../../../media/Step-2-Configure-the-DirectAccess-Server/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットまたはコマンドレットにより、リモートアクセスの役割がインストールされます。 

1. 管理者として PowerShell を開きます。

2. リモートアクセス機能のインストール:

   ```  
   Install-WindowsFeature RemoteAccess   
   ```  

3. コンピューターを再起動します。

   ```
   Restart-Computer
   ```
   
4. リモートアクセス PowerShell のインストール:

   ```
   Install-WindowsFeature RSAT-RemoteAccess-PowerShell
   ```



  
## <a name="configure-directaccess-with-the-getting-started-wizard"></a>作業の開始ウィザードを使用した DirectAccess の構成  
  
#### <a name="to-configure-directaccess-using-the-getting-started-wizard"></a>作業の開始ウィザードを使用して DirectAccess を構成するには  
  
1.  サーバー マネージャーのクリックで **ツール**, 、 をクリックし、 **リモート アクセス管理**します。  
  
2.  リモート アクセス管理コンソールで、左側のナビゲーション ウィンドウで、構成するロール サービスを選択し、クリックして **作業の開始ウィザードを実行**します。  
  
3.  **[DirectAccess のみを展開します]** をクリックします。  
  
4.  ネットワーク構成のトポロジを選択し、リモート アクセス クライアントの接続先のパブリック名を入力します。 **[次へ]** をクリックします。  
  
    > [!NOTE]  
    > 作業の開始ウィザードでは、既定で、WMI フィルターをクライアント設定の GPO に適用して、ドメイン内のすべてのノート PC とノートブック コンピューターに DirectAccess を展開します。  
  
5.  **[Finish]** (完了) をクリックします。  
  
6.  この展開には PKI が使用されていないため、証明書が見つからない場合は、ウィザードによって、自動的に IP-HTTPS およびネットワーク ロケーション サーバー用の自己署名証明書がプロビジョニングされ、Kerberos プロキシが有効になります。 IPv4 のみの環境では、プロトコル変換のために NAT64 と DNS64 も有効になります。 ウィザードでは、構成の適用が完了したら、クリックして **閉じる**します。  
  
7.  リモート アクセス管理コンソールのコンソール ツリーで、 **[操作の状況]** を選択します。 すべてのモニターの状態が "動作中" と表示されるまで待ちます。 [タスク] ウィンドウの [監視] で、 **[最新の情報に更新]** を定期的にクリックして、表示を更新します。  
  
## <a name="update-clients-with-the-directaccess-configuration"></a>DirectAccess 構成を使用したクライアントの更新  
  
#### <a name="to-update-directaccess-clients"></a>DirectAccess クライアントを更新するには  
  
1.  管理者として PowerShell を開きます。  
  
2.  PowerShell ウィンドウで、「**gpupdate**」と入力して、**Enter** キーを押します。  
  
3.  コンピューターのポリシーの更新が正常に完了するまで待ちます。  
  
4.  「**Get-DnsClientNrptPolicy**」と入力して、**Enter** キーを押します。  
  
    DirectAccess の名前解決ポリシー テーブル (NRPT) エントリが表示されます。 NLS サーバーの除外が表示されることに注意してください。 作業の開始ウィザードによって、自動的にこの DNS エントリが DirectAccess サーバーに対して作成され、DirectAccess サーバーがネットワーク ロケーション サーバーとして機能できるように、関連する自己署名証明書がプロビジョニングされました。  
  
5.  型 **Get NCSIPolicyConfiguration** キーを押します **ENTER**します。 ウィザードによって展開されたネットワーク接続状態インジケーターの設定が表示されます。 DomainLocationDeterminationURL の値を控えておきます。 このネットワーク ロケーション サーバーの URL にアクセスできる場合、クライアントは企業ネットワーク内であると判断し、NRPT 設定は適用されません。  
  
6.  「**Get-DAConnectionStatus**」と入力して、**Enter** キーを押します。 クライアントがネットワーク ロケーション サーバーの URL に到達できるため、状態は **ConnectedLocally** と表示されます。  
  
## <a name="BKMK_Links"></a>前の手順  
  
-   [手順 1: DirectAccess インフラストラクチャを構成する](Step-1-Configure-the-DirectAccess-Infrastructure.md)  
  
## <a name="next-step"></a>次の手順  
  
-   [手順 3. 基本的な DirectAccess 展開を確認する](da-basic-configure-s3-verify.md)  
  


