---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: "Active Directory ドメイン サービス (レベル 100) のインストールします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f76aa1e5200a9fc2f47a559c4a318aa619d31557
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="install-active-directory-domain-services-level-100"></a>Active Directory ドメイン サービス (レベル 100) のインストールします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、次の方法のいずれかを使用して、Windows Server 2012 で AD DS をインストールする方法について説明します。  
  
-   [資格情報の Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)  
  
-   [Windows PowerShell を使用して AD DS をインストールします。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)  
  
-   [サーバー マネージャーを使用して AD DS をインストールします。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)  
  
-   [グラフィカル ユーザー インターフェイスを使用してステージング RODC インストールを実行します。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)  
  
## <a name="BKMK_Creds"></a>資格情報の Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための要件  
次の資格情報は、Adprep.exe を実行し、AD DS をインストールする必要があります。  
  
-   新しいフォレストをインストールするには、コンピューターのローカル管理者としてログオンする必要があります。  
  
-   新しい子ドメインまたは新しいドメイン ツリーをインストールするには、Enterprise Admins グループのメンバーとしてログオンする必要があります。  
  
-   既存のドメインで、追加のドメイン コントローラーをインストールするには、Domain Admins グループのメンバーがあります。  
  
    > [!NOTE]  
    > Adprep.exe コマンドを個別に実行しないし、既存のドメインまたはフォレスト内の Windows Server 2012 を実行している最初のドメイン コントローラーをインストールして、Adprep コマンドを実行する資格情報を入力するように求められます。 資格情報の要件は次のとおりです。  
    >   
    > -   フォレストの最初の Windows Server 2012 ドメイン コントローラーを導入するには、Enterprise Admins グループ、Schema Admins グループのメンバーの資格情報を指定する必要がありますを Domain Admins グループ、ドメインをホストする、スキーマ マスターできます。  
    > -   ドメインの最初の Windows Server 2012 ドメイン コントローラーを導入するには、Domain Admins グループのメンバーの資格情報を指定する必要があります。  
    > -   最初読み取り専用ドメイン コントローラー (RODC) フォレストを紹介するには、Enterprise Admins グループのメンバーの資格情報を指定する必要があります。  
    >   
    >     > [!NOTE]  
    >     > Adprep を実行して既に場合 /rodcprep Windows Server 2008 または Windows Server 2008 R2 では Windows Server 2012 の再度実行する必要はありません。  
  
## <a name="BKMK_PS"></a>Windows PowerShell を使用して AD DS をインストールします。  
Windows Server 2012 以降では、Windows PowerShell を使用して AD DS をインストールすることができます。 Dcpromo.exe は以降、Windows Server 2012 では推奨されなくなりましたが、応答ファイルを使用して引き続き dcpromo.exe を実行できます (dcpromo/unattend:<answerfile> dcpromo/answer または:<answerfile>)。 応答ファイルを使って dcpromo.exe の実行を継続することは、dcpromo.exe から Windows PowerShell に自動化を変換する既存の自動化時間に投資のリソースを持つ組織を提供します。 For more information about running dcpromo.exe with an answer file, see [https://support.microsoft.com/kb/947034](https://support.microsoft.com/kb/947034).  
  
Windows PowerShell を使用して AD DS の削除の詳細については、次を参照してください。[Windows PowerShell を使用して AD DS を削除する](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS)します。  
  
Windows PowerShell を使用して、役割の追加を開始します。 このコマンドは、AD DS サーバー役割をインストールし、AD DS および AD LDS サーバー管理ツール、Active Directory ユーザーとコンピューターなど、GUI ベースのツールなど、dcdia.exe などのコマンド ライン ツールをインストールします。 Windows PowerShell を使用すると、サーバー管理ツールは既定ではインストールされません。 You need to specify **"IncludeManagementTools** to manage the local server or install [Remote Server Administration Tools](https://www.microsoft.com/download/details.aspx?id=28972) to manage a remote server.  
  
```  
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools  
<<Windows PowerShell cmdlet and arguments>>  
```  
  
再起動が AD DS のインストールが完了した後まで必要はありません。  
  
ADDSDeployment モジュールで利用可能なコマンドレットを表示するには、このコマンドを実行できます。  
  
```  
Get-Command -Module ADDSDeployment
```  
  
コマンドレットと構文を指定可能な引数の一覧を表示するには。  
  
```  
Get-Help <cmdlet name>  
```  
  
たとえば、使用されていない読み取り専用ドメイン コントローラー (RODC) アカウントを作成するための引数を表示するには、次のように入力します。  
  
```  
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```  
  
省略可能な引数は角かっこで表示されます。  
  
最新のヘルプの例と Windows PowerShell コマンドレットの概念をダウンロードすることもできます。 For more information, see [about_Updatable_Help](https://technet.microsoft.com/library/hh847735.aspx).  
  
リモート サーバーに対して Windows PowerShell コマンドレットを実行することができます。  
  
-   Windows PowerShell で ADDSDeployment コマンドレットと共に Invoke-Command を使用します。 たとえば、リモート サーバーに AD DS をインストールするという名前の ConDC3 contoso.com ドメインで、種類。  
  
    ```  
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3  
    ```  
  
- または -  
  
-   サーバー マネージャーでは、リモート サーバーが含まれるサーバー グループを作成します。 リモート サーバーの名前を右クリックし、をクリックして**Windows PowerShell**します。  
  
次のセクションでは、AD DS をインストールする ADDSDeployment モジュールのコマンドレットを実行する方法について説明します。  
  
-   [ADDSDeployment コマンドレット引数](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)  
  
-   [Windows PowerShell 資格情報を指定します。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)  
  
-   [テスト コマンドレットを使用します。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)  
  
-   [Windows PowerShell を使用して、新しいフォレスト ルート ドメインをインストールします。](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)  
  
-   [Windows PowerShell を使用して新しい子ドメインまたはツリー ドメインをインストールします。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)  
  
-   [Windows PowerShell を使用して追加の (レプリカ) ドメイン コントローラーをインストールします。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)  
  
### <a name="BKMK_Params"></a>ADDSDeployment コマンドレット引数  
次の表は、Windows PowerShell の ADDSDeployment コマンドレットの引数を示します。 太字の引数が必要です。 Windows PowerShell で異なるという名前が場合、かっこで囲まれた dcpromo.exe の対応する引数のとおりです。  
  
Windows PowerShell のスイッチでは、引数 $TRUE または $FALSE を受け入れます。 既定で $TRUE の引数を指定する必要はありません。  
  
既定値を上書きするには、値を $False に引数を指定できます。 たとえば、ため**- installdns**ことを指定しない場合、する唯一の方法の新しいフォレストのインストールが自動的に実行*防止*新しいフォレストをインストールするときに、DNS のインストールは、使用します。  
  
```  
-InstallDNS:$false  
```  
  
同様に、ため**"installdns**環境では、Windows Server DNS をホストしていないドメイン コントローラーをインストールする場合は、既定の値を $False を持つサーバー、DNS サーバーをインストールするために次の引数を指定する必要があります。  
  
```  
-InstallDNS:$true  
```  
  
|引数|説明|  
|------------|---------------|  
|**ADPrepCredential <PS Credential>****注:**ドメイン内の最初の Windows Server 2012 ドメイン コントローラーをインストールするかどうか、またはフォレストと、現在のユーザーの資格情報が不十分である操作を実行するために必要なです。|Specifies the account with Enterprise Admins and Schema Admins group membership that can prepare the forest, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.<br /><br />値が指定されていない場合の値、**"credential**引数を使用します。|  
|AllowDomainControllerReinstall|同じ名前の別の書き込み可能なドメイン コントローラー アカウントが認識されているにもかかわらず、この書き込み可能なドメイン コントローラーのインストールを続行するかどうかを指定します。<br /><br />使用**$True**アカウントが現在は別の書き込み可能なドメイン コントローラーで使用しないことを確認する場合にのみです。<br /><br />既定値は**$False**します。<br /><br />この引数は、RODC に対して有効ではありません。|  
|AllowDomainReinstall|既存のドメインが再作成するかどうかを指定します。<br /><br />既定値は**$False**します。|  
|AllowPasswordReplicationAccountName < string[] >|ユーザー アカウント、グループ アカウント、およびパスワードが当該 RODC にレプリケートできるコンピューター アカウントの名前を指定します。 空の文字列を使用して""、値を空のままにする場合。 既定でのみ、許可されている RODC Password Replication Group が許可され、それが最初に作成した空です。<br /><br />文字列の配列として値を指定します。 例えば：<br /><br />-AllowPasswordReplicationAccountName"JSmith"、"JSmithPC"、"ブランチ Users"をコードします。|  
|ApplicationPartitionsToReplicate < string[] >**注:** UI に等価のオプションはありません。 UI を使用または IFM を使用してをインストールする場合はすべてのアプリケーション パーティションがレプリケートされます。|アプリケーション ディレクトリ パーティションをレプリケートするように指定します。 この引数が指定した場合にのみ適用される、**- InstallationMediaPath**メディア (IFM) からインストールする引数です。 既定では、パーティションをレプリケートするすべてのアプリケーションは、それぞれのスコープに基づいています。<br /><br />文字列の配列として値を指定します。 例えば：<br /><br />コード-<br /><br />-ApplicationPartitionsToReplicate「パーティション 1」、"partition2"、"partition3"|  
|確認|このコマンドレットを実行する前に確認を求めます。|  
|CreateDnsDelegation**注:** Add-ADDSReadOnlyDomainController コマンドレットを実行すると、この引数を指定することはできません。|ドメイン コントローラーと共にインストールする新しい DNS サーバーを参照する DNS 委任を作成するかどうかを示します。 有効なは、Active Directory"統合された DNS のみです。 委任レコードは、オンラインでアクセス可能である Microsoft DNS サーバーでのみ作成できます。 直下 .com、.gov、.biz、.edu または .nz、.au などの 2 文字の国コード ドメインなどの最上位のドメインにあるドメインの委任レコードを作成することはできません。<br /><br />既定値は、環境に基づいて自動的に計算されます。|  
|**Credential <PS Credential>****注:**、現在のユーザーの資格情報が不十分である操作を実行するかどうかにのみ必須です。|Specifies the domain account that can logon to the domain, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.<br /><br />値が指定されていない場合は、現在のユーザーの資格情報が使用されます。|  
|CriticalReplicationOnly|AD DS のインストール操作が重要なレプリケーションだけ再起動の前に実行して、続行するかどうかを指定します。 ではないレプリケーションについては、コンピューターを再起動して、インストールが完了した後に発生します。<br /><br />この引数を使用することは推奨されません。<br /><br />ユーザー インターフェイス (UI) には、このオプションに相当するものはありません。|  
|DatabasePath <string>|完全修飾指定以外"データベースを含むドメイン、たとえば、ローカル コンピューターの固定ディスク上のディレクトリへの汎用名前付け規則 (UNC) パス**C:\Windows\NTDS します。**<br /><br />既定値は**%SYSTEMROOT%\NTDS**します。 **重要:** Resilient File System (ReFS) でフォーマットされたボリューム上の AD DS データベースとログ ファイルを保存することができます、ReFS では AD DS をホストするために特に利点はありませんが、すべてのデータを ReFS でホストしているため回復性の通常の利点以外。|  
|DelegatedAdministratorAccountName <string>|ユーザーまたはインストールし、RODC を管理グループの名前を指定します。<br /><br />既定では、Domain Admins グループのメンバーのみが RODC を管理できます。|  
|DenyPasswordReplicationAccountName < string[] >|ユーザー アカウント、グループ アカウント、およびパスワードが当該 RODC にレプリケートされないが、コンピューター アカウントの名前を指定します。 空の文字列を使用して""任意のユーザーまたはコンピューターの資格情報のレプリケーションを拒否したくない場合。 既定では、Administrators、Server Operators、Backup Operators、Account Operators、および Denied RODC Password Replication Group が拒否されます。 既定では、Denied RODC Password Replication Group が含まれています Cert Publishers、Domain Admins、Enterprise Admins、Enterprise のドメイン コントローラー、Enterprise Read-Only ドメイン コントローラー、Group Policy Creator Owners、krbtgt アカウント、および Schema Admins します。<br /><br />文字列の配列として値を指定します。 例えば：<br /><br />コード-<br /><br />-DenyPasswordReplicationAccountName"RegionalAdmins"、"AdminPCs"|  
|DnsDelegationCredential <PS Credential>**注:** Add-ADDSReadOnlyDomainController コマンドレットを実行すると、この引数を指定することはできません。|Specifies the user name and password for creating DNS delegation, according to the rules of [Get-Credential](https://technet.microsoft.com/library/dd315327.aspx) and a PSCredential object.|  
|DomainMode <DomainMode> {Win2003 & #124 です。Win2008 & #124;Win2008R2 & #124;Win2012 & #124;Win2012R2}<br /><br />または<br /><br />DomainMode <DomainMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|新しいドメインの作成中には、ドメインの機能レベルを指定します。<br /><br />ドメインの機能レベルは、フォレストの機能レベルよりも低いすることはできませんより高いことができます。<br /><br />既定値が自動的に計算され、既存のフォレストの機能レベルまたはに設定されている値に設定されて**- ForestMode**します。|  
|**ドメイン名**<br /><br />Install-ADDSForest と Install-ADDSDomainController コマンドレットで必須です。|追加のドメイン コントローラーをインストールするドメインの FQDN を指定します。|  
|**DomainNetbiosName <string>**<br /><br />Install-ADDSForest FQDN のプレフィックス名が 15 文字より長い場合に必須です。|Install-ADDSForest で使用します。 新しいフォレスト ルート ドメインに NetBIOS 名を割り当てます。|  
|DomainType <DomainType> {ChildDomain & #124 です。TreeDomain} または {子 & #124; ツリー}|作成するドメインの種類を示します: フォレストの既存の新しいドメイン ツリー、既存のドメイン、または新しいフォレストの子です。<br /><br />DomainType の既定値は ChildDomain です。|  
|Force|ときに、コマンドレットを最後まで実行を許可するように、ドメイン コントローラーの追加とインストール中に通常表示されるすべての警告が表示されなくなりますこのパラメーターを指定します。 このパラメーターをインストール スクリプトを作成するときに含めることができます。|  
|ForestMode <ForestMode> {Win2003 & #124 です。Win2008 & #124;Win2008R2 & #124;Win2012 & #124;Win2012R2}<br /><br />または<br /><br />ForestMode <ForestMode> {2 & #124; 3 & #124; 4 & #124; 5 & #124; 6}|新しいフォレストを作成するときは、フォレストの機能レベルを指定します。<br /><br />既定値は Win2012 です。|  
|InstallationMediaPath|新しいドメイン コントローラーをインストールするために使用するインストール メディアの場所を示します。|  
|InstallDns|DNS サーバー サービスをインストールして、ドメイン コントローラーで構成されているかどうかを指定します。<br /><br />既定では、新しいフォレストの**$True**、DNS サーバーをインストールします。<br /><br />新しい子ドメインまたはドメイン ツリーには、親ドメイン (またはドメイン ツリーのフォレスト ルート ドメイン) 既にホストおよびドメインの DNS 名が格納されている場合、このパラメーターの既定値は $True です。<br /><br />既存のドメインにドメイン コントローラーのインストールの場合、このパラメーターは、左に指定されていないと、現在のドメインが既にホストして、このパラメーターの既定値は、ドメインの DNS 名が格納されて**$True**します。 それ以外の場合、DNS ドメイン名が Active Directory の外部でホストされている場合、既定値は**$False**し、DNS サーバーがインストールされていません。|  
|LogPath <string>|たとえば、ドメインのログ ファイルが含まれていますが、ローカル コンピューターの固定ディスク上、ディレクトリへの完全修飾 UNC パスを指定します。**C:\Windows\Logs**します。<br /><br />既定値は**%SYSTEMROOT%\NTDS**します。 **重要:** Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory ログ ファイルを格納しないでください。|  
|MoveInfrastructureOperationMasterRoleIfNecessary|"で現在グローバル カタログ サーバーでホストされている場合は"を作成して、ドメイン コントローラーにする予定がないドメイン コントローラーにインフラストラクチャ マスター操作マスターの役割 (とも呼ばれるフレキシブル シングル マスター操作または FSMO) を転送するかどうかを指定します、グローバル カタログ サーバーを作成することです。 転送が必要な場合に作成しているドメイン コントローラーにインフラストラクチャ マスターの役割を転送するには、このパラメーターを指定します。この場合は、指定の**NoGlobalCatalog**インフラストラクチャ マスターの役割を現在が発生する場合は、オプションです。|  
|**NewDomainName <string>****注:** Install-ADDSDomain でのみ必須です。|新しいドメインの単一のドメイン名を指定します。<br /><br />たとえば、という名前の新しい子ドメインを作成する**emea.corp.fabrikam.com**を指定する必要があります**emea**この引数の値として。|  
|**NewDomainNetbiosName <string>**<br /><br />Install-ADDSDomain FQDN のプレフィックス名が 15 文字より長い場合に必須です。|Install-ADDSDomain で使用します。 新しいドメインに NetBIOS 名を割り当てます。 既定値がの値から派生した**"NewDomainName**します。|  
|NoDnsOnNetwork|DNS サービスが、ネットワーク上で使用できないことを指定します。 このパラメーターは、名前解決に DNS サーバーの名前でこのコンピューターのネットワーク アダプターの IP 設定が構成されていない場合にのみ使用されます。 これは、DNS サーバーを名前解決のためには、このコンピューターにインストールすることを示します。 それ以外の場合、ネットワーク アダプターの IP 設定は、最初の DNS サーバー アドレスを持つ構成する必要があります。<br /><br />(既定) このパラメーターを省略すると、DNS サーバーに接続するこのサーバーのコンピューター上のネットワーク アダプターの TCP/IP クライアント設定が使用されることを示します。 そのため、このパラメーターを指定しない場合は、TCP/IP クライアント設定が優先 DNS サーバー アドレスで最初に構成されていることを確認します。|  
|NoGlobalCatalog|ドメイン コントローラーをグローバル カタログ サーバーにしないことを指定します。<br /><br />既定では、Windows Server 2012 を実行するドメイン コントローラーはグローバル カタログを使用してインストールします。 つまり、これが自動的に実行せず、計算を指定しない限り。<br /><br />コード-<br /><br />-NoGlobalCatalog|  
|NoRebootOnCompletion|成功した場合に関係なく、コマンドの完了時にコンピューターを再起動するかどうかを指定します。 既定では、コンピューターが再起動します。 サーバーが再起動しないようにするには、次のように指定します。<br /><br />コード-<br /><br />-NoRebootOnCompletion: $True<br /><br />ユーザー インターフェイス (UI) には、このオプションに相当するものはありません。|  
|**ParentDomainName <string>****注:** Install-ADDSDomain コマンドレット必須|既存の親ドメインの FQDN を指定します。 子ドメインまたは新しいドメイン ツリーをインストールするときに、この引数を使用します。<br /><br />たとえば、という名前の新しい子ドメインを作成する**emea.corp.fabrikam.com**を指定する必要があります**corp.fabrikam.com**この引数の値として。|  
|ReadOnlyReplica|読み取り専用ドメイン コントローラー (RODC) をインストールするかどうかを指定します。|  
|ReplicationSourceDC <string>|元のドメイン情報をレプリケートするパートナー ドメイン コントローラーの FQDN を示します。 既定値は自動的に計算します。|  
|**SafeModeAdministratorPassword <securestring>**|セーフ モードまたはそれに準ずるディレクトリ サービス復元モードなどのセーフ モードでコンピューターを起動すると、管理者アカウントのパスワードを提供します。<br /><br />既定では空のパスワードです。 パスワードを指定する必要があります。 Read-host-assecurestring や ConvertTo-SecureString によって提供されるものなど、System.Security.SecureString 形式では、パスワードを指定する必要があります。<br /><br />SafeModeAdministratorPassword 引数の操作は特別な: 引数としてを指定しない場合、コマンドレットと、マスクされたパスワードの確認入力を求められます。 これは、interactively.If が指定されているコマンドレットに指定されたその他の引数がない場合は、コマンドレットでは、確認なし、マスクされたパスワードを入力するように求められます。 interactively.If 指定値を持つ場合、値はセキュリティで保護された文字列である必要があります。 interactively.For 例では、手動での入力を求めるパスワードを使用して、Read-Host コマンドレットをセキュリティで保護された文字列を求めるダイアログ:-safemodeadministratorpassword (ホスト-読み取り - プロンプト"パスワード:"- assecurestring) 提供することも、セキュリティで保護された文字列としてクリア テキストの変換済みの変数が、これはお勧めします。 -safemodeadministratorpassword (convertto securestring"Password1"- asplaintext-強制)|  
|**サイト名 <string>**<br /><br />Add-addsreadonlydomaincontrolleraccount コマンドレット必須|ドメイン コントローラーをインストールするサイトを指定します。 あるない**"sitename**引数を実行するときに**Install-addsforest**作成された最初のサイトは Default-First-Site-Name のためです。<br /><br />引数として提供されると、サイト名は既に存在して**sitename**します。 このコマンドレットでは、サイトは作成されません。|  
|SkipAutoConfigureDNS|DNS クライアント設定、フォワーダー、およびルート ヒントの自動構成をスキップします。 この引数は、DNS サーバー サービスが既にインストールされているまたはで自動的にインストールされているかどうかでは有効でのみ**- InstallDNS**します。|  
|SystemKey <string>|データのレプリケートに使用するメディアのシステム キーを指定します。<br /><br />既定値は**none**します。<br /><br />データは、read-host-assecurestring や ConvertTo-SecureString によって提供される形式である必要があります。|  
|SysvolPath <string>|たとえば、ローカル コンピューターの固定ディスク上、ディレクトリへの完全修飾 UNC パスを指定**C:\Windows\SYSVOL**します。<br /><br />既定値は**%SYSTEMROOT%\SYSVOL**します。 **重要:** Resilient File System (ReFS) でフォーマットされたデータ ボリュームに SYSVOL を格納することはできません。|  
|SkipPreChecks|インストールを開始する前に前提条件のチェックは実行されません。 この設定を使用することはお勧めできません。|  
|WhatIf|コマンドレットを実行するどうなるかを示しています。 このコマンドレットは実行されません。|  
  
### <a name="BKMK_PSCreds"></a>Windows PowerShell 資格情報を指定します。  
You can specify credentials without revealing them in plain text on screen by using [Get-credential](https://technet.microsoft.com/library/dd315327.aspx).  
  
-Safemodeadministratorpassword 引数と LocalAdministratorPassword 引数の操作は特殊です。  
  
-   引数として指定されていない場合、コマンドレットでは、入力し、マスクされたパスワードを確認するように求められます。 これは、コマンドレットを対話的に実行するときに、推奨される使用方法です。  
  
-   値を指定して、値がセキュリティで保護された文字列にあります。 コマンドレットを対話的に実行するときに推奨される使用方法はありません。  
  
たとえば、手動での入力を求めるパスワードを使用して、**Read-host**コマンドレットをセキュリティで保護された文字列を求めるダイアログ  
  
```  
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```  
  
> [!WARNING]  
> 前のオプションは、パスワードを確認しない、細心の注意を使用して、: パスワードは表示されません。  
  
これはお勧めはクリア テキストの変換済みの変数としてセキュリティで保護された文字列を提供できます。  
  
```  
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```  
  
> [!WARNING]  
> 提供するかクリア テキストのパスワードを保存するは推奨されません。 スクリプトでこのコマンドを実行しているか、その背後で見てすべてのユーザーは、そのドメイン コントローラーの DSRM パスワードを認識します。 した情報を使って、ドメイン コントローラーそのものを偽装し、自分の権限を Active Directory フォレストで最も高いレベルに昇格します。  
  
### <a name="BKMK_TestCmdlets"></a>テスト コマンドレットを使用します。  
各 ADDSDeployment コマンドレットには、対応するコマンドレットをテストします。 テスト コマンドレットの実行、インストール操作の前提条件の確認のみインストールの設定が構成されていません。 各テスト コマンドレットの引数は、対応するインストール コマンドレットと同じが**"SkipPreChecks**テスト コマンドレットでは使用できません。  
  
|テスト コマンドレット|説明|  
|---------------|---------------|  
|テスト ADDSForestInstallation|新しい Active Directory フォレストをインストールするための前提条件を実行します。|  
|テスト ADDSDomainInstallation|Active Directory で新しいドメインをインストールするための前提条件を実行します。|  
|テスト ADDSDomainControllerInstallation|Active Directory 内のドメイン コントローラーのインストールの前提条件を実行します。|  
|テスト ADDSReadOnlyDomainControllerAccountCreation|読み取り専用ドメイン コントローラーを追加するための前提条件 (RODC) アカウントを実行します。|  
  
### <a name="BKMK_PSForest"></a>Windows PowerShell を使用して、新しいフォレスト ルート ドメインをインストールします。  
新しいフォレストをインストールするためのコマンド構文は次のとおりです。 省略可能な引数は角かっこで囲ま表示されます。  
  
```  
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字名を変更する場合、または名前が 15 文字を超える場合、-domainnetbiosname 引数が必要です。  
  
たとえば、corp.contoso.com という名前の新しいフォレストをインストールして、DSRM パスワードを入力するように求められます安全に、次のように入力します。  
  
```  
Install-ADDSForest -DomainName "corp.contoso.com"   
```  
  
> [!NOTE]  
> Install-ADDSForest を実行すると、DNS サーバーは既定でインストールされます。  
  
ディレクトリ サービス復元モード パスワードと種類を指定するように求めをインストール corp.contoso.com という名前の新しいフォレスト、contoso.com ドメインに DNS 委任を作成、Windows Server 2008 R2 にドメインの機能レベルを設定し、Windows Server 2008 にフォレストの機能レベルを設定、Active Directory データベースと SYSVOL を D:\ ドライブにインストール、ログ ファイルを E:\ ドライブにインストールします。:  
  
```  
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="BKMK_PSDomain"></a>Windows PowerShell を使用して新しい子ドメインまたはツリー ドメインをインストールします。  
新しいドメインをインストールするためのコマンド構文は次のとおりです。 省略可能な引数は角かっこで囲ま表示されます。  
  
```  
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
> [!NOTE]  
> **-Credential**引数は、のみ、Enterprise Admins グループのメンバーとしてログオンしていないときに必要です。  
>   
> **- NewDomainNetBIOSName** DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合、または名前が 15 文字を超える場合は、引数が必要です。  
  
たとえば、child.corp.contoso.com という名前の新しい子ドメインを作成、DNS サーバーをインストール、corp.contoso.com ドメインに DNS 委任を作成、Windows Server 2003 ドメイン機能レベルを設定、ヒューストンという名前のサイトでグローバル カタログ サーバーをドメイン コントローラーに行った corp\EnterpriseAdmin1 の資格情報を使用するレプリケーション ソース ドメイン コントローラーとして DC1.corp.contoso.com を使用して、Active Directory データベースと SYSVOL を D:\ ドライブにインストール、ログ ファイルを E:\ ドライブにインストールし、ディレクトリ サービス復元モード パスワードを指定するが、コマンドの確認を求めないを入力するように求められます。  
  
```  
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False  
```  
  
### <a name="BKMK_PSReplica"></a>Windows PowerShell を使用して追加の (レプリカ) ドメイン コントローラーをインストールします。  
追加のドメイン コントローラーをインストールするためのコマンド構文は次のとおりです。 省略可能な引数は角かっこで囲ま表示されます。  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
corp.contoso.com ドメインのドメイン コントローラーと DNS サーバーをインストールして、ドメイン管理者の資格情報と DSRM パスワードを指定するように求められます、次のように入力します。  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```  
  
コンピューターが既にドメインに参加していると Domain Admins グループのメンバーである、使用することができます。  
  
```  
Install-ADDSDomainController -DomainName "corp.contoso.com"  
```  
  
ドメイン名の入力が要求される次のように入力します。  
  
```  
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```  
  
次のコマンドは、資格情報を使用 Contoso\EnterpriseAdmin1 のボストンという名前のサイトで書き込み可能ドメイン コントローラーとグローバル カタログ サーバーをインストール、DNS サーバーをインストール、contoso.com ドメインに DNS 委任を作成、c:\ADDS IFM フォルダーに格納されているメディアからのインストール、Active Directory データベースと SYSVOL を D:\ ドライブにインストール、ログ ファイルを E:\ ドライブにインストール、がサーバーに自動的に再起動後、AD DS のインストールが完了し、ディレクトリ サービス復元モード パスワードを入力するように求められます。  
  
```  
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"   
```  
  
### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Windows PowerShell を使用して段階的 RODC インストールを実行します。  
RODC アカウントを作成するコマンドの構文は次のとおりです。 省略可能な引数は角かっこで囲ま表示されます。  
  
```  
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]  
```  
  
サーバーを RODC アカウントにアタッチするコマンドの構文は次のとおりです。 省略可能な引数は角かっこで囲ま表示されます。  
  
```  
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]  
```  
  
たとえば、RODC アカウントを作成する RODC1 という名前の。  
  
```  
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA  
```  
  
RODC1 アカウントにアタッチするサーバーで、次のコマンドを実行します。 サーバーは、ドメインに参加することはできません。 最初に、AD DS サーバー役割と管理ツールをインストールします。  
  
```  
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```  
  
RODC を作成する次のコマンドを実行します。  
  
```  
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```  
  
キーを押して**Y**を含めるかを確認、**"ことを確認**確認プロンプトを防ぐための引数。  
  
## <a name="BKMK_GUI"></a>サーバー マネージャーを使用して AD DS をインストールします。  
サーバー マネージャーで、新しい Windows Server 2012 以降は、Active Directory ドメイン サービス構成ウィザード、続けて役割の追加ウィザードを使用して、Windows Server 2012 で AD DS をインストールできます。 Active Directory ドメイン サービス インストール ウィザード (dcpromo.exe) は、以降では、Windows Server 2012 は推奨されなくなりました。  
  
次のセクションをインストールして複数のサーバーに AD DS を管理するためにサーバー プールを作成する方法と、ウィザードを使用して AD DS をインストールする方法について説明します。  
  
### <a name="BKMK_ServerPools"></a>サーバー プールの作成  
サーバー マネージャーは、サーバー マネージャーを実行しているコンピューターからアクセス可能である限り、ネットワーク上の他のサーバーをプールことができます。 プール、それらのサーバーのリモート インストール AD DS またはサーバー マネージャー内で使用できる構成オプションを選択します。 サーバー マネージャーを自動的に実行しているコンピューター プールされます。 For more information about server pools, see [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
> [!NOTE]  
> ワークグループ サーバー、またはその逆にサーバー マネージャーを使用してドメインに参加しているコンピューターを管理するためには、追加の構成手順が必要です。 For more information, see "Add and manage servers in workgroups" in [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
### <a name="BKMK_installADDSGUI"></a>AD DS をインストールします。  
**管理者の資格情報**  
  
AD DS をインストールするための資格情報の要件は、選択する配置構成によって異なります。 詳細については、次を参照してください。[資格情報の Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための要件](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)します。  
  
GUI の方法を使用して AD DS をインストールするのにには、次の手順を使用します。 手順は、ローカルまたはリモートで実行できます。 次の手順の詳細については、次のトピックを参照してください。  
  
-   [サーバー マネージャーでフォレストを展開します。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)  
  
-   [既存のドメイン (&) #40; でレプリカ Windows Server 2012 ドメイン コントローラーをインストールします。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  
-   [Windows Server 2012 の新しい Active Directory 子またはツリー ドメイン (&) #40; をインストールします。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
  
-   [Windows Server 2012 の Active Directory インストール Read-Only ドメイン コントローラー (&) #40 です。RODC & #41 です。& #40 です。レベル 200 & #41 です。](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)  
  
##### <a name="to-install-ad-ds-by-using-server-manager"></a>サーバー マネージャーを使用して AD DS をインストールするには  
  
1.  サーバー マネージャーで、クリックして**管理**] をクリック**追加の役割と機能**を役割の追加ウィザードを開始します。  
  
2.  **開始する前に**] ページで [**次**します。  
  
3.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**] をクリックし、**[次へ]**します。  
  
4.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、クリックして、AD DS をインストールするサーバーの名前をクリックして**[次へ]**します。  
  
    リモート サーバーを選択するには、まずサーバー プールを作成し、リモート サーバーを追加します。 For more information about creating server pools, see [Add Servers to Server Manager](https://technet.microsoft.com/library/hh831453.aspx).  
  
5.  **サーバーの役割の選択**] ページで [ **Active Directory ドメイン サービス**、次に、**追加の役割と機能のウィザード**ダイアログ ボックスで、] をクリックして**機能の追加**、] をクリックし、**[次へ]**します。  
  
6.  **機能の選択**] ページで、追加機能をインストールし] をクリックする選択**次**します。  
  
7.  **Active Directory Domain Services** ] ページで情報を確認してをクリックして**次**します。  
  
8.  **インストール オプションの確認**] ページで [**インストール**します。  
  
9. **結果**] ページで、インストールが成功したことを確認] をクリックして**このサーバーのドメイン コントローラーを昇格**を Active Directory ドメイン サービス構成ウィザードを開始します。  
  
    ![AD DS をインストールします。](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)  
  
    > [!IMPORTANT]  
    > 役割の追加ウィザードこの時点でを閉じるには、Active Directory ドメイン サービス構成ウィザードを起動しなくても、サーバー マネージャーでのタスク] をクリックして再開できます。  
  
    ![AD DS をインストールします。](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
10. **展開構成**] ページで、次のオプションのいずれかを選択します。  
  
    -   既存のドメインで、追加のドメイン コントローラーをインストールする場合はクリックして**ドメイン コントローラーを既存のドメインに追加**、ドメイン (たとえば、emea.corp.contoso.com) の名前を入力するかをクリックして**を選択しています.**ドメイン、および資格情報を選択する (たとえば、Domain Admins グループのメンバーであるアカウントを指定する)] をクリックし、**次**します。  
  
        > [!NOTE]  
        > 現在のユーザー資格情報およびドメインの名前は、コンピューターがドメインに参加していて、ローカル インストールを実行する場合にのみ、既定で提供されます。 リモート サーバーに AD DS をインストールする場合は、設計によって、資格情報を指定する必要があります。 現在のユーザー資格情報がない場合、インストールを実行するための十分な] をクリックして**変更しています.**別の資格情報を指定するためにします。  
  
        詳細については、次を参照してください[レプリカ Windows Server 2012 ドメイン コントローラーを既存のドメイン (&) #40; でインストール。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md).  
  
    -   新しい子ドメインをインストールする場合、以下の] をクリックして**既存のフォレストに新しいドメインを追加**の**ドメインの種類の選択**[**子ドメイン**入力、または親ドメインの DNS 名 (たとえば、corp.contoso.com) の名前を参照、相対的な新しい子ドメイン (emea など) を使用して、新しいドメインを作成し、をクリックする種類の資格情報の名前を入力**[次へ]**します。  
  
        詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory 子またはツリー ドメイン (&) #40; をインストールする。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   を新しいドメイン ツリーをインストールする場合はクリックして**を既存のフォレストに新しいドメインを追加**、の**ドメインの種類の選択**、選択**ツリー ドメイン**(たとえば、corp.contoso.com) のルート ドメインの名前を入力し、新しいドメイン (たとえば、fabrikam.com) を使用して、新しいドメインを作成し、をクリックする種類の資格情報の DNS 名**[次へ]**します。  
  
        詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory 子またはツリー ドメイン (&) #40; をインストールする。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md).  
  
    -   を新しいフォレストをインストールする場合はクリックして**新しいフォレストの追加**し (たとえば、corp.contoso.com) のルート ドメインの名前を入力します。  
  
        詳細については、次を参照してください[、新しい Windows Server 2012 Active Directory フォレスト (&) #40; をインストールする。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md).  
  
11. **ドメイン コントローラー オプション**] ページで、次のオプションのいずれかを選択します。  
  
    -   新しいフォレストまたはドメインを作成する場合、ドメインおよびフォレストの機能レベルを選択] をクリックして**ドメイン ネーム システム (DNS) サーバー**、DSRM パスワードを指定し、[クリックして**次**します。  
  
    -   既存のドメインにドメイン コントローラーを追加する場合はクリックして**ドメイン ネーム システム (DNS) サーバー**、**グローバル カタログ (GC)**、または**読み取りのみドメイン コントローラー (RODC)**必要に応じて、サイトの名前を選択、DSRM パスワードを入力し、クリックして**[次へ]**します。  
  
    このページのオプションは、または別の条件下で利用できないについての詳細については、次を参照してください。[ドメイン コントローラー オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)します。  
  
12. **DNS オプション**(表示される DNS サーバーをインストールする場合にのみ)] ページで [ **DNS 委任を更新**必要に応じてします。 その場合は、親 DNS ゾーンに DNS 委任レコードを作成するアクセス許可のある資格情報を提供します。  
  
    親ゾーンをホストする DNS サーバーに接続できない場合、**DNS 委任を更新**オプションは使用できません。  
  
    For more information about whether you need to update the DNS delegation, see [Understanding Zone Delegation](https://technet.microsoft.com/library/cc771640.aspx). DNS 委任を更新し、エラーが発生しを参照してくださいしようとする場合[DNS オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)します。  
  
13. **RODC オプション**(が RODC をインストールする場合にのみが表示されます)] ページでは、RODC を管理、または、許可または拒否パスワード レプリケーション グループから、アカウントを削除し、をクリックするアカウントを追加したユーザーまたはグループの名前を指定**次**します。  
  
    For more information, see [Password Replication Policy](https://technet.microsoft.com/library/cc730883(v=ws.10)).  
  
14. **追加オプション**] ページで、次のオプションのいずれかを選択します。  
  
    -   新しい NetBIOS 名を入力新しいドメインを作成する場合は場合、や、ドメインの既定の NetBIOS 名を確認し、をクリックして**次**します。  
  
    -   既存のドメインにドメイン コントローラーを追加する場合は、(またはウィザードに任意のドメイン コントローラーを選択) から AD DS インストール データをレプリケートするドメイン コントローラーを選択します。 メディアからインストールする場合は、クリックして**メディア パスからインストール**入力し、インストール ソース ファイルへのパスを確認し、クリックして**次**します。  
  
        使用することはできません (IFM) をドメインの最初のドメイン コントローラーのインストール メディアからインストールします。 IFM は、別のオペレーティング システム バージョン間では機能しません。 つまり、IFM を使用して Windows Server 2012 を実行する追加のドメイン コントローラーをインストールするために、Windows Server 2012 ドメイン コントローラーでバックアップ メディアを作成する必要があります。 For more information about IFM, see [Installing an Additional Domain Controller by Using IFM](https://technet.microsoft.com/library/cc816722(WS.10).aspx).  
  
15. **パス**ページ、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力 (または既定の場所を受け入れて)] をクリック**次**します。  
  
    > [!IMPORTANT]  
    > Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory データベース、ログ ファイル、または SYSVOL フォルダーを格納しないでください。  
  
16. **準備オプション**ページで、adprep を実行するのに十分な種類の資格情報。 詳細については、次を参照してください。[資格情報の Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)します。  
  
17. **オプションの確認**] ページでクリックし、選択内容を確認**スクリプトの表示**クリックして、Windows PowerShell スクリプトの設定をエクスポートする場合**[次へ]**します。  
  
18. **前提条件のチェック**] ページでその前提条件の検証が完了したことを確認してをクリックして**インストール**します。  
  
19. **結果**ページで、サーバーがドメイン コントローラーとして正しく構成されたことを確認します。 サーバーは、AD DS のインストールを完了する自動的に再起動されます。  
  
## <a name="BKMK_UIStaged"></a>グラフィカル ユーザー インターフェイスを使用してステージング RODC インストールを実行します。  
段階的 RODC のインストールでは、2 つのステージで RODC を作成することができます。 最初のステージでは、Domain Admins グループのメンバーは、RODC アカウントを作成します。 2 番目の段階で、サーバーを RODC アカウントに接続します。 2 番目の段階は、Domain Admins グループまたは委任されたドメイン ユーザーまたはグループのメンバーで完了できます。  
  
#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>Active Directory 管理ツールを使用して RODC アカウントを作成するには  
  
1.  Active Directory 管理センターまたは Active Directory ユーザーとコンピューターを使用して RODC アカウントを作成することができます。  
  
    1.  をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、**Active Directory 管理センター**します。  
  
    2.  ナビゲーション ウィンドウ (左側のウィンドウ) では、ドメインの名前をクリックします。  
  
    3.  管理の一覧 (中央のウィンドウ)] をクリックして、**ドメイン コントローラー** OU です。  
  
    4.  作業ウィンドウ (右側のウィンドウ) で、をクリックして**読み取り専用ドメイン コントローラー アカウントの事前作成**します。  
  
    - または -  
  
    1.  をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、 **Active Directory ユーザーとコンピューター**します。  
  
    2.  いずれかを右クリックし、**ドメイン コントローラー**組織単位 (OU) または] をクリック、**ドメイン コントローラー** OU、] をクリックし、**アクション**します。  
  
    3.  をクリックして**の事前作成 Read-only ドメイン コントローラー アカウント**します。  
  
2.  **Active Directory ドメイン サービス インストール ウィザードへようこそ**] ページで、既定のパスワード レプリケーション ポリシー (PRP)、選択を変更する**詳細モード インストールを使用して**、] をクリックし、**[次へ]**します。  
  
3.  **ネットワーク資格情報**ページで、**を使用して、インストールを実行するアカウントの資格情報を指定**、] をクリックして**[現在のログオン資格情報**] をクリックしてまたは**代替の資格情報**、] をクリックし、**設定**します。 **Windows セキュリティ**] ダイアログ ボックスで、追加のドメイン コントローラーをインストールできるアカウントのユーザー名とパスワードを入力します。 追加のドメイン コントローラーをインストールするには、Enterprise Admins グループまたは Domain Admins グループのメンバーがあります。 資格情報の提供が終了したら、クリックして**次**します。  
  
4.  **コンピューター名を指定**] ページで、RODC となるサーバーのコンピューター名を入力します。  
  
5.  **サイトを選択して**] ページで、一覧からサイトを選択または、ウィザードを実行しているコンピューターの IP アドレスに対応するサイトにドメイン コントローラーをインストールするオプションを選択してをクリックして**次**します。  
  
6.  **追加のドメイン コントローラー オプション**ページ、次の選択を行い、をクリックして**次**:  
  
    -   **DNS サーバー**: ドメイン コントローラーがドメイン ネーム システム (DNS) サーバーとして機能できるように、既定でこのオプションを選択します。 ドメイン コントローラー、DNS サーバーをしたくない場合は、このオプションをオフにします。 ただし、RODC し、RODC 上の DNS サーバーの役割は、ブランチ オフィス内の唯一のドメイン コントローラーをインストールしていない場合は、ブランチ オフィス内のユーザーは、ハブ サイトへのワイド エリア ネットワーク (WAN) がオフラインのときに、名前解決を実行できません。  
  
    -   **グローバル カタログ**: 既定でこのオプションを選択します。 これにより、グローバル カタログ検索機能と、グローバル カタログ ドメイン コントローラーに読み取り専用のディレクトリ パーティションを追加します。 ドメイン コントローラーをグローバル カタログ サーバーをしたくない場合は、このオプションをオフにします。 ただし、ブランチ オフィス内のグローバル カタログ サーバーをインストールしたり、RODC を含んだサイトに対してユニバーサル グループ メンバーシップのキャッシュを有効にするをしない場合、ブランチ オフィス内のユーザーされません、ハブ サイトへの WAN がオフラインのときに、ドメインにログオンできません。  
  
    -   **読み取り専用ドメイン コントローラー**します。 RODC アカウントを作成するときに既定では、このオプションが選択されているし、オフにすることはできません。  
  
7.  選択した場合、**詳細モード インストールを使用して**チェック ボックスをオン、**ようこそ**] ページで、**パスワード レプリケーション ポリシーを指定する**ページが表示されます。 既定では、アカウントのパスワードは、RODC にレプリケートされませんし (Domain Admins グループのメンバー) などのセキュリティの機密性の高いアカウントはパスワードを RODC にレプリケートされることから明示的に拒否します。  
  
    ポリシーに他のアカウントを追加する] をクリックして**追加**、] をクリックし、**、当該 RODC にレプリケートするアカウントのパスワードを許可する**] をクリックしてまたは**当該 RODC にレプリケートするアカウントのパスワードを拒否**し、アカウントを選択します。  
  
    完了すると (または既定の設定を受け入れるように)、] をクリックして**次**します。  
  
8.  **委任の RODC のインストールと管理**] ページで、ユーザーまたはサーバーの関連付けを作成している RODC アカウントに、グループの名前を入力します。 1 つだけのセキュリティ プリンシパルの名前を入力することができます。  
  
    特定のユーザーまたはグループのディレクトリを検索するをクリックして**設定**します。 **[ユーザーまたはグループ**、またはグループのユーザーの名前を入力します。 RODC のインストールとグループの管理に委任することをお勧めします。  
  
    このユーザーまたはグループも必要がローカルの管理者権限 RODC で、インストール後にあります。 ユーザーまたはグループを指定しない場合、Domain Admins グループまたは Enterprise Admins グループのメンバーだけは、アカウントに、サーバーをアタッチすることになります。  
  
    操作が完了したら、クリックして**次**します。  
  
9. **概要**] ページで、選択内容を確認します。 をクリックして**戻る**を必要に応じて、選択した内容を変更します。  
  
    以降の AD DS 操作を自動化は、[使用できる応答ファイルを選択した設定を保存する**設定のエクスポート**します。 応答ファイルの名前を入力し、クリックして**保存**します。  
  
    選択内容が正確であることを確認したら、クリックして**次**RODC アカウントを作成します。  
  
10. **Active Directory ドメイン サービス インストール ウィザードの完了**] ページで [**完了**します。  
  
RODC アカウントが作成されたら、RODC のインストールを完了するアカウントにサーバーをアタッチすることができます。 RODC を配置するブランチ オフィスでは、この 2 番目の段階を完了できます。 この手順を実行するサーバーをドメインに参加していない必要があります。 Windows Server 2012 以降では、する役割の追加ウィザードでサーバー マネージャーを使って、サーバーを RODC アカウントにアタッチします。  
  
#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>サーバー マネージャーを使用して RODC アカウントに、サーバーをアタッチするには  
  
1.  ローカル管理者としてログオンします。  
  
2.  サーバー マネージャーで、クリックして**役割と機能の追加**します。  
  
3.  **開始する前に**] ページで [**次**します。  
  
4.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**] をクリックし、**[次へ]**します。  
  
5.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、クリックして、AD DS をインストールするサーバーの名前をクリックして**[次へ]**します。  
  
6.  **サーバーの役割の選択**] ページで [ **Active Directory Domain Services**、] をクリックして**機能の追加**] をクリックし、**[次へ]**します。  
  
7.  **機能の選択**] ページで、追加機能をインストールし] をクリックする選択**次**します。  
  
8.  **Active Directory Domain Services** ] ページで情報を確認してをクリックして**次**します。  
  
9. **インストール オプションの確認**] ページで [**インストール**します。  
  
10. **結果**] ページで、確認**インストールに成功しました**、] をクリック**このサーバーのドメイン コントローラーを昇格**を Active Directory ドメイン サービス構成ウィザードを開始します。  
  
    > [!IMPORTANT]  
    > 役割の追加ウィザードこの時点でを閉じるには、Active Directory ドメイン サービス構成ウィザードを起動しなくても、サーバー マネージャーでのタスク] をクリックして再開できます。  
  
    (media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)  
  
11. **展開構成**] ページで [**ドメイン コントローラーを既存のドメインに追加**、ドメイン (たとえば、emea.contoso.com) の名前を入力し、資格情報 (たとえば、管理し、RODC のインストールを委任されているアカウント) を指定し、をクリックして**[次へ]**します。  
  
12. **ドメイン コントローラー オプション**ページで、[**既存の RODC アカウントを使用して**のように入力し、ディレクトリ サービス復元モード パスワードを確認し、[クリックして**次**します。  
  
13. **追加オプション**] ページで、メディアからインストールする] をクリックして**メディア パスからインストール**のように入力し、インストール ソース ファイルへのパスを確認する、(またはウィザードに任意のドメイン コントローラーを選択) から AD DS インストール データをレプリケートするドメイン コントローラーを選択し、をクリックして**[次へ]**します。  
  
14. **パス**] ページで Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力または既定の場所を受け入れて、をクリックして**次**します。  
  
15. **オプションの確認**] ページでクリックし、選択内容を確認**スクリプトの表示**、Windows PowerShell スクリプトに、設定をエクスポートし、をクリックして**次**します。  
  
16. **前提条件のチェック**] ページでその前提条件の検証が完了したことを確認してをクリックして**インストール**します。  
  
    AD DS のインストールを完了するには、サーバーは自動的に再起動します。  
  
## <a name="see-also"></a>参照してください。  
[ドメイン コント ローラーの展開のトラブルシューティング](Troubleshooting-Domain-Controller-Deployment.md)  
[Windows Server 2012 の新しい Active Directory フォレスト (&) #40; をインストールします。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)  
[Windows Server 2012 の新しい Active Directory 子またはツリー ドメイン (&) #40; をインストールします。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)  
[既存のドメイン (&) #40; でレプリカ Windows Server 2012 ドメイン コントローラーをインストールします。レベル 200 & #41 です。](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)  
  



