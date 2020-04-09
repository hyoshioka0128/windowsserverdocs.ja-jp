---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメインをインストールする (レベル 200)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f7244b76364c8e2ce7249af8e76825a08b2a75c8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825335"
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメインをインストールする (レベル 200)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して、既存の Windows Server 2012 フォレストに子ドメインとツリー ドメインを追加する方法について説明します。  
  
-   [子ドメインとツリードメインのワークフロー](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [子ドメインとツリードメインの Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)  
  
-   [展開](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)  
  
## <a name="child-and-tree-domain-workflow"></a><a name="BKMK_Workflow"></a>子ドメインとツリードメインのワークフロー  
以下の図に、既に AD DS 役割をインストール済みで、既存のフォレスト内に新しいドメインを作成するためにサーバー マネージャーを使用して Active Directory ドメイン サービス構成ウィザードを開始した場合の、Active Directory ドメイン サービスの構成プロセスを示します。  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)  
  
## <a name="child-and-tree-domain-windows-powershell"></a><a name="BKMK_PS"></a>子ドメインとツリードメインの Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字** の引数は必須です。 *斜体*の引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます。)|  
|**Install-AddsDomain**|-SkipPreChecks<p>***-NewDomainName***<p>***-ParentDomainName***<p>***-SafeModeAdministratorPassword***<p>*-ADPrepCredential*<p>-AllowDomainReinstall<p>-Confirm<p>*-CreateDNSDelegation*<p>***-Credential***<p>*-DatabasePath*<p>*-DNSDelegationCredential*<p>-NoDNSOnNetwork<p>*-DomainMode*<p>***-DomainType***<p>-Force<p>*-InstallDNS*<p>*-LogPath*<p>*-NewDomainNetBIOSName*<p>*-NoGlobalCatalog*<p>-NoNorebootoncompletion<p>*-ReplicationSourceDC*<p>*-SiteName*<p>-SkipAutoConfigureDNS<p>*-SYSVOLPath*<p>*-Whatif*|  
  
> [!NOTE]  
> **-credential** 引数は、現在 Enterprise Admins グループのメンバーとしてログオンしていない場合にのみ必須です。 **-NewDomainNetBIOSName** 引数は、DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合と、名前が 15 文字を超えている場合に必須です。  
  
## <a name="deployment"></a><a name="BKMK_Deployment"></a>ディストリビューション  
  
### <a name="deployment-configuration"></a>展開構成  
以下のスクリーン ショットに、子ドメインを追加するオプションを示します。  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)  
  
以下のスクリーン ショットに、ツリー ドメインを追加するオプションを示します。  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)  
  
サーバー マネージャーは各ドメイン コントローラーの昇格を **[配置構成]** ページで開始します。 このページおよび以降のページの他のオプションおよび必須フィールドは、選択した展開操作によって異なります。  
  
このトピックでは、子ドメインの昇格とツリー ドメインの昇格という 2 つの個別の操作について同時に説明します。 2 つの操作の違いは、作成するドメイン タイプの違いだけです。 それ以外の手順はすべて同じです。  
  
-   新しい子ドメインを作成するには、 **[ドメインを既存のフォレストに追加する]** をクリックして **[子ドメイン]** を選択します。 **[親ドメイン名]** として、親ドメインの名前を入力するか選択します。 その後、新しいドメインの名前を **[新しいドメイン名]** ボックスに名前を入力します。 有効な単一ラベルの子ドメイン名を指定します。DNS ドメイン名の要件を満たす必要があります。  
  
-   既存のフォレスト内にツリー ドメインを作成するには、 **[ドメインを既存のフォレストに追加する]** をクリックして **[ツリー ドメイン]** を選択します。 フォレストのルート ドメインの名前を入力し、新しいドメインの名前を入力します。 有効な完全修飾ルート ドメイン名を指定します。単一ラベルは使用できず、DNS ドメイン名の要件を満たす必要があります。  
  
DNS 名の詳細については、 [コンピューター、ドメイン、サイト、OU などの Active Directory の命名規則に関する説明](https://support.microsoft.com/kb/909264)を参照してください。  
  
現在の資格情報がドメインのものではない場合、サーバー マネージャー Active Directory Domain Services 構成ウィザードではドメイン資格情報の入力を求められます。 **[変更]** をクリックして、昇格操作のためのドメイン資格情報を指定します。  
  
展開構成の ADDSDeployment コマンドレットと引数は以下のとおりです  
  
```  
Install-AddsDomain  
-domaintype <{childdomain | treedomain}>  
-parentdomainname <string>  
-newdomainname <string>  
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>ドメイン コントローラー オプション  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)  
  
**[ドメイン コントローラー オプション]** ページでは、新しいドメイン コントローラーのドメイン コントローラー オプションを指定します。 構成可能なドメイン コントローラー オプションは **[DNS サーバー]** と **[グローバル カタログ]** であり、読み取り専用ドメイン コントローラーを新しいドメインの最初のドメイン コントローラーとして構成することはできません。  
  
Microsoft では、分散環境で高可用性を実現するため、すべてのドメイン コントローラーで、DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択されます。DNS は、現在のドメインが、Start-of-Authority クエリに基づいて既にその DC 上にある DNS をホストする場合に、既定で選択されます。 また、 **[ドメインの機能レベル]** を指定する必要があります。 既定の機能レベルは Windows Server 2012 です。現在のフォレストの機能レベルと同じかそれ以上なら、どのような値でも選択できます。  
  
**[ドメイン コントローラー オプション]** ページでは、フォレストの構成から適切な Active Directory 論理**サイト名**を選択することもできます。 既定では、最適なサブネットのサイトが選択されます。 サイトが 1 つしかない場合は、それが自動的に選択されます。  
  
> [!IMPORTANT]  
> サーバーが Active Directory サブネットに属せず、複数の Active Directory サイトが存在する場合は、何も選択されず、リストからサイトを選択するまでは **[次へ]** ボタンが使用できません。  
  
**[ディレクトリ サービスの復元モード パスワード]** には、サーバーに適用されるパスワード ポリシーに従ったパスワードを指定する必要があります。 常に強力で複雑なパスワードを、または可能であればパスフレーズを選択します。  
  
**[ドメイン コントローラー オプション]** の ADDSDeployment コマンドレット引数は以下のとおりです。  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-Sitename <string>  
-SafeModeAdministratorPassword <secure string>  
-Credential <pscredential>  
```  
  
> [!IMPORTANT]  
> **sitename** 引数の値として指定するサイト名は既に存在している必要があります。 **install-AddsDomainController** コマンドレットはサイト名を作成しません。 新しいサイトを作成するには **new-adreplicationsite** コマンドレットを使用します。  
  
**Install-ADDSDomainController** コマンドレット引数は、特に指定しない限り、サーバー マネージャーと同じ既定値を使用します。  
  
**SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります。  
  
-   この引数を*指定しない*場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。  
  
    たとえば、NorthAmerica という名前の新しい子ドメインを Contoso.com フォレストに作成し、マスクされたパスワードの入力と確認入力を求められるようにするには、以下のように実行します  
  
    ```  
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child  
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
  
最後に、暗号化したパスワードをファイルに保存して後で使用することができます。こうするとクリア テキストのパスワードを表示せずに済みます。 例 :  
  
```  
$file = "c:\pw.txt"  
$pw = read-host -prompt "Password:" -assecurestring  
$pw | ConvertFrom-SecureString | Set-Content $file  
  
-safemodeadministratorpassword (Get-Content $File | ConvertTo-SecureString)  
  
```  
  
> [!WARNING]  
> クリア テキストや暗号化されたテキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。  そのファイルにアクセスできる人はだれでも、暗号化されたパスワードを元に戻すことができます。 それができると、DSRM で開始された DS にログオンでき、その後ドメイン コントローラー自体を偽装し、アクセス権を AD フォレスト内で最高レベルに昇格することができます。 テキスト ファイル データを暗号化するための **System.Security.Cryptography** の一連の使用手順を読むことが推奨されますが、ここでは取り上げません。 ベスト プラクティスは、パスワードの保存を絶対に避けることです。  
  
ADDSDeployment モジュールには、DNS クライアントの設定、フォワーダー、ルート ヒントの自動構成を省略するオプションがあります。 これは、サーバー マネージャーを使用する場合は構成できません。 この引数は、ドメイン コントローラーを構成する前に DNS サーバー サービスをインストールした場合のみ意味を持ちます。  
  
```  
-SkipAutoConfigureDNS  
  
```  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)  
  
**[DNS オプション]** ページでは、委任用の別の DNS 管理者資格情報を指定することができます。  
  
**[ドメイン コントローラー オプション]** ページで DNS インストールを選択した既存のフォレストに新しいドメインをインストールする場合、オプションを構成することはできません。自動的に委任が行われ、変更できません。 その構造を更新する権利を持つ、別の DNS 管理者資格情報を指定することができます。  
  
**[DNS オプション]** の ADDSDeployment Windows PowerShell 引数は以下のとおりです  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
DNS 委任の詳細については、「 [Understanding Zone Delegation (ゾーンの委任とは)](https://technet.microsoft.com/library/cc771640.aspx)」を参照してください。  
  
### <a name="additional-options"></a>追加オプション  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)  
  
**[追加オプション]** ページには、ドメインの NetBIOS 名が表示されます。この名前は上書きできます。 既定では、NetBIOS ドメイン名は **[配置構成]** ページで指定された完全修飾ドメイン名の一番左のラベルに一致します。 たとえば、完全修飾ドメイン名として corp.contoso.com を指定した場合、既定の NetBIOS ドメイン名は CORP です。  
  
15 文字以下で、他の NetBIOS 名と競合していない名前は、変更されません。 他の NetBIOS 名と競合している場合は、番号が付加されます。 15 文字を超えている場合は、一意の、もっと短い名前の候補がウィザードによって示されます。 ウィザードでは、いずれの場合も、WINS 参照および NetBIOS ブロードキャストを介して、名前が既に使用されていないかどうかが最初に検証されます。  
  
DNS 名の詳細については、 [コンピューター、ドメイン、サイト、OU などの Active Directory の命名規則に関する説明](https://support.microsoft.com/kb/909264)を参照してください。  
  
**Install-ADDSDomainController** コマンドレット引数は、特に指定しない限り、サーバー マネージャーと同じ既定値を使用します。 **SafeModeAdministratorPassword** 引数の操作は特別で、以下のような特徴があります  
  
1.  NetBIOS ドメイン名に **NewDomainNetBIOSName** 引数が指定されない場合で、 **DomainName** 引数の単一ラベルのプレフィックス ドメイン名が 15 文字以下の場合は、自動的に生成された名前で昇格が続行します。  
  
2.  NetBIOS ドメイン名に **NewDomainNetBIOSName** 引数が指定されない場合で、 **DomainName** 引数の単一ラベルのプレフィックス ドメイン名が 16 文字以上の場合は、昇格が失敗します。  
  
3.  **NewDomainNetBIOSName** 引数に 15 文字以下の NetBIOS ドメイン名が指定された場合は、その名前で昇格が続行します。  
  
4.  **NewDomainNetBIOSName** 引数に 16 文字以上の NetBIOS ドメイン名が指定された場合は、昇格が失敗します。  
  
**[追加オプション]** の ADDSDeployment コマンドレットの引数は以下のとおりです。  
  
```  
-newdomainnetbiosname <string>  
```  
  
### <a name="paths"></a>パス  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**[パス]** ページでは、AD DS データベース、データベース トランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所を上書きできます。 既定の場所は常に %systemroot% のサブディレクトリです。  
  
**[ドメイン コントローラー オプション]** の ADDSDeployment コマンドレット引数は以下のとおりです。  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)  
  
**[オプションの確認]** ページでは、インストールを開始する前に、設定を確認し、それらが要件を満たしているかどうか確認することができます。 これがサーバー マネージャーの使用中においてインストールを中止する最後の機会ではありません。 構成を続行する前に設定を確認するためのオプションにすぎません。  
  
サーバー マネージャーの **[オプションの確認]** ページにあるオプションの **[スクリプトの表示]** ボタンを使用すると、現在の ADDSDeployment モジュール構成を単一の Windows PowerShell スクリプトとして含む Unicode テキスト ファイルを作成することもできます。 これにより、サーバー マネージャーのグラフィカル インターフェイスを Windows PowerShell 展開スタジオとして使用できます。 Active Directory ドメイン サービス構成ウィザードを使用してオプションを構成し、構成をエクスポートした後、ウィザードをキャンセルします。  これによって有効で正しい構文のサンプルが作成されるので、それをさらに変更したり、直接使用したりできます。 例 :  
  
```  
#  
# Windows PowerShell Script for AD DS Deployment  
#  
  
Import-Module ADDSDeployment  
Install-ADDSDomain `  
-NoGlobalCatalog:$false `  
-CreateDNSDelegation `  
-Credential (Get-Credential) `  
-DatabasePath "C:\Windows\NTDS" `  
-DomainMode "Win2012" `  
-DomainType "ChildDomain" `  
-InstallDNS:$true `  
-LogPath "C:\Windows\NTDS" `  
-NewDomainName "research" `  
-NewDomainNetBIOSName "RESEARCH" `  
-ParentDomainName "corp.contoso.com" `  
-Norebootoncompletion:$false `  
-SiteName "Default-First-Site-Name" `  
-SYSVOLPath "C:\Windows\SYSVOL"  
-Force:$true  
  
```  
  
> [!NOTE]  
> サーバー マネージャーでは通常、昇格時にすべての引数とその値を入力し、既定値に依存しません (既定値は将来のバージョンの Windows 間またはサービス パック間で変わる可能性があるため)。 唯一の例外は **-safemodeadministratorpassword** 引数です (これはあえてスクリプトから除外されています)。 確認プロンプトを強制的に表示するには、コマンドレットを対話的に実行するときに値を省略します。  
  
構成情報を確認するには、**Install-ADDSForest** コマンドレットと共にオプションの **Whatif** 引数を使用します。 これにより、コマンドレットの引数の明示的および暗黙的な値を見ることができます。  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件のチェック  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)  
  
**[前提条件のチェック]** は、AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバー構成が新しい AD DS ドメインをサポートできるかどうかを検証します。  
  
新しいフォレスト ルート ドメインをインストールするときに、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードが、シリアル化された一連のモジュラー テストを呼び出します。 これらのテストでは、警告と共に、候補となる修正オプションが提示されます。 テストは必要なだけ何度でも実行できます。 前提条件のテストにすべて合格するまで、ドメイン コントローラー プロセスを続行することはできません。  
  
**[前提条件のチェック]** では、以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかになります。  
  
具体的な前提条件チェックの詳細については、「[前提条件のチェック](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)」を参照してください。  
  
サーバー マネージャーを使用する場合は **[前提条件のチェック]** を省略することはできませんが、AD DS 展開コマンドレットと以下の引数を使用すると省略できます。  
  
```  
-skipprechecks  
```  
  
> [!WARNING]  
> ただし Microsoft では前提条件のチェックを省略することはお勧めしません。ドメイン コントローラーの昇格が部分的に行われたり、AD DS フォレストに障害が発生したりする恐れがあります。  
  
ドメイン コントローラーの昇格プロセスを開始するには、 **[インストール]** をクリックします。 ここが、インストールをキャンセルする最後のチャンスとなります。 昇格プロセスが開始されると、キャンセルすることはできません。 昇格の結果に関係なく、昇格プロセスの最後でコンピューターが自動的に再起動します。  
  
### <a name="installation"></a>インストール  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)  
  
**[インストール]** ページが表示されると、ドメイン コントローラーの構成が開始され、停止やキャンセルは実行できません。 操作の詳しい内容がこのページに表示され、以下のログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment モジュールを使用して新しい Active Directory ドメインをインストールするには、以下のコマンドレットを使用します  
  
```  
Install-addsdomain  
```  
  
必須とオプションの引数については、[子ドメインとツリードメインの Windows PowerShell に関する説明](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)をご覧ください。**Install-addsdomain** コマンドレットのフェーズは 2 つだけです (前提条件のチェックとインストール)。 以下の 2 つの図は、 **-domaintype**、 **-newdomainname**、 **-parentdomainname**、 **-credential** の最低限の必須引数を使用したインストール フェーズを示しています。 **Install-ADDSDomain** は、サーバー マネージャーと同様、昇格プロセスによって自動的にサーバーが再起動されることを知らせます。  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)  
  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)  
  
再起動プロンプトを自動的に受け入れるには、ADDSDeployment Windows PowerShell コマンドレットで **-force** または **-confirm:$false** 引数を使用します。 昇格の終了時にサーバーが自動的に再起動されないようにするには、 **-norebootoncompletion** 引数を使用します。  
  
> [!WARNING]  
> 再起動の上書きはお勧めしません。 ドメイン コントローラーを正常に機能させるには、再起動する必要があります。  
  
### <a name="results"></a>結果  
![新しい AD 子のインストール](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**[結果]** ページには、昇格の成功または失敗と、重要な管理情報が表示されます。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  

