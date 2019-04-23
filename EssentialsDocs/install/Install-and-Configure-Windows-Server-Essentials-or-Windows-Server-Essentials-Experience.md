---
title: Windows Server Essentials または Windows Server Essentials エクスペリエンスのインストールと構成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 8a2310b178663c6ca32a4e07d11656f1aaf2a11b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844413"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Windows Server Essentials または Windows Server Essentials エクスペリエンスのインストールと構成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials は、小規模企業に最大 25 ユーザーおよび 50 台のデバイスで最適な最初のサーバーです。 組織では最大 100 人のユーザーと 200 台のデバイス、Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 を使用できます。 このトピックでは両方のシナリオについて説明します。  
  
Windows Server Essentials エクスペリエンス役割 (リモート Web アクセスや PC バックアップなど) で使用可能な Windows Server Essentials で、ロックや制限が適用されることがなくすべての機能を活用することができる Windows Server 2016 では、します。 Windows Server Essentials。 このサーバーの役割はも Windows Server Essentials での使用と既定で有効です。
  
Windows Server Essentials または、Essentials Experience 役割をインストールする前に、次の制限事項に注意してください。  
  
|Windows Server Essentials での Windows Server Essentials エクスペリエンス|Windows Server 2016 での Windows Server Essentials エクスペリエンス
|----|----|
|-ドメイン コント ローラーはフォレストおよびドメインのルートには、すべての FSMO 役割を保持する必要があります。<br /><br /> の (ただしは移行を実行するために 21 日の猶予期間) の既存の Active Directory ドメイン環境でインストールことはできません。|で既存の Active Directory ドメイン環境でインストールされている場合、ドメイン コント ローラーはありません。<br /><br /> -Active Directory ドメインが存在しない場合は、役割をインストールすると、Active Directory ドメインが作成され、サーバーは、すべての FSMO 役割を保持しているフォレストおよびドメインのルートにあるドメイン コント ローラーになります。  
|1 つのドメインにのみ展開できます。|1 つのドメインにのみ展開できます。  
|読み取り専用ドメイン コントローラーは、ドメインに存在できません。|読み取り専用ドメイン コントローラーは、ドメインに存在できません。

> [!NOTE]
>  オペレーティング システムの評価版をダウンロードするには、TechNet Evaluation Center を参照してください。  
>   
>  [Windows Server 2016 をダウンロードします。](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials をダウンロードします。](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>インストール オプション  
 このドキュメントでは、Windows Server Essentials をインストールして構成するための詳細な手順について説明します。 ネットワーク環境によって、次のインストール オプションを使用できます。  
  
-    Windows Server Essentials (と既定で有効になっている Windows Server Essentials エクスペリエンス役割)  
  
-    Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2016  
 
|展開環境|説明|関連項目|  
|----------------------------|-----------------|---------------------|  
|新しい Active Directory 環境|Windows Server Essentials をインストールして、新しい Active Directory 環境を作成することができます。|[新しい Active Directory 環境を設定する Windows Server Essentials の展開します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|既存の Active Directory 環境|既存の Active Directory 環境に Windows Server Essentials をインストールすることができます。|[既存の Active Directory 環境での Windows Server Essentials の展開します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|仮想環境|Windows Server Essentials を仮想マシンとして展開できます。|[環境内の仮想化します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|自動展開|Windows PowerShell を使用して Windows Server Essentials の展開を自動化することができます。|[インストールし、Windows PowerShell を使用して Windows Server Essentials を構成します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>始める前に  
 インストールを開始する前に、次のドキュメントを確認してください。  
  
-   [Windows Server Essentials 製品概要](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a> 新しい Active Directory 環境を設定する Windows Server Essentials の展開します。  
 Windows Server Essentials は、Active Directory 環境と関連のサーバー機能を迅速にセットアップする方法を提供します。  
  
###  <a name="BKMK_WSEDeploy"></a> Windows Server Essentials の展開  
 Windows Server Essentials を使用している場合は、Windows Server Essentials エクスペリエンスが既に有効です。 ただし、サーバーを構成するためにいくつかの手順を実行する必要があります。  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>物理サーバーで Windows Server Essentials を構成するには  
  
1.  Windows **[ようこそ]** ページの後、**Windows Server Essentials の構成ウィザード**がデスクトップに表示されます。  
  
2.  次のように、指示に従ってウィザードを完了します。  
  
    1.  **[Windows Server Essentials の構成]** ページで、**[次へ]** をクリックします。  
  
    2.  **[時刻の設定]** で、日付、時刻、タイム ゾーンが正しいことを確認し、**[次へ]** をクリックします。  
  
    3.  **[会社についての情報]** に、「 **Contoso,Ltd.**」などの会社名を入力し、**[次へ]** をクリックします。 オプションで、内部ドメイン名とサーバー名を変更することができます。  
  
    4.  **[ネットワーク管理者の作成]** で、新しい管理者アカウント名とパスワードを入力します。  
  
        > [!NOTE]
        >  既定の **Administrator** アカウント名とパスワードは使用しないでください。  
  
    5.  をクリックして**構成**です。  
  
3.  構成プロセス中にサーバーが複数回再起動し、構成が完了するまで、ログオンが自動的に行われます。 このプロセスには約 20 分かかります。  
  
4.  デスクトップで、ダッシュボード アイコンをクリックし、サーバーを起動します。 **[ホーム]** ページで、**[セットアップ]** タブに表示されている **[作業の開始]** タスクを実行します。  
  
 サーバーの構成を完了すると、Windows Server Essentials を実行しているサーバーがドメイン コントローラーとして設定されます。  
  
###  <a name="BKMK_DeployWSERole"></a> Windows Server 2012 R2 Standard および Datacenter で Windows Server Essentials エクスペリエンス役割を展開します。  
 サーバー マネージャーを使用して、有効にして、次の手順を使用して Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter、Windows Server Essentials エクスペリエンス役割を構成することができます。  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Windows Server 2012 R2 に Windows Server Essentials エクスペリエンス役割を展開するには  
  
1.  ローカル管理者としてサーバーにログオンします。  
  
2.  **サーバー マネージャー**を開いて、**[役割と機能の追加]** をクリックします。  
  
3.  **[サーバーの役割の選択]** で、**[Windows Server Essentials エクスペリエンス]** 役割を選択します。 ダイアログ ボックスで、**[機能の追加]** をクリックし、**[次へ]** をクリックします。  
  
4.  **[機能]** で、**[次へ]** をクリックします。  
  
5.  **[Windows Server Essentials エクスペリエンス]** 役割の説明を確認して、**[次へ]** をクリックします。  
  
6.  次のページで **[次へ]** をクリックし、確認ページで、**[インストール]** をクリックします。  
  
7.  インストールが完了したら、Windows Server Essentials エクスペリエンスがサーバー マネージャーでサーバーの役割として表示されます。  
  
8.  サーバー マネージャーのフラグ通知領域で、フラグをクリックし、**[Windows Server Essentials の構成]** をクリックします。  
  
9. (省略可能) 必要に応じて、サーバー名を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後に、サーバー名を変更することはできません。  
  

10. 前半で説明したように Windows Server Essentials を構成するウィザードの指示に従って、 [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクション。  

10. 前半で説明したように Windows Server Essentials を構成するウィザードの指示に従って、 [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクション。  

  
##  <a name="BKMK_ExistingAD"></a> 既存の Active Directory 環境での Windows Server Essentials の展開します。  
 組織に既存の Active Directory 環境がある場合は、Windows Server Essentials を展開することもできます。 さらに、Windows Server Essentials をドメイン コントローラーとして展開するかどうかを選択することができます。  
  
> [!IMPORTANT]
>  このオプションは Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter、Windows Server Essentials エクスペリエンス役割を展開する場合にのみ使用します。  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>既存の Active Directory 環境に Windows Server Essentials を展開するには  
  
1.  (省略可能) 必要に応じて、サーバー名を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後に、サーバー名を変更することはできません。  
  
2.  次のように、Windows Server Essentials を実行するサーバーを既存のドメインに参加させます。  
  
    1.  このサーバーをドメイン コントローラーにする場合は、サーバーをレプリカ ドメイン コントローラーとしてセットアップします。  
  
    2.  このサーバーをドメイン コントローラーにしない場合は、Windows ネイティブ ツールを使用して、このサーバーをドメインに参加させます。  
  
3.  サーバーを再起動し、ドメイン管理者としてサーバーにログオンします。  
  
4.  サーバー マネージャーを開いて、[**役割と機能の追加]** をクリックします。  
  
5.  次のページで、**[次へ]** をクリックします。  
  
6.  **[サーバーの役割の選択]** で、**[Windows Server Essentials エクスペリエンス]** を選択します。 ダイアログ ボックスで、**[機能の追加]** をクリックし、**[次へ]** をクリックします。  
  
7.  **[機能]** で、**[次へ]** をクリックします。  
  
8.  **[Windows Server Essentials エクスペリエンス]** の説明を確認して、**[次へ]** をクリックします。  
  
9. 次のページで **[次へ]** をクリックし、確認ページで、**[インストール]** をクリックします。  
  
10. インストールが完了したら、Windows Server Essentials エクスペリエンスは、サーバー マネージャーでサーバーの役割として表示されます。  
  
11. **サーバー マネージャー**のフラグ通知領域で、フラグをクリックし、**[Windows Server Essentials の構成]** をクリックします。  
  
12. ウィザードに従って、Windows Server Essentials を構成します。 Active Directory 構成に応じて、Windows Server Essentials をドメイン コントローラー上に構成しているか、またはドメイン メンバーとして構成しているかどうかが通知されます。 **[構成]** をクリックして、構成を開始します。 構成プロセスが完了するまで、約 10 分かかります。  
  
##  <a name="BKMK_VirtualWSE"></a> 環境内の仮想化します。  
  Windows Server Essentials、Windows Server 2012 R2 Standard、および Windows Server 2012 R2 Datacenter は、仮想マシンとして実行することができます。 Hyper-V を実行するサーバーで、Hyper-V 管理ツールを使用して仮想マシンを実行します。 ライセンスのパースペクティブからは、Windows Server Essentials を使用すると、HYPER-V ロールをセットアップし、環境を仮想化できます。 ライセンスを使用すると、Windows Server Essentials を実行している別のゲスト オペレーティング システムを設定できます。 によって、システムのプロバイダー"™ の構成では、Windows Server Essentials を使用する仮想化環境をシームレスにセットアップします。  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Windows Server Essentials を仮想マシンとして展開するには  
  
1.  (構成によってはシステム プロバイダー"セント s)、Windows へようこそ ページの後、**開始する前に**ページには、仮想インスタンスとして、または物理ハードウェア上に Windows Server Essentials を設定するオプションが提供されます。 これらのオプションが使用できるかどうかは、システム プロバイダーによって事前定義されており、両方のオプションが常に使用できるとは限りません。 仮想マシンでは、Windows Server Essentials をインストールする**Install Windows Server Essentials**を選択します**仮想インスタンスとしてインストール**、 をクリックし、**構成**します。  
  
2.  ウィザードによって仮想マシンがプロビジョニングされますが、これには約 5 分かかります。  
  

3.  前半で説明したように、Windows Server Essentials を次に、構成、 [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクション。  

3.  前半で説明したように、Windows Server Essentials を次に、構成、 [Deploying Windows Server Essentials](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクション。  

  
##  <a name="BKMK_PowerShell"></a> インストールし、Windows PowerShell を使用して Windows Server Essentials を構成します。  
 Windows PowerShell コマンドレットを使用して、Windows Server Essentials のインストールを自動化できます。  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Windows PowerShell を使用して Windows Server Essentials をインストールするには  
  
1.  管理者特権でのコマンド プロンプトから Windows PowerShell コンソールを開きます。  
  
2.  次のコマンドを使用して、Windows Server Essentials エクスペリエンス役割をインストールします。  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  `Get-Help Start-WssConfigurationService` を実行します。  
  
    1.  次のコマンドを実行して、Windows Server Essentials をドメイン コントローラーとしてセットアップするための構成を開始します。  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  次のコマンドを実行して、Windows Server Essentials を既存のドメイン メンバーとしてセットアップするための構成を開始します。 このタスクを実行するには、Active Directory の Enterprise Admin グループと Domain Admin グループのメンバーである必要があります。  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  次のコマンドを使用して、インストールの進行状況を監視します。  
  
    -   インストール状態が進行状況バーに表示されるようにするには、 `Get-WssConfigurationStatus  œShowProgress`を実行します。  
  
    -   進行状況バーなしで、即時の進行状況を得るには、`Get-WssConfigurationStatus` を実行します。  
  
## <a name="see-also"></a>関連項目  
  
-   [新機能 Windows Server Essentials の新機能](../get-started/what-s-new.md)  
  
-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を概要します。](../get-started/get-started.md)
