---
ms.assetid: e3d55565-ad45-4504-ad73-8103d1a92170
title: "Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメイン (レベル 200) をインストールします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc0eecc44bbc5f7459f22aceb5ebe41cd61948b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-a-new-windows-server-2012-active-directory-child-or-tree-domain-level-200"></a>Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメイン (レベル 200) をインストールします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、サーバー マネージャーまたは Windows PowerShell を使用して、既存の Windows Server 2012 フォレストに子ドメインとツリー ドメインを追加する方法について説明します。  
  
-   [子ドメインとツリー ドメインのワークフロー](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Workflow)  
  
-   [子ドメインとツリー ドメインの Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)  
  
-   [展開](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_Deployment)  
  
## <a name="BKMK_Workflow"></a>子ドメインとツリー ドメインのワークフロー  
次の図は、以前に AD DS の役割をインストールして、Active Directory ドメイン サービス構成ウィザードを既存のフォレストに新しいドメインを作成するサーバー マネージャーを使用してを開始した場合に、Active Directory Domain Services 構成プロセスを示します。  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/adds_childtreedeploy_beta1.png)  
  
## <a name="BKMK_PS"></a>子ドメインとツリー ドメインの Windows PowerShell  
  
|||  
|-|-|  
|**ADDSDeployment コマンドレット**|引数 (**太字**引数は必須です。 *文字を斜体に*引数は、Windows PowerShell または AD DS 構成ウィザードを使用して指定できます)。|  
|**Install-addsdomain**|-SkipPreChecks<br /><br />***-NewDomainName***<br /><br />***-ParentDomainName***<br /><br />***-Safemodeadministratorpassword***<br /><br />*-ADPrepCredential*<br /><br />-AllowDomainReinstall<br /><br />-確認します。<br /><br />*-CreateDNSDelegation*<br /><br />***資格情報***<br /><br />*-DatabasePath*<br /><br />*-DNSDelegationCredential*<br /><br />-NoDNSOnNetwork<br /><br />*DomainMode-*<br /><br />***DomainType-***<br /><br />フォース<br /><br />*-InstallDNS*<br /><br />*-Logpath*<br /><br />*NewDomainNetBIOSName-*<br /><br />*-NoGlobalCatalog*<br /><br />-NoNorebootoncompletion<br /><br />*-ReplicationSourceDC*<br /><br />*-サイト名*<br /><br />-SkipAutoConfigureDNS<br /><br />*-SYSVOLPath*<br /><br />*-Whatif*|  
  
> [!NOTE]  
> **-Credential**引数は、のみ、Enterprise Admins グループのメンバーとしてログオンしていないときに必要です。**- NewDomainNetBIOSName** DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合、または名前が 15 文字を超える場合は、引数が必要です。  
  
## <a name="BKMK_Deployment"></a>展開  
  
### <a name="deployment-configuration"></a>展開の構成  
次のスクリーン ショットは、子ドメインを追加するオプションを示します。  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDeployConfig.png)  
  
次のスクリーン ショットは、ツリー ドメインを追加するオプションを示します。  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_TreeDeployConfig.png)  
  
サーバー マネージャーですべてのドメイン コントローラーの昇格を開始する、**展開構成**ページ。 他のオプションおよび必須フィールドは、このページと選択した展開操作によって、以降のページに変更します。  
  
このトピックは次の 2 つの個別の操作を組み合わせたもの: 子ドメインの昇格とツリー ドメインの昇格します。 2 つの操作の唯一の違いは、ドメインの種類を作成することです。 すべての他の手順は、2 つの操作の間で同じです。  
  
-   新しい子ドメインを作成する] をクリックして**既存のフォレストにドメインを追加**選択および**子ドメイン**します。 **親ドメイン名**を入力するか、親ドメインの名前を選択します。 新しいドメインの名前を入力し、**新しいドメイン名**ボックス。 有効な単一ラベルの子ドメイン名を提供します。名前は、DNS ドメイン名の要件を使用する必要があります。  
  
-   既存のフォレスト内にツリー ドメインを作成する] をクリックして**既存のフォレストにドメインを追加**選択および**ツリー ドメイン**します。 フォレスト ルート ドメインの名前を入力し、新しいドメインの名前を入力します。 有効な完全修飾ルート ドメイン名を指定します。名前は、単一ラベルをすることはできず、DNS ドメイン名の要件を使用する必要があります。  
  
DNS 名の詳細については、次を参照してください。[の命名規則 Active Directory 内のコンピューター、ドメイン、サイト、および Ou](https://support.microsoft.com/kb/909264)します。  
  
サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、ドメイン資格情報の場合は、現在の資格情報がドメインからするように求めます。 をクリックして**変更**を昇格操作のドメイン資格情報を提供します。  
  
展開構成の ADDSDeployment コマンドレットと引数は。  
  
```  
Install-AddsDomain  
-domaintype <{childdomain | treedomain}>  
-parentdomainname <string>  
-newdomainname <string>  
-credential <pscredential>  
```  
  
### <a name="domain-controller-options"></a>ドメイン コント ローラー オプション  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_DCOptions_Child.gif)  
  
**ドメイン コント ローラー オプション**] ページが新しいドメイン コント ローラーのドメイン コント ローラー オプションを指定します。 構成可能なドメイン コント ローラー オプションは**DNS サーバー**と**グローバル カタログ**です。新しいドメインの最初のドメイン コント ローラーとして、読み取り専用ドメイン コント ローラーを構成することはできません。  
  
マイクロソフトでは、すべてのドメイン コントローラが、分散環境での高可用性の DNS と GC サービスを提供することをお勧めします。 GC は常に既定で選択し、現在のドメインが既にその Dc は、スタート画面から権限のクエリに基づく上の DNS をホストしている場合、DNS が既定で選択します。 指定する必要があります、**ドメインの機能レベル**します。 既定の機能レベルが Windows Server 2012、およびその他の現在のフォレストの機能レベル以上の値を選択できます。  
  
**ドメイン コント ローラー オプション**] ページでは、適切な Active Directory 論理を選択することもできます**サイト名**、フォレストの構成からです。 既定では、最も適切なサブネットのサイトを選択します。 1 つのサイトがある場合は、自動的に選択されます。  
  
> [!IMPORTANT]  
> サーバーが Active Directory のサブネットに属していない複数の Active Directory サイトがある場合は、何も選択し、**[次へ]**ボタンは、一覧からサイトを選択するまでは利用できません。  
  
指定した**ディレクトリ サービス復元モード パスワード**サーバーに適用されるパスワード ポリシーに従う必要があります。 常に強力で複雑なパスワードまたは可能であれば、パスフレーズを選択します。  
  
**ドメイン コント ローラー オプション**ADDSDeployment コマンドレット引数は。  
  
```  
-InstallDNS <{$false | $true}>  
-NoGlobalCatalog <{$false | $true}>  
-DomainMode <{Win2003 | Win2008 | Win2008R2 | Win2012 | Default}>  
-Sitename <string>  
-SafeModeAdministratorPassword <secure string>  
-Credential <pscredential>  
```  
  
> [!IMPORTANT]  
> 値として提供されると、サイト名は既に存在して、 **sitename**引数。 **Install-addsdomaincontroller**コマンドレットは、サイト名を作成しません。 使用することができます、**新しい adreplicationsite**コマンドレットに新しいサイトを作成します。  
  
**Install-addsdomaincontroller**コマンドレットの引数が指定されていない場合はサーバー マネージャーと同じ既定値に従います。  
  
**SafeModeAdministratorPassword**引数の操作は特別な。  
  
-   場合*が指定されていない*を引数としてコマンドレットは、して、マスクされたパスワードの確認入力を求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
    やなどの新しい子を作成するドメイン Contoso.com フォレスト NorthAmerica という名前と、マスクされたパスワードの確認入力を求めるメッセージが表示されます。  
  
    ```  
    Install-ADDSDomain "NewDomainName NorthAmerica "ParentDomainName Contoso.com "DomainType Child  
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
  
ADDSDeployment モジュールは、DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップする追加のオプションを提供します。 これはサーバー マネージャーを使用する場合に構成できません。 この引数が重要なは、ドメイン コント ローラーを構成する前に、DNS サーバー サービスが既にインストールされている場合にのみ。  
  
```  
-SkipAutoConfigureDNS  
  
```  
  
### <a name="dns-options-and-dns-delegation-credentials"></a>DNS オプションと DNS 委任資格情報  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildDNSOptions.png)  
  
**DNS オプション**] ページでは、委任の代替の DNS 管理者資格情報を提供することができます。  
  
DNS インストールを選択した既存のフォレストに新しいドメインをインストールするときに、**ドメイン コント ローラー オプション**ページ - 任意のオプションを構成することはできません委任は、自動的にれ、変更できませんは発生します。 その構造を更新する権限を持つ別の DNS 管理者資格情報を提供するためのオプションがあります。  
  
**DNS オプション**ADDSDeployment Windows PowerShell 引数は。  
  
```  
-creatednsdelegation   
-dnsdelegationcredential <pscredential>  
```  
  
DNS 委任の詳細については、次を参照してください。[ゾーンの委任](https://technet.microsoft.com/library/cc771640.aspx)します。  
  
### <a name="additional-options"></a>その他のオプション  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildAdditionalOptions.png)  
  
**追加オプション**] ページに、ドメインの NetBIOS 名、およびそれを上書きすることができます。 既定では、NetBIOS ドメイン名は上で提供される完全修飾ドメイン名の一番左のラベルと一致する、**展開構成**ページ。 たとえば、corp.contoso.com の完全修飾ドメイン名を指定した場合、既定の NetBIOS ドメイン名は CORP です。  
  
名前が 15 文字以内と競合しない別の NetBIOS 名では変更します。 別の NetBIOS 名と競合している、名前に、数字が付加されます。 名前が 15 文字以内の場合、ウィザードは、切り捨てられた一意の候補を提供します。 ウィザードの最初の検証どちらの場合、名前が既に WINS 参照で使用されていないおよび NetBIOS ブロードキャストします。  
  
DNS 名の詳細については、次を参照してください。[の命名規則 Active Directory 内のコンピューター、ドメイン、サイト、および Ou](https://support.microsoft.com/kb/909264)します。  
  
**Install-addsdomain**引数が指定されていない場合はサーバー マネージャーと同じ既定値に従います。 **DomainNetBIOSName**操作は特別な。  
  
1.  場合、 **NewDomainNetBIOSName**引数が NetBIOS ドメイン名と、単一ラベル プレフィックスのドメイン名で指定されていない、 **DomainName**引数が 15 文字以下、自動的に生成された名前で昇格が続行します。  
  
2.  場合、 **NewDomainNetBIOSName**引数が NetBIOS ドメイン名と、単一ラベル プレフィックスのドメイン名で指定されていない、 **DomainName**引数が 16 文字以上し、昇格は失敗します。  
  
3.  場合、 **NewDomainNetBIOSName**引数が 15 文字以下の NetBIOS ドメイン名と共に指定し、指定された名前で昇格が続行します。  
  
4.  場合、 **NewDomainNetBIOSName**引数が NetBIOS ドメイン名が 16 文字以上指定し、昇格は失敗します。  
  
**追加オプション**ADDSDeployment コマンドレット引数は。  
  
```  
-newdomainnetbiosname <string>  
```  
  
### <a name="paths"></a>パス  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_UpgradePaths.png)  
  
**パス**] ページでは、AD DS データベース、データの基本のトランザクション ログ、および SYSVOL 共有の既定のフォルダーの場所を上書きすることができます。 既定の場所は、常に %systemroot% のサブディレクトリ内にします。  
  
**パス**ADDSDeployment コマンドレット引数は。  
  
```  
-databasepath <string>  
-logpath <string>  
-sysvolpath <string>  
```  
  
### <a name="review-options-and-view-script"></a>オプションの確認とスクリプトの表示  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildReviewOptions.png)  
  
**オプションの確認**] ページを使用して設定を確認し、インストールを開始する前に、要件を満たしていることを確認します。 これは、サーバー マネージャーを使っているときに、インストールを停止する最後の機会ではありません。 これは、単に、構成を続行する前に、設定を確認するオプション  
  
**オプションの確認**ページ サーバー マネージャーでも用意されています、省略可能な**スクリプトの表示**を単一の Windows PowerShell スクリプトとして現在の addsdeployment モジュール構成を含む Unicode テキスト ファイルを作成するボタンをクリックします。 これにより、Windows PowerShell 展開スタジオとしてサーバー マネージャーのグラフィカル インターフェイスを使用することができます。 Active Directory ドメイン サービス構成ウィザードを使用して、オプションを構成し、構成をエクスポート、ウィザードをキャンセルします。  このプロセスでは、さらに変更またはダイレクトの使用の有効であり、正しい構文のサンプルを作成します。 例えば：  
  
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
> サーバー マネージャーは、一般にすべての引数と値のプロモーションおよび (サービス パックまたは Windows の将来のバージョン間で変わる可能性がある) のように既定の設定に依存しないときに入力します。 1 つの例外は、 **-safemodeadministratorpassword**引数です (これは意図的に省略すると、スクリプトから)。 確認プロンプトを強制するには、コマンドレットを対話的に実行するときに値を省略します。  
  
オプションを使用して**Whatif**引数を使用、 **Install-addsforest**コマンドレットを構成情報を確認します。 これにより、コマンドレットの引数の明示的および暗黙的な値を表示することができます。  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildWhatIf.png)  
  
### <a name="prerequisites-check"></a>前提条件の確認  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildPrereqCheck.png)  
  
**前提条件のチェック**AD DS ドメイン構成の新しい機能です。 この新しいフェーズでは、サーバーの構成が新しい AD DS ドメインをサポートできることを検証します。  
  
新しいフォレスト ルート ドメインをインストールする場合、サーバー マネージャー Active Directory ドメイン サービス構成ウィザードは、一連のモジュラー テストをシリアル化されたを呼び出します。 これらのテストでは、推奨される修復のオプションを使用してアラートです。 必要なだけ何度でもテストを実行することができます。 すべての前提条件のテストまで、ドメイン コントローラーのプロセスを続行できません渡します。  
  
**前提条件のチェック**以前のオペレーティング システムに影響を与えるセキュリティの変更といった関連情報も明らかです。  
  
具体的な前提条件チェックの詳細については、次を参照してください。[前提条件のチェック](../../ad-ds/manage/AD-DS-Simplified-Administration.md#BKMK_PrereuisiteChecking)します。  
  
バイパスすることはできません、**の前提条件チェック**ときは、サーバー マネージャーを使用して進むことができます、プロセスは次の引数を使用して、AD DS 展開コマンドレットを使用する場合。  
  
```  
-skipprechecks  
```  
  
> [!WARNING]  
> Microsoft は、部分的なドメイン コントローラーの昇格につながるまたは AD DS フォレストが破損している前提条件のチェックをスキップすることです。  
  
をクリックして**インストール**をドメイン コントローラーの昇格プロセスを開始します。 これは、インストールをキャンセルする最後の機会です。 開始されると、昇格プロセスをキャンセルすることはできません。 コンピューターは、昇格の結果に関係なく、昇格プロセスの終了時に自動的に再起動します。  
  
### <a name="installation"></a>インストール  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ChildInstallation.png)  
  
ときに、**インストール**ページが表示されます、ドメイン コントローラーの構成を開始、停止またはできません取り消されます。 操作の詳しい内容は、このページに表示され、ログに書き込まれます。  
  
-   %systemroot%\debug\dcpromo.log  
  
-   %systemroot%\debug\dcpromoui.log  
  
ADDSDeployment モジュールを使用して新しい Active Directory ドメインをインストールするには、次のコマンドレットを使用します。  
  
```  
Install-addsdomain  
```  
  
参照してください[子ドメインとツリー ドメインの Windows PowerShell](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md#BKMK_PS)必須およびオプションの引数。**Install-addsdomain**コマンドレットはだけです (前提条件のチェックとインストール) の 2 つのフェーズです。 以下の 2 つの図の最低限の必須引数を使用したインストール フェーズを表示する**- domaintype**、 **- newdomainname**、 **- parentdomainname**、および**-credential**します。 注: 同様、サーバー マネージャー、 **Install-addsdomain**昇格プロセスで、サーバーの再起動は自動的にされることを知らせます。  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomain.png)  
  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_PSInstallADDSDomainProgress.png)  
  
再起動プロンプトを自動的に同意するを使用して、**-強制**または**-ことを確認: $false**いずれかの Windows PowerShell の ADDSDeployment コマンドレットと引数。 サーバーが自動的に昇格の最後に再起動を防ぐには、使用、**- norebootoncompletion**引数。  
  
> [!WARNING]  
> 再起動の上書きはお勧めしません。 正常に機能するドメイン コント ローラーを再起動する必要があります。  
  
### <a name="results"></a>結果  
![新しい AD 子をインストールします。](media/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-/ADDS_SMI_TR_ForestSignOff.png)  
  
**結果**ページは、の成功または失敗、昇格し、重要な管理情報を示しています。 ドメイン コントローラーは、10 秒後に自動的に再起動します。  
  

