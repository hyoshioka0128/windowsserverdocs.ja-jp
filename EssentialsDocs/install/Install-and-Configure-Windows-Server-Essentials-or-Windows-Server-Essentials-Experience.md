---
title: "Windows Server Essentials または Windows Server Essentials エクスペリエンス インストールし、構成"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Windows Server Essentials または Windows Server Essentials エクスペリエンス インストールし、構成

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Windows Server Essentials は、小規模企業に最大 25 ユーザーおよび 50 台のデバイスで最適な最初のサーバーです。 組織では最大 100 ユーザーおよび 200 台のデバイス、Windows Server Essentials エクスペリエンス役割がインストールされたと Windows Server 2012 R2 を使用できます。 このトピックでは、両方のシナリオを説明します。  
  
Windows Server Essentials エクスペリエンスは、すべての機能 (リモート Web アクセスや PC バックアップなど) を使用可能な Windows Server Essentials で、ロックや Windows Server Essentials で適用される制限なくを活用することができます、Windows Server 2016 での役割です。 このサーバーの役割は Windows Server Essentials で利用可能なが既定で有効になっています。
  
Windows Server Essentials または、Essentials Experience 役割をインストールする前に、次の制限に注意してください。  
  
|Windows Server Essentials での Windows Server Essentials エクスペリエンス|Windows Server 2016 での Windows Server Essentials エクスペリエンス
|----|----|
|-フォレストおよびドメインのルートにあるドメイン コントローラーは、すべての FSMO 役割を保持する必要があります。<br /><br /> -(ただしは移行を実行するために 21 日の猶予期間) の既存の Active Directory ドメインのある環境にインストールことはできません。|で既存の Active Directory ドメインのある環境にインストールされている場合、ドメイン コントローラーはありません。<br /><br /> -Active Directory ドメインが存在しない場合は、役割をインストールすると、Active Directory ドメインが作成され、サーバー、ドメイン コントローラーとなるすべての FSMO 役割を保持するフォレストおよびドメインのルートにあります。  
|1 つのドメインにのみ展開できます。|1 つのドメインにのみ展開できます。  
|読み取り専用ドメイン コントローラーは、ドメインに存在できません。|読み取り専用ドメイン コントローラーは、ドメインに存在できません。

> [!NOTE]
>  オペレーティング システムの評価版をダウンロードするには、TechNet Evaluation Center を参照してください。  
>   
>  [Windows Server 2016 をダウンロードします。](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)  
>   
>  [Windows Server Essentials をダウンロードします。](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)
  
## <a name="installation-options"></a>インストール オプション  
 このドキュメントでは、インストールして Windows Server Essentials を構成するための手順を示します。 ネットワーク環境によって、次のインストールに使用できるオプションがあります。  
  
-    Windows Server Essentials (と、Windows Server Essentials エクスペリエンス役割が既定で有効になっている)  
  
-    Windows Server 2016 の Windows Server Essentials エクスペリエンス役割がインストールされました。  
 
|展開環境|説明|関連セクション|  
|----------------------------|-----------------|---------------------|  
|新しい Active Directory 環境|新しい Active Directory 環境を作成する Windows Server Essentials をインストールすることができます。|[新しい Active Directory 環境をセットアップする Windows Server Essentials を展開します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|  
|既存の Active Directory 環境|既存の Active Directory 環境で Windows Server Essentials をインストールすることができます。|[既存の Active Directory 環境での Windows Server Essentials の展開します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|  
|仮想環境|仮想マシンとして Windows Server Essentials を展開することができます。|[お客様の環境を仮想化します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|  
|自動展開|Windows PowerShell を使用して、Windows Server Essentials の展開を自動化できます。|[インストールして Windows PowerShell を使用して Windows Server Essentials を構成します。](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|  
  
## <a name="before-you-begin"></a>開始する前に  
 インストールを開始する前に、次のドキュメントを確認します。  
  
-   [Windows Server Essentials 製品概要](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)  
  

-   [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)   

  
##  <a name="BKMK_NewAD"></a>新しい Active Directory 環境をセットアップする Windows Server Essentials を展開します。  
 Windows Server Essentials では、Active Directory 環境と関連するサーバーの機能をすぐに設定するための手段を提供します。  
  
###  <a name="BKMK_WSEDeploy"></a>Windows Server Essentials の展開  
 Windows Server Essentials を使用している場合は、Windows Server Essentials エクスペリエンスが既に有効です。 ただし、一部のサーバーを構成する手順を完了する必要があります。  
  
##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>物理サーバーで Windows Server Essentials を構成するには  
  
1.  後、Windows**ようこそ**] ページで、**を構成する Windows Server Essentials のウィザード**はデスクトップ上に表示します。  
  
2.  次のように、ウィザードを完了する手順に従います。  
  
    1.  **Windows Server Essentials の構成**] ページで [**次**します。  
  
    2.  **時刻の設定**、日付、時刻、タイム ゾーンが正しいことを確認し、[クリックして**次**します。  
  
    3.  **会社情報**など、会社名を入力**Contoso, ltd.**、] をクリックし、**次**します。 必要に応じて、内部ドメイン名とサーバー名を変更することができます。  
  
    4.  **ネットワークの管理者を作成する**、新しい管理者アカウント名とパスワードを入力します。  
  
        > [!NOTE]
        >  既定値を使用しない**管理者**アカウント名とパスワード。  
  
    5.  をクリックして**構成**します。  
  
3.  サーバーは、構成プロセス中に複数回再起動し、構成が完了するまで、ログオンを自動的に行われます。 このプロセスは、約 20 分間かかります。  
  
4.  デスクトップには、サーバー ダッシュ ボードを起動するダッシュ ボード アイコンをクリックします。 **ホーム**] ページで、完了、**Getting Started**に記載されているタスク、**セットアップ**] タブ。  
  
 サーバーの構成を完了したら後、は、ドメイン コントローラーとして Windows Server Essentials を実行しているサーバーが設定されます。  
  
###  <a name="BKMK_DeployWSERole"></a>Windows Server 2012 R2 Standard および Datacenter の Windows Server Essentials エクスペリエンス役割を展開します。  
 有効にして、次の手順を使用して Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter、Windows Server Essentials Experience 役割を構成するのには、サーバー マネージャーを使用することができます。  
  
##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Windows Server 2012 R2 での Windows Server Essentials エクスペリエンス役割を展開するには  
  
1.  ローカル管理者としてサーバーにログオンします。  
  
2.  開いている**サーバー マネージャー**、] をクリックし、**追加の役割と機能**します。  
  
3.  **サーバーの役割の選択**を選択、**Windows Server Essentials エクスペリエンス**ロール。 ダイアログ ボックスで、[**機能の追加**、] をクリックし、**次**します。  
  
4.  **機能**、] をクリックして**次**します。  
  
5.  レビュー、**Windows Server Essentials エクスペリエンス**ロールの説明、およびクリック**次**します。  
  
6.  以下の] をクリックするページに**[次へ]**、[確認] ページで、] をクリックし、**インストール**します。  
  
7.  インストールが完了したら、Windows Server Essentials エクスペリエンスがサーバー マネージャーでサーバーの役割として表示されます。  
  
8.  フラグ通知領域でサーバー マネージャーで、フラグをクリックし、をクリックして**Windows Server Essentials の構成**します。  
  
9. (省略可能)必要な場合は、サーバー名を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後、サーバーの名前を変更することはできません。  
  

10. 前述の Windows Server Essentials の構成ウィザードの指示に従って、[Windows Server Essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクションです。  

10. 前述の Windows Server Essentials の構成ウィザードの指示に従って、[Windows Server Essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクションです。  

  
##  <a name="BKMK_ExistingAD"></a>既存の Active Directory 環境での Windows Server Essentials の展開します。  
 場合は、既存の Active Directory 環境には、組織は既に Windows Server Essentials を展開することもできます。 さらに、ドメイン コントローラーとして Windows Server Essentials を展開するかどうかに選択できます。  
  
> [!IMPORTANT]
>  このオプションは使用できるは、Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter、Windows Server Essentials エクスペリエンス役割を展開する場合だけです。  
  
#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>既存の Active Directory 環境で Windows Server Essentials を展開するには  
  
1.  (省略可能)必要な場合は、サーバー名を変更します。  
  
    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後、サーバーの名前を変更することはできません。  
  
2.  既存のドメインに次のように Windows Server Essentials を実行しているサーバーを参加させるには。  
  
    1.  このサーバーをドメイン コントローラーにする場合は、レプリカ ドメイン コントローラーとして、サーバーをセットアップします。  
  
    2.  このサーバーをドメイン コントローラーにしたくない場合は、ドメインにこのサーバーを参加させ、Windows ネイティブ ツールを使用します。  
  
3.  サーバーを再起動し、ドメイン管理者としてサーバーにログオンします。  
  
4.  サーバー マネージャーを開き、クリックして**追加の役割と機能**します。  
  
5.  ページに従って、] をクリックを**次**します。  
  
6.  **サーバーの役割の選択**[ **Windows Server Essentials エクスペリエンス**します。 ダイアログ ボックスで、[**機能の追加**、] をクリックし、**次**します。  
  
7.  **機能**、] をクリックして**次**します。  
  
8.  レビュー、**Windows Server Essentials エクスペリエンス**説明、およびクリック**次**します。  
  
9. 以下の] をクリックするページに**[次へ]**、[確認] ページで、] をクリックし、**インストール**します。  
  
10. インストールが完了したら、Windows Server Essentials エクスペリエンスは、サーバー マネージャーでサーバーの役割として表示されます。  
  
11. フラグ通知領域に**サーバー マネージャー**、フラグをクリックし、[クリックして**Windows Server Essentials の構成**します。  
  
12. Windows Server Essentials の構成ウィザードに従います。 構成に応じて、Active Directory は、ドメイン コントローラーまたはドメイン メンバーとして、Windows Server Essentials を構成しているかどうかが通知されます。 をクリックして**構成**、構成を開始します。 構成プロセスは、約 10 分です。  
  
##  <a name="BKMK_VirtualWSE"></a>お客様の環境を仮想化します。  
  仮想マシンとしては、Windows Server Essentials、Windows Server 2012 R2 Standard、および Windows Server 2012 R2 Datacenter を実行することができます。 仮想マシンを実行するには、Hyper-V を実行するサーバーで Hyper-V 管理ツールを使用します。 ライセンスのパースペクティブから Windows Server Essentials にインストールされた Hyper-v の役割をセットアップし、環境を仮想化することができます。 ライセンスでは、Windows Server Essentials を実行している別のゲスト オペレーティング システムをセットアップすることができます。 システム プロバイダーに依存する"™ の構成では、Windows Server Essentials を使用する仮想化された環境をシームレスにセットアップします。  
  
#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Windows Server Essentials を仮想マシンとして展開するには  
  
1.  Windows へようこそ] ページ (構成に応じて、システム プロバイダー"™ s) の後、**開始する前に**ページは、仮想インスタンスとして、または物理ハードウェア上で Windows Server Essentials を設定するオプションを提供します。 これらのオプションの可用性が、システム プロバイダーによってあらかじめ定義されており、両方のオプションは常に利用できません。 インストールする Windows Server Essentials を仮想マシンとして**Windows Server Essentials のインストール**を選択**仮想インスタンスとしてインストール**、] をクリックし、**構成**します。  
  
2.  ウィザードでは、約 5 分かかります仮想マシンをプロビジョニングします。  
  

3.  前述のように、Windows Server Essentials を次に、構成、[Windows Server Essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクションです。  

3.  前述のように、Windows Server Essentials を次に、構成、[Windows Server Essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)セクションです。  

  
##  <a name="BKMK_PowerShell"></a>インストールして Windows PowerShell を使用して Windows Server Essentials を構成します。  
 Windows PowerShell コマンドレットを使用して、Windows Server Essentials のインストールを自動化できます。  
  
#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Windows PowerShell を使用して Windows Server Essentials をインストールするには  
  
1.  管理者特権のコマンド プロンプトから、Windows PowerShell コンソールを開きます。  
  
2.  次のコマンドを使用して、Windows Server Essentials Experience 役割をインストールします。  
  
    ```  
    Add-WindowsFeature ServerEssentialsRole  
    ```  
  
3.  実行`Get-Help Start-WssConfigurationService`します。  
  
    1.  ドメイン コントローラーとして Windows Server Essentials の設定の構成を開始するには、次のコマンドを実行します。  
  
        ```  
        Start-WssConfigurationService -CompanyName "ContosoTest" -DNSName "ContosoTest.com" -NetBiosName "ContosoTest" -ComputerName "YourServerName  œNewAdminCredential $cred  
        ```  
  
    2.  既存のドメイン メンバーとしての Windows Server Essentials の設定の構成を開始するには、次のコマンドを実行します。 このタスクを実行するには、Enterprise Admin グループと Active Directory 内の Domain Admin グループのメンバーがあります。  
  
        ```  
        Start-WssConfigurationService  œCredential <Your Credential>  
  
        ```  
  
4.  次のコマンドを使用して、インストールの進行状況を監視します。  
  
    -   進行状況バーに表示されるインストールの状態を表示するには、実行`Get-WssConfigurationStatus  œShowProgress`します。  
  
    -   進行状況バーなし即時の進行状況を取得するには、実行`Get-WssConfigurationStatus`します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials の新機能](../get-started/what-s-new.md)  
  
-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を使ってみる](../get-started/get-started.md)
