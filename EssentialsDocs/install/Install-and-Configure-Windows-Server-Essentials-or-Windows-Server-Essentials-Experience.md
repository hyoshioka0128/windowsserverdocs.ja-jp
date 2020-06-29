---
title: Windows Server Essentials または Windows Server Essentials エクスペリエンスのインストールと構成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 48ea6cd4-3955-4aaf-9236-2515a6c3e730
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 338fe421b4ba30afc1b2cd3ee983668b282f3a15
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470957"
---
# <a name="install-and-configure-windows-server-essentials-or-windows-server-essentials-experience"></a>Windows Server Essentials または Windows Server Essentials エクスペリエンスのインストールと構成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

Windows Server Essentials は、最大25人のユーザーと50のデバイスを備えた小規模企業向けの理想的な最初のサーバーです。 最大100のユーザーと200のデバイスがある組織では、windows server Essentials Experience 役割がインストールされた Windows Server 2012 R2 を使用できるようになりました。 このトピックでは両方のシナリオについて説明します。

Windows server Essentials エクスペリエンスは Windows server 2016 の役割であり、windows server essentials で適用されるロックや制限なしに、Windows server Essentials で利用可能なすべての機能 (リモート Web アクセス、PC バックアップなど) を利用できます。 このサーバーの役割は、Windows Server Essentials でも使用でき、既定で有効になっています。

Windows Server Essentials または Essentials エクスペリエンスロールをインストールする前に、次の制限事項に注意してください。

|Windows Server Essentials の windows Server Essentials エクスペリエンス|Windows Server 2016 の windows Server Essentials エクスペリエンス
|----|----|
|-フォレストおよびドメインのルートにあるドメインコントローラーである必要があり、すべての FSMO 役割を保持する必要があります。<br /><br /> -既存の Active Directory ドメインを持つ環境にはインストールできません (ただし、移行の実行に21日の猶予期間があります)。|-既存の Active Directory ドメインを持つ環境にインストールされている場合、ドメインコントローラーである必要はありません。<br /><br /> -Active Directory ドメインが存在しない場合、役割をインストールすると Active Directory ドメインが作成され、サーバーはフォレストおよびドメインのルートにあるドメインコントローラーになり、すべての FSMO 役割が保持されます。
|1 つのドメインにのみ展開できます。|1 つのドメインにのみ展開できます。
|読み取り専用ドメイン コントローラーは、ドメインに存在できません。|読み取り専用ドメイン コントローラーは、ドメインに存在できません。

> [!NOTE]
>  オペレーティング システムの評価版をダウンロードするには、TechNet Evaluation Center を参照してください。
>
>  [Windows Server 2016 のダウンロード](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)
>
>  [Windows Server Essentials のダウンロード](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016-essentials)

## <a name="installation-options"></a>インストール オプション
 このドキュメントでは、Windows Server Essentials をインストールして構成するための詳細な手順について説明します。 ネットワーク環境によって、次のインストール オプションを使用できます。

-    Windows Server Essentials (Windows Server Essentials エクスペリエンスの役割が既定で有効)

-    Windows server Essentials の役割がインストールされた windows Server 2016

|デプロイ環境|説明|関連項目|
|----------------------------|-----------------|---------------------|
|新しい Active Directory 環境|Windows Server Essentials をインストールして、新しい Active Directory 環境を作成することができます。|[Windows Server Essentials を展開して、新しい Active Directory 環境をセットアップする](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_NewAD)|
|既存の Active Directory 環境|既存の Active Directory 環境に Windows Server Essentials をインストールすることができます。|[既存の Active Directory 環境に Windows Server Essentials を展開する](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_ExistingAD)|
|仮想環境|Windows Server Essentials を仮想マシンとして展開できます。|[環境の仮想化](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_VirtualWSE)|
|自動化されたデプロイ|Windows PowerShell を使用して Windows Server Essentials の展開を自動化することができます。|[Windows PowerShell を使用して、Windows Server Essentials をインストールおよび構成する](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_PowerShell)|

## <a name="before-you-begin"></a>開始する前に
 インストールを開始する前に、次のドキュメントを確認してください。

-   [Windows Server Essentials 製品の概要](https://www.microsoft.com/server-cloud/windows-server-essentials/windows-server-2012-r2-essentials.aspx)


-   [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)


##  <a name="deploy-windows-server-essentials-to-set-up-a-new-active-directory-environment"></a><a name="BKMK_NewAD"></a>Windows Server Essentials を展開して新しい Active Directory 環境をセットアップする
 Windows Server Essentials は、Active Directory 環境と関連のサーバー機能を迅速にセットアップする方法を提供します。

###  <a name="deploying-windows-server-essentials"></a><a name="BKMK_WSEDeploy"></a>Windows Server Essentials の展開
 Windows Server Essentials を使用している場合は、Windows Server Essentials エクスペリエンスが既に有効になっています。 ただし、サーバーを構成するためにいくつかの手順を実行する必要があります。

##### <a name="to-configure-windows-server-essentials-on-a-physical-server"></a>物理サーバーで Windows Server Essentials を構成するには

1. Windows [**ようこそ**] ページの後、**Windows Server Essentials の構成ウィザード**がデスクトップに表示されます。

2. 次のように、指示に従ってウィザードを完了します。

   1.  [**Windows Server Essentials の構成**] ページで、[**次へ**] をクリックします。

   2.  [**時刻の設定**] で、日付、時刻、タイム ゾーンが正しいことを確認し、[**次へ**] をクリックします。

   3.  [**会社についての情報**] に、「**Contoso,Ltd.**」などの会社名を入力し、[**次へ**] をクリックします。 オプションで、内部ドメイン名とサーバー名を変更することができます。

   4.  [**ネットワーク管理者の作成**] で、新しい管理者アカウント名とパスワードを入力します。

       > [!NOTE]
       >  既定の **Administrator** アカウント名とパスワードは使用しないでください。

   5.  **[構成]** をクリックします。

3. 構成プロセス中にサーバーが複数回再起動し、構成が完了するまで、ログオンが自動的に行われます。 このプロセスには約 20 分かかります。

4. デスクトップで、ダッシュボード アイコンをクリックし、サーバーを起動します。 [**ホーム**] ページで、[**セットアップ**] タブに表示されている [**作業の開始**] タスクを実行します。

   サーバーの構成を完了すると、Windows Server Essentials を実行しているサーバーがドメイン コントローラーとして設定されます。

###  <a name="deploying-the-windows-server-essentials-experience-role-in-windows-server-2012-r2-standard-and-datacenter"></a><a name="BKMK_DeployWSERole"></a>Windows Server 2012 R2 Standard および Datacenter での Windows Server Essentials エクスペリエンス役割の展開
 次の手順に従って、サーバーマネージャーを使用して、Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter で Windows Server Essentials エクスペリエンスの役割を有効にし、構成することができます。

##### <a name="to-deploy-the-windows-server-essentials-experience-role-in-windows-server-2012-r2"></a>Windows Server 2012 R2 に Windows Server Essentials エクスペリエンス役割を展開するには

1.  ローカル管理者としてサーバーにログオンします。

2.  **サーバー マネージャー**を開いて、[**役割と機能の追加**] をクリックします。

3.  [**サーバーの役割の選択**] で、[**Windows Server Essentials エクスペリエンス**] 役割を選択します。 ダイアログ ボックスで、[**機能の追加**] をクリックし、[**次へ**] をクリックします。

4.  [**機能**] で、[**次へ**] をクリックします。

5.  [**Windows Server Essentials エクスペリエンス**] 役割の説明を確認して、[**次へ**] をクリックします。

6.  次のページで [**次へ**] をクリックし、確認ページで、[**インストール**] をクリックします。

7.  インストールが完了したら、Windows Server Essentials エクスペリエンスをサーバーの役割としてサーバーマネージャーに表示する必要があります。

8.  サーバー マネージャーのフラグ通知領域で、フラグをクリックし、[**Windows Server Essentials の構成**] をクリックします。

9. (省略可能) 必要に応じて、サーバー名を変更します。

    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後に、サーバー名を変更することはできません。


10. 前の「 [Windows Server essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)」で説明したように、ウィザードに従って Windows server essentials を構成します。

10. 前の「 [Windows Server essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)」で説明したように、ウィザードに従って Windows server essentials を構成します。


##  <a name="deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a><a name="BKMK_ExistingAD"></a>Windows Server Essentials を既存の Active Directory 環境に展開する
 組織に既存の Active Directory 環境がある場合は、Windows Server Essentials を展開することもできます。 さらに、Windows Server Essentials をドメイン コントローラーとして展開するかどうかを選択することができます。

> [!IMPORTANT]
>  このオプションは、windows server 2012 R2 Standard または Windows Server 2012 R2 Datacenter で Windows Server Essentials エクスペリエンスの役割を展開する場合にのみ使用できます。

#### <a name="to-deploy-windows-server-essentials-in-an-existing-active-directory-environment"></a>既存の Active Directory 環境に Windows Server Essentials を展開するには

1.  (省略可能) 必要に応じて、サーバー名を変更します。

    > [!IMPORTANT]
    >  Windows Server Essentials を構成した後に、サーバー名を変更することはできません。

2.  次のように、Windows Server Essentials を実行するサーバーを既存のドメインに参加させます。

    1.  このサーバーをドメイン コントローラーにする場合は、サーバーをレプリカ ドメイン コントローラーとしてセットアップします。

    2.  このサーバーをドメイン コントローラーにしない場合は、Windows ネイティブ ツールを使用して、このサーバーをドメインに参加させます。

3.  サーバーを再起動し、ドメイン管理者としてサーバーにログオンします。

4.  サーバー マネージャーを開いて、[**役割と機能の追加]** をクリックします。

5.  次のページで、[**次へ**] をクリックします。

6.  [**サーバーの役割の選択**] で、[**Windows Server Essentials エクスペリエンス**] を選択します。 ダイアログ ボックスで、[**機能の追加**] をクリックし、[**次へ**] をクリックします。

7.  [**機能**] で、[**次へ**] をクリックします。

8.  [**Windows Server Essentials エクスペリエンス**] の説明を確認して、[**次へ**] をクリックします。

9. 次のページで [**次へ**] をクリックし、確認ページで、[**インストール**] をクリックします。

10. インストールが完了すると、Windows Server Essentials エクスペリエンスがサーバーマネージャーにサーバーの役割として表示されます。

11. **サーバー マネージャー**のフラグ通知領域で、フラグをクリックし、[**Windows Server Essentials の構成**] をクリックします。

12. ウィザードに従って、Windows Server Essentials を構成します。 Active Directory 構成に応じて、Windows Server Essentials をドメイン コントローラー上に構成しているか、またはドメイン メンバーとして構成しているかどうかが通知されます。 [**構成**] をクリックして、構成を開始します。 構成プロセスが完了するまで、約 10 分かかります。

##  <a name="virtualize-your-environment"></a><a name="BKMK_VirtualWSE"></a>環境を仮想化する
  Windows Server Essentials、Windows Server 2012 R2 Standard、および Windows Server 2012 R2 Datacenter は、仮想マシンとして実行できます。 Hyper-V を実行するサーバーで、Hyper-V 管理ツールを使用して仮想マシンを実行します。 Windows Server Essentials では、ライセンスの観点から、Hyper-v の役割を設定し、環境を仮想化することができます。 このライセンスでは、Windows Server Essentials を実行している別のゲストオペレーティングシステムをセットアップすることができます。 Windows Server Essentials では、システムプロバイダー "され s の構成に応じて、仮想化環境をシームレスに設定できます。

#### <a name="to-deploy-windows-server-essentials-as-a-virtual-machine"></a>Windows Server Essentials を仮想マシンとして展開するには

1.  Windows の [ようこそ] ページの後 (システムプロバイダーの "され s 構成" によって異なります) で、[**開始する前**に] ページに、仮想インスタンスとして、または物理ハードウェア上に Windows Server Essentials を設定するオプションが表示されます。 これらのオプションが使用できるかどうかは、システム プロバイダーによって事前定義されており、両方のオプションが常に使用できるとは限りません。 Windows Server Essentials を仮想マシンとしてインストールするには、[ **Windows Server essentials のインストール**] で、[**仮想インスタンスとしてインストール**] を選択し、[**構成**] をクリックします。

2.  ウィザードによって仮想マシンがプロビジョニングされますが、これには約 5 分かかります。

3.  次に、windows [Server essentials の展開](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md#BKMK_WSEDeploy)に関するセクションで前述したように、Windows server essentials を構成します。


##  <a name="install-and-configure-windows-server-essentials-by-using-windows-powershell"></a><a name="BKMK_PowerShell"></a>Windows PowerShell を使用した Windows Server Essentials のインストールと構成
 Windows PowerShell コマンドレットを使用して、Windows Server Essentials のインストールを自動化できます。

#### <a name="to-install-windows-server-essentials-by-using-windows-powershell"></a>Windows PowerShell を使用して Windows Server Essentials をインストールするには

1.  管理者特権でのコマンド プロンプトから Windows PowerShell コンソールを開きます。

2.  次のコマンドを使用して、Windows Server Essentials Experience 役割をインストールします。

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

    -   進行状況バーなしで、即時の進行状況を得るには、 `Get-WssConfigurationStatus`を実行します。

## <a name="see-also"></a>関連項目

-   [Windows Server Essentials の新機能](../get-started/what-s-new.md)

-   [Windows Server Essentials のインストール](Install-Windows-Server-Essentials.md)

-   [Windows Server Essentials を使ってみる](../get-started/get-started.md)
