---
ms.assetid: e6da5984-d99d-4c34-9c11-4a18cd413f06
title: Windows Server 2012 のレプリカ ドメイン コントローラーを既存のドメインにインストールする (レベル 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5e72c18d3aa49774cf73d5365748e7bf20764b22
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390838"
---
# <a name="install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain-level-200"></a>Windows Server 2012 のレプリカ ドメイン コントローラーを既存のドメインにインストールする (レベル 200)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して、既存のフォレスト ドメインを Windows Server 2012 にアップグレードするための手順について説明します。 また Windows Server 2012 を実行するドメイン コントローラーを既存のドメインに追加する方法を説明します。  
  
-   [アップグレードとレプリカのワークフロー](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [アップグレードとレプリカの Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS)  
  
-   [展開](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_Dep)  
  
## <a name="BKMK_Workflow"></a>アップグレードとレプリカのワークフロー  
以下の図に、既に AD DS 役割をインストール済みで、既存のドメイン内に新しいドメイン コントローラーを作成するためにサーバー マネージャーを使用して Active Directory ドメイン サービス構成ウィザードを開始した場合の、Active Directory ドメイン サービスの構成プロセスを示します。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/adds_forestupgrade.png)  
  
## <a name="BKMK_PS"></a>アップグレードとレプリカの Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字** の引数は必須です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。)|  
|Install-AddsDomainController|-SkipPreChecks<br /><br />***-DomainName***<br /><br />*-SafeModeAdministratorPassword*<br /><br />*-SiteName*<br /><br />*-ADPrepCredential*<br /><br />-ApplicationPartitionsToReplicate<br /><br />*-Allowdomainコントローラーの再インストール*<br /><br />-Confirm<br /><br />*-CreateDNSDelegation*<br /><br />***-Credential***<br /><br />-CriticalReplicationOnly<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-Force<br /><br />*-InstallationMediaPath*<br /><br />*-InstallDNS*<br /><br />*-LogPath*<br /><br />-MoveInfrastructureOperationMasterRoleIfNecessary<br /><br />-NoDnsOnNetwork<br /><br />*-NoGlobalCatalog*<br /><br />-Norebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />-SkipAutoConfigureDNS<br /><br />-SiteName<br /><br />*-SystemKey*<br /><br />*-SYSVOLPath*<br /><br />*-UseExistingAccount*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-credential** 引数は、フォレストをアップグレードする場合は、Enterprise Admins および Schema Admins グループのメンバーとしてログインしていない場合のみ必須です。新しい DC を既存のドメインに追加する場合は、Domain Admins グループのメンバーとしてログインしていない場合のみ必須です。  
  
## <a name="BKMK_Dep"></a>ディストリビューション  
  
### <a name="deployment-configuration"></a>展開構成  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDeployConfig.png)  
  
サーバー マネージャーは各ドメイン コントローラーの昇格を **[配置構成]** ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。  
  
既存のフォレストをアップグレードする、または既存のドメインに書き込み可能なドメイン コントローラーを追加するには、 **[既存のドメインにドメイン コントローラーを追加する]** をクリックし、 **[選択]** をクリックして **[このドメインのドメイン情報を指定する]** に進みます。 必要な場合、サーバー マネージャーでは有効な資格情報の入力を求められます。  
  
フォレストをアップグレードするには、Windows Server 2012 の Enterprise Admins および Schema Admins グループのメンバーシップを含む資格情報が必要です。 現在の資格情報に適切なアクセス許可またはグループ メンバーシップがない場合、Active Directory Domain Services 構成ウィザードでは後で入力を求められます。  
  
ドメイン コントローラーの追加先が既存の Windows Server 2012 ドメインである場合と、ドメイン コントローラーが以前のバージョンの Windows Server を実行しているドメインである場合では、操作の違いは自動 Adprep プロセスのみです。  
  
展開構成の ADDSDeployment コマンドレットと引数は以下のとおりです  
  
```  
Install-AddsDomainController  
-domainname <string>  
-credential <pscredential>  
```  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeSelectDomain.png)  
  
各ページで特定のテストが実行されます。その内いくつかは、個別の前提条件チェックとして後でまた実行されます。 たとえば、選択したドメインが最低限の機能レベルを満たしていない場合、前提条件のチェック段階まで、昇格のすべてのプロセスをさかのぼる必要はありません。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeFFLError.png)  
  
### <a name="domain-controller-options"></a>ドメイン コントローラー オプション  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptions.png)  
  
**[ドメイン コントローラー オプション]** ページでは、新しいドメイン コントローラーのドメイン コントローラー機能を指定します。 構成可能なドメイン コントローラー機能は、 **[DNS サーバー]** 、 **[グローバル カタログ]** 、 **[読み取り専用ドメイン コントローラー]** です。 Microsoft では、分散環境で高可用性を実現するため、すべてのドメイン コントローラーで、DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択されます。DNS サーバーは、現在のドメインが、Start of Authority クエリに基づいて既にその DC 上にある DNS をホストする場合に、既定で選択されます。 **[ドメイン コントローラー オプション]** ページでは、フォレストの構成から適切な Active Directory 論理**サイト名**を選択することもできます。 既定では、最も適切なサブネットのサイトが選択されます。 サイトが 1 つしかない場合は、それが自動的に選択されます。  
  
> [!NOTE]  
> サーバーが Active Directory サブネットに属せず、複数の Active Directory サイトが存在する場合は、何も選択されず、リストからサイトを選択するまでは **[次へ]** ボタンが使用できません。  
  
**[ディレクトリ サービスの復元モード パスワード]** には、サーバーに適用されるパスワード ポリシーに従ったパスワードを指定する必要があります。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。  
  
**[ドメイン コントローラー オプション]** の ADDSDeployment 引数は以下のとおりです  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-sitename <string>  
-SafeModeAdministratorPassword <secure string>  
```  
  
> [!IMPORTANT]  
> **-sitename** に引数として指定するサイト名は既に存在している必要があります。 **install-AddsDomainController** コマンドレットはサイトを作成しません。 新しいサイトを作成するには **new-adreplicationsite** コマンドレットを使用します。  
  
**SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります。  
  
-   この引数を*指定しない*場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。  
  
    たとえば、treyresearch.net ドメイン内に追加のドメイン コントローラーを作成し、マスクされたパスワードの入力と確認入力を求められるようにするには、以下のように実行します  
  
    ```  
    Install-ADDSDomainController "DomainName treyresearch.net "credential (get-credential)  
    ```  
  
-   この引数を *値と共に*指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。  
  
たとえば、**Read-Host** コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。  
  
```  
-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring)  
```  
  
> [!WARNING]  
> この方法ではパスワードの確認入力が行われないため、細心の注意が必要です。パスワードは表示されません。  
  
セキュリティで保護された文字列は、変換されるクリア テキストの変数として指定することもできますが、これはお勧めしません。  
  
```  
-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force)  
  
```  
  
最後に、暗号化したパスワードをファイルに保存して後で使用することができます。こうするとクリア テキストのパスワードを表示せずに済みます。 以下に例を示します。  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> クリア テキストや暗号化されたテキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。  そのファイルにアクセスできる人はだれでも、暗号化されたパスワードを元に戻すことができます。 そのパスワードがわかれば、DSRM で起動された DC にログオンし、最終的にドメイン コントローラーそのものを偽装して、自分の権限を Active Directory フォレストで最も高いレベルに昇格させることができます。 テキスト ファイル データを暗号化するための **System.Security.Cryptography** の一連の使用手順を読むことが推奨されますが、ここでは取り上げません。 ベスト プラクティスは、パスワードの保存を絶対に避けることです。  
  
ADDSDeployment コマンドレットには、DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップする追加オプションがあります。 サーバー マネージャーを使用しているときは、この構成オプションをスキップできません。 この引数が重要なのは、ドメイン コントローラーを構成する前に DNS サーバーの役割をインストールした場合だけです。  
  
```  
-SkipAutoConfigureDNS  
```  
  
**[ドメイン コントローラー オプション]** ページで、既存のドメイン コントローラーが Windows Server 2003 を実行している場合は読み取り専用のドメイン コントローラーを作成できないことが通知されます。 これは予期される反応です。この警告は無視して問題ありません。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDCOptionsError.png)  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeDNSOptions.png)  
  
**[ドメイン コントローラー オプション]** ページで **[DNS サーバー]** オプションを選択し、DNS 委任が許可されるゾーンをポイントしている場合は、[ *DNS オプション* ] ページで、DNS 委任を構成することができます。 **DNS Admins** グループのメンバーである別のユーザーの資格情報を指定しなければならないことがあります。  
  
**[DNS オプション]** の ADDSDeployment コマンドレット引数は以下のとおりです。  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeCreds.png)  
  
DNS 委任を作成する必要があるかどうかの詳細については、「 [ゾーンの委任とは](https://technet.microsoft.com/library/cc771640.aspx)」を参照してください。  
  
### <a name="additional-options"></a>追加オプション  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeAdditionalOptions.png)  
  
**[追加オプション]** ページには、レプリケーション ソースとして特定のドメイン コントローラーを指定するか、またはどのドメイン コントローラーでもレプリケーション ソースとして使用できるかを指定する構成オプションがあります。  
  
また、メディアからのインストール (IFM) オプションを使用して、バックアップされているメディアからドメイン コントローラーをインストールすることもできます。 **[メディアからのインストール]** チェック ボックスをオンにすると参照オプションが表示されます。指定したパスが有効なメディアであることを示すため **[検証]** をクリックする必要があります。 IFM オプションで使用するメディアは、Windows Server バックアップまたは Ntdsutil.exe を使用して、既存の別の Windows Server 2012 コンピューターからのみ作成します。Windows Server 2008 R2 以前のオペレーティング システムを使用して Windows Server 2012 のドメイン コントローラー用のメディアを作成することはできません。 IFM の変更の詳細については、「 [Simplified Administration Appendix](../../ad-ds/deploy/Simplified-Administration-Appendix.md)」を参照してください。 SYSKEY で保護されているメディアを使用する場合、サーバー マネージャーは確認の間にイメージのパスワードの入力を求めます。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_NtdsutilIFM.png)  
  
**[追加オプション]** の ADDSDeployment コマンドレット引数は以下のとおりです。  
  
```  
-replicationsourcedc <string>  
-installationmediapath <string>  
-syskey <secure string>  
```  
  
### <a name="paths"></a>パス  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所を上書きできます。 既定の場所は常に %systemroot% のサブディレクトリです。  
  
Active Directory Paths ADDSDeployment コマンドレット引数は以下のとおりです  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="preparation-options"></a>準備オプション  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptions.png)  
  
**[準備オプション]** ページでは、AD DS 構成に、スキーマの拡張 (forestprep) とドメインの更新 (domainprep) が含まれることが通知されます。  このページは、フォレストとドメインが、以前の Windows Server 2012 ドメイン コントローラー インストールまたは手動で実行された Adprep.exe で準備されていない場合のみ表示されます。 たとえば、既存の Windows Server 2012 フォレストのルート ドメインに新しいドメイン コントローラーを追加した場合は、Active Directory ドメイン サービス構成ウィザードにこのページが表示されません。  
  
**[次へ]** をクリックしても、スキーマの拡張やドメインの更新は実行されません。 これらのイベントは、インストール フェーズでのみ発生します。 このページの目的は、インストール中の後の段階で発生するイベントについて通知することだけです。  
  
このページでは、現在のユーザーの資格情報が Schema Admin と Enterprise Admins グループのメンバーであるかどうかも確認します。これは、ドメイン準備のためにスキーマを拡張するにはこれらのグループのメンバーシップが必要であるためです。 現在の資格情報に十分なアクセス権がないと表示された場合は、 **[変更]** をクリックして適切なユーザー資格情報を指定してください。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrepOptionsCreds.png)  
  
[追加オプション] の ADDSDeployment コマンドレットの引数は以下のとおりです。  
  
```  
-adprepcredential <pscredential>  
```  
  
> [!IMPORTANT]  
> 以前のバージョンの Windows Server と同様、Windows Server 2012 を実行するドメイン コントローラーの自動ドメイン準備では GPPREP は実行されません。 Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 用に準備されていないすべてのドメインに対して、**adprep.exe /gpprep** を手動で実行してください。 特定のドメインに対して 1 度だけ (アップグレードのたびにではなく) GPPrep を実行する必要があります。 Adprep.exe は /gpprep を自動的に実行しません。これは、その操作により SYSVOL フォルダー内のすべてのファイルとフォルダーがすべてのドメイン コントローラー上で再レプリケートされる可能性があるためです。  
>   
> 自動 RODCPrep は、ドメイン内で最初の非段階的 RODC を昇格したときに実行されます。 最初の書き込み可能な Windows Server 2012 ドメイン コントローラーを昇格したときには実行されません。 読み取り専用ドメイン コントローラーを展開する予定がある場合は、手動で **adprep.exe /rodcprep** を実行することもできます。  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeReviewOptions.png)  
  
**[オプションの確認]** ページでは、インストールを開始する前に、設定を検証し、設定が要件を満たしていることを確認できます。 これがサーバー マネージャーを使用するインストールを停止する最後の機会ではありません。 このページでは、構成を続行する前に設定を検討して確認することだけができます。  
  
サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。  これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。  
  
以下に例を示します。  
  
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
> サーバー マネージャーでは通常、昇格時にすべての引数とその値を入力し、既定値に依存しません (既定値は将来のバージョンの Windows 間またはサービス パック間で変わる可能性があるため)。 唯一の例外は、 **-safemodeadministratorpassword** 引数です。 確認メッセージを強制するには、コマンドレットを対話的に実行する際に値を省略してください。  
>   
> オプションの **Whatif** 引数を **Install-ADDSDomainController** コマンドレットで使用すると、構成情報を確認することができます。 これにより、コマンドレットの引数の明示的および暗黙的な値を見ることができます。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSWhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件のチェック  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradePrereqCheck.png)  
  
**[前提条件のチェック]** は、AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、ドメインとフォレストが新しい Windows Server 2012 ドメイン コントローラーをサポートできるかどうかを検証します。  
  
新しいドメイン コントローラーをインストールするときに、サーバー マネージャー Active Directory Domain Services 構成ウィザードがシリアル化された一連のモジュラー テストを呼び出します。 これらのテストでは、警告と共に、候補となる修正オプションが提示されます。 テストは必要なだけ何度でも実行できます。 前提条件のテストにすべて合格するまで、ドメイン コントローラー プロセスを続行することはできません。  
  
**[前提条件のチェック]** では、以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかになります。  
  
特定の前提条件チェックについて詳しくは、[前提条件のチェックに関する説明](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)をご覧ください。  
  
サーバー マネージャーを使用する場合は **[前提条件のチェック]** を省略することはできませんが、AD DS 展開コマンドレットと以下の引数を使用すると省略できます。  
  
```  
-skipprechecks  
  
```  
  
> [!WARNING]  
> ただし Microsoft では前提条件のチェックを省略することはお勧めしません。ドメイン コントローラーの昇格が部分的に行われたり、AD DS フォレストに障害が発生したりする恐れがあります。  
  
ドメイン コントローラーの昇格プロセスを開始するには、 **[インストール]** をクリックします。 ここが、インストールをキャンセルする最後のチャンスとなります。 昇格プロセスが開始されると、キャンセルすることはできません。 昇格の結果に関係なく、昇格プロセスの最後でコンピューターが自動的に再起動します。プロセス中に発生した問題とその解決に関するガイダンスが **[前提条件のチェック]** ページに表示されます。  
  
### <a name="installation"></a>インストール  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_UpgradeInstallProgress.png)  
  
**[インストール]** ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
-   %systemroot%\debug\adprep\logs  
  
-   %systemroot%\debug\netsetup.log (サーバーがワークグループ内にある場合)  
  
ADDSDeployment モジュールを使って新しい Active Directory フォレストをインストールするには、次のコマンドレットを使用します。  
  
```  
Install-addsdomaincontroller  
```  
  
必須およびオプションの引数について詳しくは、[アップグレードとレプリカの Windows PowerShell](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md#BKMK_PS) をご覧ください。  
  
**Install-AddsDomainController** コマンドレットのフェーズは 2 つだけです (前提条件のチェックとインストール)。 以下の 2 つの図は、 **-domainname** および **-credential**の最低限の必須引数を使用したインストール フェーズを示しています。 Adprep 操作は、最初の Windows Server 2012 ドメイン コントローラーを既存の Windows Server 2003 フォレストに追加するプロセスの一部として自動的に実行されます。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSGetCred.png)  
  
**Install-ADDSDomainController** は、サーバー マネージャーと同様、昇格プロセスによって自動的にサーバーが再起動されることを知らせます。 再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の終了時にサーバーが自動的に再起動されないようにするには、 **-norebootoncompletion** 引数を使用します。  
  
> [!WARNING]  
> 再起動の無効化は推奨されません。 ドメイン コントローラーを正常に機能させるには、再起動する必要があります。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeConfirm.gif)  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeProgress.png)  
  
Windows PowerShell を使用してドメインコントローラーをリモートで構成するには、 **uninstall-addsdomaincontroller**コマンドレットを**コマンド**レットの*内部*にラップします。 これには中かっこが必要です。  
  
```  
invoke-command {install-addsdomaincontroller "domainname <domain> -credential (get-credential)} -computername <dc name>  
```  
  
以下に例を示します。  
  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_PSUpgradeExample.gif)  
  
> [!NOTE]  
> インストールと Adprep プロセスの動作の詳細については、[ドメイン コントローラーの展開のトラブルシューティング](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)をご覧ください。  
  
### <a name="results"></a>結果  
![レプリカをインストールする](media/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**[結果]** ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 正常に昇格された場合、ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  
以前のバージョンの Windows Server と同様、Windows Server 2012 を実行するドメイン コントローラーの自動ドメイン準備では GPPREP は実行されません。 Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 用に準備されていないすべてのドメインに対して、**adprep.exe /gpprep** を手動で実行してください。 特定のドメインに対して 1 度だけ (アップグレードのたびにではなく) GPPrep を実行する必要があります。 Adprep.exe は /gpprep を自動的に実行しません。これは、その操作により SYSVOL フォルダー内のすべてのファイルとフォルダーがすべてのドメイン コントローラー上で再レプリケートされる可能性があるためです。  
  

