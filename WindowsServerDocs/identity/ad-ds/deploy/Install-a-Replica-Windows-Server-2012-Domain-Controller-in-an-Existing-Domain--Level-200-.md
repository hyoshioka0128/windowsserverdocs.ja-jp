---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: "レプリカ Windows Server 2012 ドメイン コントローラーを既存のドメイン (レベル 200) のインストールします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e3151a8beee2870ecc747a64241df9d562ad4cc2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>レプリカ Windows Server 2012 ドメイン コントローラーを既存のドメイン (レベル 200) のインストールします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して、Windows Server 2012 への既存のフォレストまたはドメインのアップグレードに必要な手順について説明します。 既存のドメインに Windows Server 2012 を実行するドメイン コントローラーを追加する方法について説明します。  
  
-   [アップグレードとレプリカのワークフロー](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [アップグレードとレプリカの Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [展開](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="BKMK_Workflow"></a>アップグレードとレプリカのワークフロー  
次の図は、以前に AD DS の役割をインストールして、Active Directory ドメイン サービス構成ウィザードを既存のドメインに新しいドメイン コントローラーを作成するサーバー マネージャーを使用してを開始した場合に、Active Directory Domain Services 構成プロセスを示します。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="BKMK_PS"></a>アップグレードとレプリカの Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-Safemodeadministratorpassword*<br /><br />*-サイト名*<br /><br />*-ADPrepCredential*<br /><br />-ApplicationPartitionsToReplicate<br /><br />*-AllowDomainControllerReinstall*<br /><br />-確認します。<br /><br />*-CreateDNSDelegation*<br /><br />***資格情報***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />フォース<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-Logpath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />-NoDnsOnNetwork<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />-サイト名<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-Useexistingaccount*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-Credential**引数は、のみために必要なかどうかは、既にログオンしていない (フォレストをアップグレードしている) 場合は、[Enterprise Admins および Schema Admins グループまたは Domain Admins グループのメンバーとして (既存のドメインを新しい DC に追加する) 場合。  
  
## <a name="BKMK_Dep"></a>展開  
  
### <a name="deployment-configuration"></a>展開の構成  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
サーバー マネージャーですべてのドメイン コントローラーの昇格を開始する、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。  
  
既存のフォレストをアップグレードするか、既存のドメインに書き込み可能なドメイン コントローラーを追加する] をクリックして**ドメイン コントローラーを既存のドメインに追加**] をクリック**選択**に**このドメインのドメイン情報を指定**します。 サーバー マネージャーの入力を要求有効な資格情報が必要な場合です。  
  
フォレストをアップグレードするには、Windows Server 2012 での Enterprise Admins および Schema Admins の両方のグループのグループ メンバーシップを含む資格情報が必要です。 Active Directory ドメイン サービス構成ウィザードが表示されたら後で、現在の資格情報が適切なアクセス許可またはグループのメンバーシップがあるない場合。  
  
自動 Adprep プロセスは、既存の Windows Server 2012 ドメインとドメインのドメイン コントローラーが以前のバージョンの Windows Server を実行するドメイン コントローラーを追加する間のみ運用差です。  
  
展開構成の ADDSDeployment コマンドレットと引数は。  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
後で、個別の前提条件チェックを繰り返す一部の各ページで、特定のテストを実行します。 たとえば、選択したドメインが最低限の機能レベルを満たしていない場合を調べるには、前提条件の確認に昇格まで移動する必要はありません。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>ドメイン コント ローラー オプション  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
**ドメイン コントローラー オプション**] ページが新しいドメイン コントローラーのドメイン コントローラーの機能を指定します。 構成可能なドメイン コントローラーの機能は**DNS サーバー**、**グローバル カタログ**、および**読み取り専用ドメイン コントローラー**します。 マイクロソフトでは、すべてのドメイン コントローラが、分散環境での高可用性の DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択し、Start of Authority クエリに基づいて既にその Dc 上の DNS を現在のドメインのホストの場合は、DNS サーバーを既定で選択します。 **ドメイン コント ローラー オプション**] ページでは、適切な Active Directory 論理を選択することもできます**サイト名**、フォレストの構成からです。 既定では、最も適切なサブネットのサイトを選択します。 1 つのサイトがある場合に自動的にその選択されます。  
  
> [!NOTE]  
> サーバーが Active Directory のサブネットに属していない複数の Active Directory サイトがある場合は、何も選択し、**[次へ]**ボタンは、一覧からサイトを選択するまでは利用できません。  
  
指定した**ディレクトリ サービス復元モード パスワード**サーバーに適用されるパスワード ポリシーに従う必要があります。 常に強力で複雑なパスワードまたは可能であれば、パスフレーズを選択します。  
  
**ドメイン コントローラー オプション**ADDSDeployment 引数は。  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> 引数として提供されると、サイト名は既に存在して**sitename**します。 **Install-addsdomaincontroller**コマンドレットは、サイトを作成しません。 コマンドレットを使用する**新しい adreplicationsite**新しいサイトを作成します。  
  
**SafeModeAdministratorPassword**引数の操作は特別な。  
  
-   場合*が指定されていない*を引数としてコマンドレットは、して、マスクされたパスワードの確認入力を求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
    たとえば、treyresearch.net ドメインに追加のドメイン コントローラーを作成して、マスクされたパスワードの確認入力を求め。  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
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
> テキストをクリアや暗号化されたパスワードの保存を提供または推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのドメイン コントローラーの DSRM パスワードを認識します。  その暗号化されたパスワードを取り消すファイルへのアクセスを持つユーザー可能性があります。 した情報を使って、DSRM で起動された DC にログオンし、最終的にドメイン コントローラー自体は、自分の権限を Active Directory フォレストで最も高いレベルに昇格を偽装します。 追加の手順を使用してセット**System.Security.Cryptography**データはことをお勧めがスコープ外にテキスト ファイルを暗号化します。 パスワードの保存を絶対に避けることをお勧めします。  
  
ADDSDeployment コマンドレットは、DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップする追加のオプションを提供します。 サーバー マネージャーを使用する場合、この構成オプションをスキップすることはできません。 この引数が重要なは、ドメイン コントローラーを構成する前に、DNS サーバーの役割をインストールした場合にのみ。  
  
```  
-SkipAutoConfigureDNS  
```  
  
**ドメイン コントローラー オプション**] ページで、既存のドメイン コントローラーが Windows Server 2003 を実行している場合は、読み取り専用ドメイン コントローラーを作成できません警告が表示されます。 これと、警告を無視することができます。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
**DNS オプション**] ページでは、選択した場合、DNS 委任を構成することができます、**DNS サーバー** ] オプションを選択、*ドメイン コントローラー オプション*ページ DNS 委任が許可されているゾーンにポイントしている場合。 メンバーであるユーザーの代替の資格情報を提供する必要があります、**DNS Admins**グループ。  
  
**DNS オプション**ADDSDeployment コマンドレット引数は。  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
For more information about whether you need to create a DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx).  
  
### <a name="additional-options"></a>その他のオプション  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
**追加オプション**] ページには、構成オプションとして、レプリケーション ソース ドメイン コントローラーに名前を付けるか、レプリケーション ソースとして任意のドメイン コントローラーを使用することができます。  
  
できますをドメイン コント ローラーを使用して、インストールするバックアップ メディア (IFM) オプションからインストールを使用してメディアを作成します。 **メディアからインストール**] チェック ボックスは、参照オプションが選択されているし] をクリックする必要があります**確認**指定されたパスが有効なメディアであることを確認します。 IFM オプションで使用されるメディアは Windows Server バックアップまたは Ntdsutil.exe 別既存 Windows Server 2012 コンピューターからのみ作成します。Windows Server 2008 R2 または以前のオペレーティング システムを使用して、Windows Server 2012 ドメイン コントローラーのメディアを作成することはできません。 IFM の変更の詳細については、次を参照してください。[簡略化された管理付録](../../ad-ds/deploy/Simplified-Administration-Appendix.md)します。 SYSKEY で保護されているメディアを使用して場合、サーバー マネージャーは検証中にイメージのパスワードを要求します。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
**追加オプション**ADDSDeployment コマンドレット引数は。  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>パス  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**パス**および SYSVOL 共有のページでは、AD DS データベース、データベースのトランザクション ログの既定のフォルダーの場所を上書きすることができます。 既定の場所は、常に %systemroot% のサブディレクトリ内にします。  
  
Active Directory Paths ADDSDeployment コマンドレット引数は、次のとおりです。  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>準備オプション  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
**準備オプション**ページは、AD DS 構成には、(forestprep) スキーマを拡張して、ドメイン (domainprep) の更新が含まれているを通知します。  のみ、フォレストとドメインで以前の Windows Server 2012 ドメイン コントローラーのインストールまたは手動で Adprep.exe を実行には準備されていない場合は、このページを表示します。 たとえば、Active Directory ドメイン サービス構成ウィザードでは、新しいドメイン コントローラーを既存の Windows Server 2012 フォレスト ルート ドメインに追加する場合にこのページが表示されません。  
  
クリックすると、スキーマを拡張して、ドメインの更新が発生しない**次**します。 これらのイベントは、インストール フェーズ中にのみ発生します。 このページには、インストール後に発生するイベントについて通知だけが表示されます。  
  
このページにスキーマを拡張またはドメインを準備するこれらのグループのメンバーシップが必要なに現在のユーザー資格情報は Schema Admin と Enterprise Admins グループのメンバーあるがも検証します。 をクリックして**変更**ページは、現在の資格情報は、十分なアクセス許可を提供しないことを通知する場合は、適切なユーザー資格情報を提供します。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
その他のオプションの ADDSDeployment コマンドレット引数です。  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> として、Windows Server の以前のバージョンと Windows Server 2012 を実行するドメイン コントローラーの自動ドメイン準備は GPPREP は実行されません。 実行**adprep.exe/gpprep**に準備されていない Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 のすべてのドメインを手動でします。 アップグレードのたびに、ドメインの履歴に GPPrep 1 回だけを実行する必要があります。 Adprep.exe を実行しない /gpprep の操作で原因になるすべてのファイルとフォルダー、SYSVOL フォルダーをすべてのドメイン コントローラ上で再レプリケートために自動的にします。  
>   
> ドメイン内の最初の非段階的 RODC を昇格したときに、自動 RODCPrep が実行されます。 最初の書き込み可能な Windows Server 2012 ドメイン コントローラーを昇格したときに発生しません。 手動でも実行できます**adprep.exe/rodcprep**読み取り専用ドメイン コントローラーを展開する予定の場合。  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
**オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、お客様の要件を満たしていることを確認します。 これは、サーバー マネージャーを使用してインストールを中止する最後の機会ではありません。 単に、このページを使用すると、確認し、構成を続行する前に、設定を確認できます。  
  
**オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。  このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。  
  
例えば：  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
Import-Module ADDSDeployment  
Install-ADDSDomainController `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-CriticalReplicationOnly:$false `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainName "root.fabrikam.com" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> サーバー マネージャーは、一般にすべての引数と値のプロモーションおよび (サービス パックまたは Windows の将来のバージョン間で変わる可能性がある) のように既定の設定に依存しないときに入力します。 1 つの例外は、**-safemodeadministratorpassword**引数。 確認プロンプトがコマンドレットを対話的に実行されている場合、値を省略を強制的に  
>   
> オプションを使用して**Whatif**引数を使用、**Install-addsdomaincontroller**コマンドレットを構成情報を確認します。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示することができます。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件の確認  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
**前提条件のチェック**AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、ドメインとフォレストが新しい Windows Server 2012 ドメイン コントローラーをサポートできることを検証します。  
  
新しいドメイン コントローラーをインストールする場合、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、一連のモジュラー テストをシリアル化されたを呼び出します。 これらのテストでは、推奨される修復のオプションを使用してアラートです。 必要なだけ何度でもテストを実行することができます。 すべての前提条件のテストまで、ドメイン コントローラーのプロセスを続行できません渡します。  
  
**前提条件のチェック**以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかです。  
  
具体的な前提条件チェックの詳細については、次を参照してください。[前提条件のチェック](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)します。  
  
バイパスすることはできません、**の前提条件チェック**ときは、サーバー マネージャーを使用して進むことができます、プロセスは次の引数を使用して、AD DS 展開コマンドレットを使用する場合。  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> Microsoft は、部分的なドメイン コントローラーの昇格につながるまたは AD DS フォレストが破損している前提条件のチェックをスキップすることです。  
  
をクリックして**インストール**をドメイン コントローラーの昇格プロセスを開始します。 これは、インストールをキャンセルする最後の機会です。 開始されると、昇格プロセスをキャンセルすることはできません。 コンピューターが自動的に再起動プロモーション results.The**前提条件のチェック**] ページで、問題を解決するためのガイダンスとプロセス中に発生したが表示されます。  
  
### <a name="installation"></a>インストール  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
ときに、**インストール**ページが表示されます、ドメイン コントローラーの構成を開始、停止またはできません取り消されます。 操作の詳しい内容は、このページに表示され、ログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log (サーバーがワークグループ内にある場合)  
  
ADDSDeployment モジュールを使用して新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```  
Install-addsdomaincontroller  
```  
  
参照してください[アップグレードとレプリカの Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)必須およびオプションの引数。  
  
**Install-addsdomaincontroller**コマンドレットはだけです (前提条件のチェックとインストール) の 2 つのフェーズです。 以下の 2 つの図の最低限の必須引数を使用したインストール フェーズを表示する**- domainname**と**-credential**します。 最初の Windows Server 2012 ドメイン コントローラーを既存の Windows Server 2003 フォレストに追加の一環として Adprep 操作がどのように自動的には注意してください。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
注: 同様、サーバー マネージャー、**Install-addsdomaincontroller**昇格プロセスで、サーバーの再起動は自動的にされることを知らせます。 再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めします。 正常に機能するドメイン コントローラーを再起動しなければなりません。  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
Windows PowerShell を使用してリモートでドメイン コントローラーを構成するのには、ラップ、**インストール adddomaincontroller**コマンドレット*内部*の**呼び出すコマンド**コマンドレット。 これは、中かっこを使用する必要があります。  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
例えば：  
  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> インストールと Adprep プロセスの動作の詳細については、次を参照してください。、[ドメイン コントローラーの展開のトラブルシューティング](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)します。  
  
### <a name="results"></a>結果  
![レプリカをインストールします。](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 成功した場合、ドメイン コントローラーは 10 秒後に自動的に再起動します。  
  
Windows Server の以前のバージョンと Windows server 2012 を実行するドメイン コントローラーの自動ドメイン準備で GPPREP は実行されません。 実行**adprep.exe/gpprep**に準備されていない Windows Server 2003、Windows Server 2008、または Windows Server 2008 R2 のすべてのドメインを手動でします。 アップグレードのたびに、ドメインの履歴に GPPrep 1 回だけを実行する必要があります。 Adprep.exe を実行しない /gpprep の操作で原因になるすべてのファイルとフォルダー、SYSVOL フォルダーをすべてのドメイン コントローラ上で再レプリケートために自動的にします。  
  

