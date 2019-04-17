---
ms.assetid: 66fa945e-598d-4f18-b603-97a39ce0d836
title: "Windows Server 2012 の Active Directory インストール Read-Only ドメイン コントローラー (RODC) (レベル 200)"
description: "このトピックでは、段階的 RODC アカウントを作成し、そのアカウントに RODC のインストール中にサーバーをアタッチする方法について説明します。 このトピックでは、段階的なインストールを実行せずに RODC をインストールする方法についても説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 78281ca845f79955aaa25aa45394284c59e639cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-windows-server-2012-active-directory-read-only-domain-controller-rodc-level-200"></a>Windows Server 2012 の Active Directory インストール Read-Only ドメイン コントローラー (RODC) (レベル 200)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、段階的 RODC アカウントを作成し、そのアカウントに RODC のインストール中にサーバーをアタッチする方法について説明します。 このトピックでは、段階的なインストールを実行せずに RODC をインストールする方法についても説明します。  
  
## <a name="stage-rodc-workflow"></a>段階 RODC のワークフロー  
段階的段階的な 2 つのドメイン コントローラー (RODC) のインストール動作のみになります。  
  
1.  使用されていないコンピューター アカウントをステージングします。  
  
2.  昇格中にそのアカウントに RODC をアタッチします。  
  
次の図は、Active Directory ドメイン サービス Read-Only に移行するプロセスは、Active Directory 管理センター (Dsac.exe) を使用してドメイン内の空の RODC コンピューター アカウントを作成するドメイン コントローラー。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stagedcreation.png)  
  
## <a name="BKMK_StagePS"></a>段階 RODC の Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Add-addsreadonlydomaincontrolleraccount|-SkipPreChecks<br /><br />***-DomainControllerAccountName***<br /><br />***-DomainName***<br /><br />***-サイト名***<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />***資格情報***<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />*-NoGlobalCatalog*<br /><br />*-InstallDNS*<br /><br />-ReplicationSourceDC|  
  
> [!NOTE]  
> **-Credential**引数は、のみために必要なかどうかは、既にログオンしていない、Domain Admins グループのメンバーとして。  
  
## <a name="attach-rodc-workflow"></a>RODC アタッチのワークフロー  
次の図を既にインストールされている、AD DS の役割を Active Directory Domain Services 構成プロセスを示しています、RODC アカウントをステージングし、開始する**このサーバーのドメイン コントローラーを昇格**サーバー マネージャーを使用して、既存のドメインに段階的なコンピューター アカウントにアタッチすることで新しい RODC を作成します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_stageddeploy_beta1.png)  
  
## <a name="BKMK_AttachPS"></a>RODC の Windows PowerShell をアタッチします。  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Install-AddsDomaincontroller|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-Safemodeadministratorpassword*<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***資格情報***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />*-InstallationMediaPath*<br /><br />*-Logpath*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />***-Useexistingaccount***|  
  
> [!NOTE]  
> **-Credential**引数は、のみために必要なかどうかは、既にログオンしていない、Domain Admins グループのメンバーとして。  
  
## <a name="staging"></a>ステージング  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_PreCreateRODC.png)  
  
Active Directory 管理センターを開くことによって、読み取り専用ドメイン コントローラー コンピューター アカウントのステージングの操作を実行する (**Dsac.exe**)。 ナビゲーション ウィンドウで、ドメインの名前をクリックします。 ダブルクリック**ドメイン コントローラー**管理の一覧でします。 をクリックして**を事前に作成、Read-only ドメイン コントローラー アカウント**作業ウィンドウでします。  
  
Active Directory 管理センターの詳細については、次を参照してください。[詳細 AD DS 管理を使用して Active Directory 管理センター (&) #40 です。レベル 200 & #41 です。](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)し確認[Active Directory 管理センター: Getting Started](https://technet.microsoft.com/library/dd560651(WS.10).aspx)します。  
  
読み取り専用ドメイン コントローラーを作成してきた経験がある場合は、インストール ウィザードは、古い Active Directory ユーザーとコンピューター スナップインから Windows Server 2008 を使用する場合のように、同じグラフィカル インターフェイスを備えたし、非推奨の dcpromo で使用される無人セットアップ ファイルの形式で構成をエクスポートするには、同じコードを使用してを検出します。  
  
Windows Server 2012 のステージ RODC コンピューター アカウントに新しい ADDSDeployment コマンドレットが導入されていますが、ウィザードではその操作のコマンドレットを使用しません。 次のセクションに関連付けられている情報を各わかりやすくするためには、それと同等のコマンドレットと引数を表示します。  
  
**を事前に作成、Read-only ドメイン コントローラー アカウント**Active Directory 管理センターのタスク] ウィンドウのリンクは、Windows PowerShell の ADDSDeployment コマンドレットに相当します。  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
### <a name="welcome"></a>ようこそ  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_WelcomeStage1.png)  
  
**Active Directory ドメイン サービス インストール ウィザードへようこそ**ダイアログという名前の 1 つのオプションには、**詳細モード インストールを使用して**します。 このオプションを選択し] をクリックして**次**パスワード レプリケーション ポリシー オプションを表示します。 (これはこのセクションで後で詳しく説明します) のパスワード レプリケーション ポリシー オプションの既定値を使用するには、このオプションをオフにします。  
  
### <a name="network-credentials"></a>ネットワーク資格情報  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Creds.png)  
  
ドメイン名オプション、**ネットワーク資格情報**] ダイアログには、既定では、Active Directory 管理センターの対象となるドメインが表示されます。 現在の資格情報は、既定で使用されます。 場合は、Domain Admins グループのメンバーシップが含まれない、] をクリックして**別の資格情報**、] をクリック**設定**をユーザー名とパスワードが Domain Admins のメンバーであると、ウィザードを提供します。  
  
それと同等の ADDSDeployment Windows PowerShell 引数です。  
  
```  
-credential <pscredential>  
```  
  
ステージング システムは Windows Server 2008 R2 からの直接ポートと、新しい Adprep 機能を提供しないことに留意してください。 段階的 RODC アカウントを展開する場合は、する必要があります、自動 rodcprep 操作が実行されるようにそのドメイン内で非段階的 RODC を最初に展開または手動で adprep.exe を実行 /rodcprep 最初します。  
  
それ以外の場合、エラーが表示されます「しないことができます"adprep/rodcprep"was not yet run ために、このドメインの読み取り専用ドメイン コントローラーをインストールする」です。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepNotRunError.png)  
  
### <a name="specify-the-computer-name"></a>コンピューター名を指定します。  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1CompName.png)  
  
**コンピューター名を指定**] ダイアログでは、単一ラベルを入力する必要があります**コンピューター名**が存在しないドメイン コントローラーのします。 ドメイン コントローラーを構成し、後でこのアカウントに接続する必要があります、同じ名前を付ける、または昇格操作は段階的アカウントを検出しません。  
  
それと同等の ADDSDeployment Windows PowerShell 引数です。  
  
```  
-domaincontrolleraccountname <string>  
```  
  
### <a name="select-a-site"></a>サイトを選択します。  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Site.png)  
  
**サイトを選択して**ダイアログは、現在のフォレストの Active Directory サイトの一覧を示しています。 段階的読み取り専用ドメイン コントローラー操作では、一覧から 1 つのサイトを選択する必要があります。 RODC では、この情報を使用して、構成パーティションに NTDS 設定オブジェクトを作成し、展開後に最初に開始されたときに、正しいサイトに参加します。  
  
それと同等の ADDSDeployment Windows PowerShell 引数です。  
  
```  
-sitename <string>  
```  
  
### <a name="additional-domain-controller-options"></a>追加のドメイン コントローラー オプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DCOptions.png)  
  
**追加のドメイン コントローラー オプション**] ダイアログでは、ドメイン コントローラーとして実行しているが含まれることを指定することができます、**DNS サーバー**と**グローバル カタログ**します。 既定では両方がインストールされているために、読み取り専用ドメイン コントローラーが DNS と GC サービスを提供することをお勧めします。RODC 役割の 1 つの目的でブランチ オフィスのシナリオは、ワイド エリア ネットワークを利用できない可能性がありますおこれらの DNS およびグローバル カタログ サービスなし、ブランチ内のコンピューターでは、AD DS リソースと機能を使用できません。  
  
**読み取り専用ドメイン コントローラー (RODC)**オプションは事前に選択し、無効にすることはできません。 それと同等の ADDSDeployment Windows PowerShell 引数は次のとおりです。  
  
```  
-installdns <string>  
-NoGlobalCatalog <{$true | $false}>  
  
```  
  
> [!NOTE]  
> 既定で、**- NoGlobalCatalog**値は $false で、引数が指定されていない場合、ドメイン コントローラーはグローバル カタログ サーバーになることを意味します。  
  
### <a name="specify-the-password-replication-policy"></a>パスワード レプリケーション ポリシーを指定します。  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRP.png)  
  
**パスワード レプリケーション ポリシーを指定する**] ダイアログでは、この読み取り専用ドメイン コントローラー上でパスワードをキャッシュできるアカウントの既定の一覧を変更することができます。 構成されている一覧内のアカウント**拒否**ではない、または (暗黙的) の一覧にはパスワードはキャッシュされません。 RODC のパスワードをキャッシュすることはできませんとできません接続し、アカウント、書き込み可能なドメイン コントローラーへの認証は、リソースまたは Active Directory によって提供される機能にアクセスできません。  
  
> [!IMPORTANT]  
> ウィザードが表示のみ、このダイアログ ボックスを選択するかどうか、**詳細モード インストールを使用して**ようこそ画面にチェック ボックスをオンします。 このチェック ボックスをオフにした場合は、次の既定のグループと値のウィザードが使用されます。  
>   
> -   管理者を拒否します。  
> -   Server Operators を拒否します。  
> -   バックアップ オペレーターの拒否  
> -   アカウントの演算子の拒否  
> -   拒否 RODC Password Replication Group - が拒否されました  
> -   RODC Password Replication Group - 許可を許可します。  
  
それと同等の ADDSDeployment Windows PowerShell 引数は次のとおりです。  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1PRPAllow.png)  
  
### <a name="delegation-of-rodc-installation-and-administration"></a>RODC のインストールと管理の委任  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1DelegateAdmin.png)  
  
**委任の RODC のインストールと管理**] ダイアログでは、ユーザーまたはサーバーを RODC コンピューター アカウントに接続を許可されているユーザーを含むグループを構成することができます。 をクリックして**設定**ユーザーまたはグループのドメインを参照します。 ユーザーまたはグループのこのダイアログが向上ローカル管理アクセス許可] で、RODC に指定されています。 指定したユーザーまたは指定したグループのメンバーは、コンピューターの Administrators グループと同等の権限によって RODC 上の操作を実行できます。 *いない*、Domain Admins グループまたはドメインのビルトイン管理者グループのメンバーです。  
  
このオプションを使用すると、Domain Admins グループに支社の管理者メンバーシップを与えずに支社の管理を委任できます。 RODC 管理の委任は必要ありません。  
  
それと同等の ADDSDeployment Windows PowerShell 引数です。  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
### <a name="summary"></a>概要  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Summary.png)  
  
**概要**] ダイアログでは、設定内容を確認することができます。 これは、ウィザードが段階的アカウントを作成する前に、インストールを中止する最後の機会です。 をクリックして**次**を段階的 RODC コンピューター アカウントを作成する準備ができたらします。  をクリックして**設定のエクスポート**を非推奨の dcpromo 無人セットアップファイル形式で応答ファイルを保存します。  
  
### <a name="creation"></a>作成  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1InstallProgress.png)  
  
**Active Directory ドメイン サービス インストール ウィザード**Active Directory に段階的読み取り専用ドメイン コントローラーを作成します。 開始した後、この操作をキャンセルすることはできません。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage1Complete.png)  
  
Windows PowerShell の ADDSDeployment モジュールを使用して、読み取り専用ドメイン コントローラーのコンピューター アカウントをステージングするには、次のコマンドレットを使用します。  
  
```  
Add-addsreadonlydomaincontrolleraccount  
  
```  
  
参照してください[段階 RODC の Windows PowerShell](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_StagePS)必須およびオプションの引数。  
  
**Add-addsreadonlydomaincontrolleraccount**のみが 1 つの操作 (前提条件のチェックとインストール) の 2 つのフェーズ、以下のスクリーン ショットが最低限の必須引数を使用したインストール フェーズを表示します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODC.png)  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSAddRODCValidating.png)  
  
段階 RODC 操作は、Active Directory の RODC コンピューター アカウントを作成します。 Active Directory 管理センターを示しています、**ドメイン コントローラーの種類**として、**使用されていないドメイン コントローラー アカウント**します。 このドメイン コントローラーの種類は、段階的 RODC アカウントが読み取り専用ドメイン コントローラーとして、それにアタッチするようにサーバーの準備ができてであることを示します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Unoccupied.png)  
  
> [!IMPORTANT]  
> Active Directory 管理センターは読み取り専用ドメイン コントローラーのコンピューター アカウントに、サーバーをアタッチする必要はありません。 サーバー マネージャーを使用して、Active Directory ドメイン サービス構成ウィザードまたは ADDSDeployment Windows PowerShell モジュール コマンドレット**Install-addsdomaincontroller**新しい RODC をアタッチすることのアカウントをステージングします。 手順は、段階的 RODC コンピューター アカウントに RODC コンピューター アカウントをステージングしたときに決定した構成オプションが含まれているは例外で、既存のドメインに新しい書き込み可能なドメイン コントローラーの追加に似ています。  
  
## <a name="attaching"></a>アタッチ  
  
### <a name="deployment-configuration"></a>展開の構成  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
サーバー マネージャーですべてのドメイン コントローラーの昇格を開始する、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。  
  
読み取り専用ドメイン コントローラーを既存のドメインに追加するには、選択**ドメイン コントローラーを既存のドメインに追加**] をクリックし、**選択**] ボタンをクリックして**このドメインのドメイン情報を指定**します。 サーバー マネージャーに自動的に求めるプロンプトが有効な資格情報、または] をクリックすることができます**変更**します。  
  
RODC をアタッチするには、Windows Server 2012 での Domain Admins グループのメンバーシップが必要です。 Active Directory ドメイン サービス構成ウィザードが表示されたら後で、現在の資格情報が適切なアクセス許可またはグループのメンバーシップがあるない場合。  
  
**展開構成**ADDSDeployment Windows PowerShell コマンドレットと引数は。  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>ドメイン コント ローラー オプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2DCOptions.png)  
  
**ドメイン コントローラー オプション**ページが、ドメインを新しいドメイン コントローラーのコントローラー オプションが表示されます。 このページが読み込まれると、Active Directory ドメイン サービス構成ウィザードは、使用されていないアカウントを確認する既存のドメイン コントローラーに LDAP クエリを送信します。 かどうか、クエリは、現在のコンピューターと同じ名前を共有しているコンピューター アカウントに使用されていないドメイン コントローラーを検索し、ウィザード ページの上部に情報のメッセージが表示されます"**ディレクトリに、ターゲット サーバーの名前と一致する事前に作成した RODC アカウントが存在します。既存の RODC アカウントを使用して、またはこのドメイン コントローラーを再インストールするかどうか**." ウィザードを使用して、**既存の RODC アカウントを使用して**既定の構成とします。  
  
> [!IMPORTANT]  
> 使用することができます、**このドメイン コントローラーを再インストール**オプションと、ドメイン コントローラーが物理的な問題が発生した機能を返すことはできません。 このセーブ データは、時間、ドメイン コントローラー コンピューター アカウントのままにして、ドメイン コントローラーを構成するときにし、オブジェクトの Active Directory 内のメタデータします。 新しいコンピューターをインストール、*同名*、ドメイン内のドメイン コントローラーとして昇格します。 **このドメイン コントローラーを再インストール**オプションは、ドメイン コントローラー オブジェクトのメタデータを Active Directory (メタデータ クリーンアップ) から削除した場合は使用できません。  
  
サーバーを RODC コンピューター アカウントにアタッチする場合は、ドメイン コントローラー オプションを構成することはできません。 段階的 RODC コンピューター アカウントを作成するときに、ドメイン コントローラー オプションを構成します。  
  
指定した**ディレクトリ サービス復元モード パスワード**サーバーに適用されるパスワード ポリシーに従う必要があります。 常に強力で複雑なパスワードまたは可能であれば、パスフレーズを選択します。  
  
**ドメイン コントローラー オプション**ADDSDeployment Windows PowerShell 引数は。  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 引数として提供されると、サイト名は既に存在して**sitename**します。 **Install-addsdomaincontroller**コマンドレットは、サイト名を作成しません。 コマンドレットを使用する**新しい adreplicationsite**新しいサイトを作成します。  
  
**Install-addsdomaincontroller**引数が指定されていない場合はサーバー マネージャーと同じ既定値に従います。  
  
**SafeModeAdministratorPassword**引数の操作は特別な。  
  
-   場合*が指定されていない*を引数としてコマンドレットは、して、マスクされたパスワードの確認入力を求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
    たとえば、corp.contoso.com で新しい RODC を作成してなると、マスクされたパスワードの確認入力を求め。  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
    ```  
  
-   指定されている場合*値を持つ*、値が、セキュリティで保護された文字列を指定する必要があります。 コマンドレットを対話的に実行するときに推奨される使用方法はありません。  
  
たとえば、手動での入力を求めるパスワードを使用して、**Read-host**コマンドレットをセキュリティで保護された文字列をユーザーに確認します。  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> 前のオプションは、パスワードを確認しない、細心の注意を使用して、: パスワードは表示されません。  
  
これはお勧めはクリア テキストの変換済みの変数として、セキュリティで保護された文字列を提供できます。  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
最後に、ファイル、暗号化されたパスワードに格納され、クリア テキストのパスワードが表示されることがなく、後で再する可能性があります。 例えば：  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> テキストをクリアや暗号化されたパスワードの保存を提供または推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのドメイン コントローラーの DSRM パスワードを認識します。  その暗号化されたパスワードを取り消すファイルへのアクセスを持つユーザー可能性があります。 した情報を使って、DSRM で起動された DC にログオンし、最終的にドメイン コントローラー自体は、自分の権限を AD フォレストで最も高いレベルに昇格を偽装します。 追加の手順を使用してセット**System.Security.Cryptography**データはことをお勧めがスコープ外にテキスト ファイルを暗号化します。 パスワードの保存を絶対に避けることをお勧めします。  
  
### <a name="additional-options"></a>その他のオプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2AdditionalOptions.png)  
  
**追加オプション**] ページには、レプリケーション ソースとしてドメイン コントローラーに名前を付ける構成オプションまたは任意のドメイン コントローラーをレプリケーション ソースとして使用することができます。  
  
できますをドメイン コント ローラーを使用して、インストールするバックアップ メディア (IFM) オプションからインストールを使用してメディアを作成します。 **メディアからインストール**] チェック ボックスは、参照オプションが選択されているし] をクリックする必要があります**確認**指定されたパスが有効なメディアであることを確認します。 IFM オプションで使用されるメディアは Windows Server バックアップまたは Ntdsutil.exe 別既存 Windows Server 2012 コンピューターからのみ作成します。Windows Server 2008 R2 または以前のオペレーティング システムを使用して、Windows Server 2012 ドメイン コントローラーのメディアを作成することはできません。 IFM の変更の詳細については、次を参照してください。[Ntdsutil.exe インストール メディアの変更から](../../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)します。 SYSKEY で保護されているメディアを使用して場合、サーバー マネージャーは検証中にイメージのパスワードを要求します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_StagedIFM.png)  
  
**追加オプション**ADDSDeployment コマンドレット引数は。  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>パス  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Paths.png)  
  
**パス**および SYSVOL 共有のページでは、AD DS データベース、データベースのトランザクション ログの既定のフォルダーの場所を上書きすることができます。 既定の場所は、常に %systemroot% のサブディレクトリ内にします。 **パス**ADDSDeployment コマンドレット引数は。  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2ReviewOptions.png)  
  
**オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、お客様の要件を満たしていることを確認します。 これは、サーバー マネージャーを使用してインストールを中止する最後の機会ではありません。 単に、このページを使用すると、確認し、構成を続行する前に、設定を確認できます。 **オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。 このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。 例えば：  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "corp.contoso.com" `  
-LogPath "C:\Windows\NTDS" `  
-SYSVOLPath "C:\Windows\SYSVOL" `  
-UseExistingAccount:$true `  
-Norebootoncompletion:$false  
-Force:$true  
  
```  
  
> [!NOTE]  
> サーバー マネージャーは、一般にすべての引数と値のプロモーションおよび (サービス パックまたは Windows の将来のバージョン間で変わる可能性がある) のように既定の設定に依存しないときに入力します。 1 つの例外は、**-safemodeadministratorpassword**引数。 確認プロンプトがコマンドレットを対話的に実行されている場合、値を省略を強制的に  
  
オプションを使用して**Whatif**引数を使用、**Install-addsdomaincontroller**コマンドレットを構成情報を確認します。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示することができます。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2WhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件の確認  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2PrereqCheck.png)  
  
**前提条件のチェック**AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバーの構成が新しい AD DS フォレストをサポートできることを検証します。  
  
新しいフォレスト ルート ドメインをインストールする場合、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、一連のモジュラー テストをシリアル化されたを呼び出します。 これらのテストでは、推奨される修復のオプションを使用してアラートです。 必要なだけ何度でもテストを実行することができます。 すべての前提条件のテストまで、ドメイン コントローラーのインストール プロセスを続行できません渡します。  
  
**前提条件のチェック**以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかです。 前提条件チェックの詳細については、次を参照してください。[前提条件のチェック](../../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)します。  
  
バイパスすることはできません、**の前提条件チェック**ときは、サーバー マネージャーを使用して進むことができます、プロセスは次の引数を使用して、AD DS 展開コマンドレットを使用する場合。  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft は、部分的なドメイン コントローラーの昇格につながるまたは AD DS フォレストが破損している前提条件のチェックをスキップすることです。  
  
をクリックして**インストール**をドメイン コントローラーの昇格プロセスを開始します。 これは、インストールをキャンセルする最後の機会です。 開始されると、昇格プロセスをキャンセルすることはできません。 コンピューターは、昇格の結果に関係なく、昇格プロセスの終了時に自動的に再起動します。  
  
### <a name="installation"></a>インストール  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_Stage2Installation.png)  
  
[インストール] ページが表示されたら、ドメイン コントローラーの構成を開始、停止またはできませんキャンセルします。 操作の詳しい内容は、このページに表示され、ログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment モジュールを使用して新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```  
Install-addsdomaincontroller  
  
```  
  
参照してください[RODC の Windows PowerShell のアタッチ](../../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md#BKMK_AttachPS)必須およびオプションの引数。  
  
**Install-addsdomaincontroller**コマンドレットはだけです (前提条件のチェックとインストール) の 2 つのフェーズです。 以下の 2 つの図の最低限の必須引数を使用したインストール フェーズを表示する**- domainname**、**-useexistingaccount**、および**-credential**します。 注: 同様、サーバー マネージャー、**Install-addsdomaincontroller**昇格プロセスで、サーバーの再起動は自動的にされることを知らせます。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2.png)  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSStage2Complete.png)  
  
再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めします。 正常に機能するドメイン コントローラーを再起動しなければなりません。  
  
### <a name="results"></a>結果  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  
## <a name="rodc-without-staging-workflow"></a>ワークフローのステージングなしの RODC  
次の図は、以前に AD DS の役割をインストールして、Active Directory ドメイン サービス構成ウィザードを既存の Windows Server 2012 ドメインに新しい非段階的読み取り専用ドメイン コントローラーを作成するサーバー マネージャーを使用してを開始した場合に、Active Directory Domain Services 構成プロセスを示します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/adds_rodcdeploy.png)  
  
## <a name="rodc-without-staging-windows-powershell"></a>Windows PowerShell をステージングなしの RODC  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-Safemodeadministratorpassword*<br /><br />***-サイト名***<br /><br />*-ApplicationPartitionsToReplicate*<br /><br />*-CreateDNSDelegation*<br /><br />***資格情報***<br /><br />*-CriticalReplicationOnly*<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-DNSOnNetwork<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-Logpath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-AllowPasswordReplicationAccountName*<br /><br />*-DelegatedAdministratorAccountName*<br /><br />*-DenyPasswordReplicationAccountName*<br /><br />***-ReadOnlyReplica***|  
  
> [!NOTE]  
> **-Credential**引数は、のみために必要なかどうかは、既にログオンしていない、Domain Admins グループのメンバーとして。  
  
## <a name="rodc-without-staging-deployment"></a>展開のステージングなしの RODC  
  
### <a name="deployment-configuration"></a>展開の構成  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDeployConfig.png)  
  
サーバー マネージャーですべてのドメイン コントローラーの昇格を開始する、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。  
  
非段階的読み取り専用ドメイン コントローラーを既存の Windows Server 2012 ドメインに追加するには、選択**ドメイン コントローラーを既存のドメインに追加**] をクリックし、**選択**] ボタンをクリックして**このドメインのドメイン情報を指定**します。 サーバー マネージャーに自動的に求めるプロンプトが有効な資格情報、または] をクリックすることができます**変更**します。  
  
RODC をアタッチするには、Windows Server 2012 での Domain Admins グループのメンバーシップが必要です。 Active Directory ドメイン サービス構成ウィザードが表示されたら後で、現在の資格情報が適切なアクセス許可またはグループのメンバーシップがあるない場合。  
  
**展開構成**ADDSDeployment Windows PowerShell コマンドレットと引数は。  
  
```  
Install-AddsDomainController  
-domainname <string>   
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>ドメイン コント ローラー オプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCDCOptions.png)  
  
**ドメイン コントローラー オプション**] ページが新しいドメイン コントローラーのドメイン コントローラーの機能を指定します。 構成可能なドメイン コントローラーの機能は**DNS サーバー**、**グローバル カタログ**、および**読み取り専用ドメイン コントローラー**します。 マイクロソフトでは、すべてのドメイン コントローラが、分散環境での高可用性の DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択し、Start of Authority クエリに基づいて既にその Dc 上の DNS を現在のドメインのホストの場合は、DNS サーバーを既定で選択します。  
  
**ドメイン コント ローラー オプション**] ページでは、適切な Active Directory 論理を選択することもできます**サイト名**、フォレストの構成からです。 既定では、最も適切なサブネットのサイトを選択します。 1 つのサイトがある場合は、そのサイトを自動的に選択します。  
  
> [!IMPORTANT]  
> サーバーが Active Directory のサブネットに属していない複数の Active Directory サイトがある場合は、何も選択し、**[次へ]**ボタンは、一覧からサイトを選択するまでは利用できません。  
  
指定した**ディレクトリ サービス復元モード パスワード**サーバーに適用されるパスワード ポリシーに従う必要があります。 常に強力で複雑なパスワードまたは可能であれば、passphrase.The**ドメイン コントローラー オプション**ADDSDeployment Windows PowerShell 引数は。  
  
```  
-UseExistingAccount <{$true | $false}>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 引数として提供されると、サイト名は既に存在して**sitename**します。 **Install-addsdomaincontroller**コマンドレットは、サイト名を作成しません。 コマンドレットを使用する**新しい adreplicationsite**新しいサイトを作成します。  
  
**Install-addsdomaincontroller**引数が指定されていない場合はサーバー マネージャーと同じ既定値に従います。  
  
**SafeModeAdministratorPassword**引数の操作は特別な。  
  
-   場合*が指定されていない*を引数としてコマンドレットは、して、マスクされたパスワードの確認入力を求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
    たとえば、corp.contoso.com で新しい RODC を作成してなると、マスクされたパスワードの確認入力を求め。  
  
    ```  
    Install-ADDSDomainController -DomainName corp.contoso.com -credential (get-credential)  
    ```  
  
-   指定されている場合*値を持つ*、値が、セキュリティで保護された文字列を指定する必要があります。 コマンドレットを対話的に実行するときに推奨される使用方法はありません。  
  
たとえば、手動での入力を求めるパスワードを使用して、**Read-host**コマンドレットをセキュリティで保護された文字列をユーザーに確認します。  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
  
```  
  
> [!WARNING]  
> 前のオプションは、パスワードを確認しない、細心の注意を使用して、: パスワードは表示されません。  
  
これはお勧めはクリア テキストの変換済みの変数として、セキュリティで保護された文字列を提供できます。  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
```  
  
最後に、ファイル、暗号化されたパスワードに格納され、クリア テキストのパスワードが表示されることがなく、後で再する可能性があります。 例えば：  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> テキストをクリアや暗号化されたパスワードの保存を提供または推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのドメイン コントローラーの DSRM パスワードを認識します。  その暗号化されたパスワードを取り消すファイルへのアクセスを持つユーザー可能性があります。 した情報を使って、DSRM で起動された DC にログオンし、最終的にドメイン コントローラー自体は、自分の権限を AD フォレストで最も高いレベルに昇格を偽装します。 追加の手順を使用してセット**System.Security.Cryptography**データはことをお勧めがスコープ外にテキスト ファイルを暗号化します。 パスワードの保存を絶対に避けることをお勧めします。  
  
### <a name="rodc-options"></a>RODC オプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCOptions.png)  
  
**RODC オプション**] ページでは、設定を変更することができます。  
  
-   代理管理者アカウント  
  
-   アカウントのパスワードを RODC にレプリケートを許可します。  
  
-   アカウントのパスワードを RODC にレプリケートを拒否します。  
  
代理管理者のアカウントは、RODC に対するローカル管理者のアクセス許可を獲得します。 これらのユーザーは、ローカル コンピューターの Administrators グループと同等の権限で操作できます。  Domain Admins グループまたはドメインのビルトインの Administrators グループのメンバーではありません。 このオプションは、ドメイン管理者のアクセス許可を与えることがなく支社の管理を委任するのに便利です。 管理の委任を構成する必要はありません。  
  
それと同等の ADDSDeployment Windows PowerShell 引数です。  
  
```  
-delegatedadministratoraccountname <string>  
```  
  
RODC のパスワードをキャッシュすることはできませんとできません接続し、アカウント、書き込み可能なドメイン コントローラーへの認証は、リソースまたは Active Directory によって提供される機能にアクセスできません。  
  
> [!IMPORTANT]  
> 変更しない場合、既定のグループと設定が使用されます。  
>   
> -   管理者を拒否します。  
> -   Server Operators を拒否します。  
> -   バックアップ オペレーターの拒否  
> -   アカウントの演算子の拒否  
> -   拒否 RODC Password Replication Group - が拒否されました  
> -   RODC Password Replication Group - 許可を許可します。  
  
それと同等の ADDSDeployment Windows PowerShell 引数は次のとおりです。  
  
```  
-allowpasswordreplicationaccountname <string []>  
-denypasswordreplicationaccountname <string []>  
```  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_SelectDelAdmin.png)  
  
### <a name="additional-options"></a>その他のオプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCAdditionalOptions.png)  
  
**追加オプション**] ページには、レプリケーション ソースとしてドメイン コントローラーに名前を付ける構成オプションまたは任意のドメイン コントローラーをレプリケーション ソースとして使用することができます。  
  
できますをドメイン コント ローラーを使用して、インストールするバックアップ メディア (IFM) オプションからインストールを使用してメディアを作成します。 **メディアからインストール**] チェック ボックスは、参照オプションが選択されているし] をクリックする必要があります**確認**指定されたパスが有効なメディアであることを確認します。 IFM オプションで使用されるメディアは Windows Server バックアップまたは Ntdsutil.exe 別既存 Windows Server 2012 コンピューターからのみ作成します。Windows Server 2008 R2 または以前のオペレーティング システムを使用して、Windows Server 2012 ドメイン コントローラーのメディアを作成することはできません。  付録では、IFM の変更の説明を示します。 SYSKEY で保護されているメディアを使用して場合、サーバー マネージャーは検証中にイメージのパスワードを要求します。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSIFM.png)  
  
その他のオプションの ADDSDeployment コマンドレット引数は、次のとおりです。  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-systemkey <secure string>  
```  
  
### <a name="paths"></a>パス  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPaths.png)  
  
**パス**および SYSVOL 共有のページでは、AD DS データベース、データベースのトランザクション ログの既定のフォルダーの場所を上書きすることができます。 既定の場所は、常に %systemroot% のサブディレクトリ内にします。 **パス**ADDSDeployment コマンドレット引数は。  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>準備オプション  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrepOptions.png)  
  
**準備オプション**ページは、AD DS 構成には、(forestprep) スキーマを拡張して、ドメイン (domainprep) の更新が含まれているを通知します。 フォレストまたはドメインが準備されていない以前の Windows Server 2012 ドメイン コントローラー インストールまたは手動で Adprep.exe を実行時にのみこのページを表示します。 たとえば、Active Directory ドメイン サービス構成ウィザードは、既存の Windows Server 2012 フォレスト ルート ドメインを新しいレプリカ ドメイン コントローラーを追加した場合、このページを抑制します。  
  
クリックすると、スキーマを拡張して、ドメインの更新が発生しない**次**します。 これらのイベントは、インストール フェーズ中にのみ発生します。 このページには、インストール後に発生するイベントについて通知だけが表示されます。  
  
このページにスキーマを拡張またはドメインを準備するこれらのグループのメンバーシップが必要なに現在のユーザー資格情報は Schema Admin と Enterprise Admins グループのメンバーあるがも検証します。 をクリックして**変更**ページは、現在の資格情報は、十分なアクセス許可を提供しないことを通知する場合は、適切なユーザー資格情報を提供します。  
  
その他のオプションの ADDSDeployment コマンドレット引数です。  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> として、Windows Server の以前のバージョンと Windows Server 2012 の自動ドメイン準備は GPPREP は実行されません。 実行**adprep.exe/gpprep**に準備されていない Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 のすべてのドメインを手動でします。 アップグレードのたびに、ドメインの履歴に GPPrep 1 回だけを実行する必要があります。 Adprep.exe を実行しない /gpprep の操作で原因になるすべてのファイルとフォルダー、SYSVOL フォルダーをすべてのドメイン コントローラ上で再レプリケートために自動的にします。  
>   
> ドメイン内の最初の非段階的 RODC を昇格したときに、自動 RODCPrep が実行されます。 最初の書き込み可能な Windows Server 2012 ドメイン コントローラーを昇格したときに発生しません。 手動で実行することができます**adprep.exe/rodcprep**読み取り専用ドメイン コントローラーを展開する予定の場合。  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCReviewOptions.png)  
  
**オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、お客様の要件を満たしていることを確認します。 これは、サーバー マネージャーを使用してインストールを中止する最後の機会ではありません。 単に、このページを使用すると、確認し、構成を続行する前に、設定を確認できます。  
  
**オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。 このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。 例えば：  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-AllowPasswordReplicationAccountName @("CORP\Allowed RODC Password Replication Group", "CORP\Chicago RODC Admins", "CORP\Chicago RODC Users and Computers") `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DelegatedAdministratorAccountName "CORP\Chicago RODC Admins" `  
-DenyPasswordReplicationAccountName @("BUILTIN\Administrators", "BUILTIN\Server Operators", "BUILTIN\Backup Operators", "BUILTIN\Account Operators", "CORP\Denied RODC Password Replication Group") `  
-DomainName "corp.contoso.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-ReadOnlyReplica:$true `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> サーバー マネージャーは、一般にすべての引数と値のプロモーションおよび (サービス パックまたは Windows の将来のバージョン間で変わる可能性がある) のように既定の設定に依存しないときに入力します。 1 つの例外は、**-safemodeadministratorpassword**引数。 確認プロンプトを強制するには、コマンドレットを対話的に実行するときに値を省略します。  
  
Install-ADDSDomainController コマンドレットで省略可能な-whatif 引数が指定を使用して、構成情報を確認します。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示することができます。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCWhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件の確認  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCPrereqCheck.png)  
  
**前提条件のチェック**AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバーの構成が新しい AD DS フォレストをサポートできることを検証します。  
  
新しいフォレスト ルート ドメインをインストールする場合、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、一連のモジュラー テストをシリアル化されたを呼び出します。 これらのテストでは、推奨される修復のオプションを使用してアラートです。 必要なだけ何度でもテストを実行することができます。 すべての前提条件のテストまで、ドメイン コントローラーのプロセスを続行できません渡します。  
  
**前提条件のチェック**以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかです。  
  
バイパスすることはできません、**の前提条件チェック**ときは、サーバー マネージャーを使用して進むことができます、プロセスは次の引数を使用して、AD DS 展開コマンドレットを使用する場合。  
  
```  
-skipprechecks  
  
```  
  
をクリックして**インストール**をドメイン コントローラーの昇格プロセスを開始します。 これは、インストールをキャンセルする最後の機会です。 開始されると、昇格プロセスをキャンセルすることはできません。 コンピューターは、昇格の結果に関係なく、昇格プロセスの終了時に自動的に再起動します。  
  
### <a name="installation"></a>インストール  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCInstallation.png)  
  
ときに、**インストール**ページが表示されます、ドメイン コントローラーの構成を開始、停止またはできません取り消されます。 操作の詳しい内容は、このページに表示され、ログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment モジュールを使用して新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```  
Install-addsdomaincontroller  
  
```  
  
参照してください、**ADDSDeployment コマンドレット**必須およびオプションの引数は、このセクションの最初にある表。  
  
**Install-addsdomaincontroller**コマンドレットはだけです (前提条件のチェックとインストール) の 2 つのフェーズです。 以下の 2 つの図の最低限の必須引数を使用したインストール フェーズを表示する**- domainname**、**- readonlyreplica**、**sitename**、および**-credential**します。 注: 同様、サーバー マネージャー、**Install-addsdomaincontroller**昇格プロセスで、サーバーの再起動は自動的にされることを知らせます。  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODC.png)  
  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_PSInstallRODCProgress.png)  
  
再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めしません。 正常に機能するドメイン コントローラーを再起動しなければなりません。 ドメイン コントローラーからログオフした場合をログオンできませんバック対話的に再起動するまで。  
  
### <a name="results"></a>結果  
![RODC をインストールします。](media/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-/ADDS_SMI_TR_RODCSignoff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  

