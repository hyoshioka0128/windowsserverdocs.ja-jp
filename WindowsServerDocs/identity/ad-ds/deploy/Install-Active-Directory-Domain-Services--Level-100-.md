---
ms.assetid: ae241ed8-ef19-40a9-b2d5-80b8391551ff
title: Active Directory Domain Services をインストールする (レベル 100)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 179c8e5be0dc539971f449c257f331215937d553
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990438"
---
# <a name="install-active-directory-domain-services-level-100"></a>Active Directory Domain Services をインストールする (レベル 100)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、次のいずれかの方法を使用して、Windows Server 2012 に AD DS をインストールする方法について説明します。

-   [Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための資格情報要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)

-   [Windows PowerShell を使用して AD DS をインストールする](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PS)

-   [サーバー マネージャーを使用して AD DS をインストールする](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_GUI)

-   [グラフィカル ユーザー インターフェイスを使用して RODC の段階的なインストールを実行する](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_UIStaged)

## <a name="credential-requirements-to-run-adprepexe-and-install-active-directory-domain-services"></a><a name="BKMK_Creds"></a>Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための資格情報要件
Adprep.exe を実行して AD DS をインストールするには、次の資格情報が必要です。

-   新しいフォレストをインストールするには、対象のコンピューターにローカルの Administrator としてログオンしている必要があります。

-   新しい子ドメインまたは新しいドメイン ツリーをインストールするには、Enterprise Admins グループのメンバーとしてログオンしている必要があります。

-   既存のドメインに追加のドメイン コントローラーをインストールするには、Domain Admins グループのメンバーである必要があります。

    > [!NOTE]
    > adprep.exe コマンドを個別に実行せず、Windows Server 2012 を実行する最初のドメインコントローラーを既存のドメインまたはフォレストにインストールする場合は、Adprep コマンドを実行するための資格情報を入力するように求められます。 その資格情報の要件は次のとおりです。
    >
    > -   フォレスト内の最初の Windows Server 2012 ドメインコントローラーを導入するには、Enterprise Admins グループ、Schema Admins グループ、およびスキーママスターをホストするドメインの Domain Admins グループのメンバーの資格情報を指定する必要があります。
    > -   最初の Windows Server 2012 ドメインコントローラーをドメインに導入するには、Domain Admins グループのメンバーの資格情報を指定する必要があります。
    > -   フォレストの最初の読み取り専用ドメイン コントローラー (RODC) を導入するには、Enterprise Admins グループのメンバーの資格情報を入力する必要があります。
    >
    >     > [!NOTE]
    >     > Windows Server 2008 または Windows Server 2008 R2 で adprep/rodcprep を既に実行している場合は、Windows Server 2012 用にもう一度実行する必要はありません。

## <a name="installing-ad-ds-by-using-windows-powershell"></a><a name="BKMK_PS"></a>Windows PowerShell を使用して AD DS をインストールする
Windows Server 2012 以降では、Windows PowerShell を使用して AD DS をインストールできます。 Dcpromo.exe は、Windows Server 2012 以降では非推奨とされますが、応答ファイル (dcpromo/unattend: <answerfile> または dcpromo/answer:) を使用して dcpromo.exe を実行でき <answerfile> ます。 このように、応答ファイルを使用して引き続き dcpromo.exe を実行できるため、既存の自動化にリソースを投資した組織で、dcpromo.exe から Windows PowerShell に自動化を移行するための時間を確保できます。 応答ファイルを使用した dcpromo.exe の実行の詳細については、「」を参照してください [https://support.microsoft.com/kb/947034](https://support.microsoft.com/kb/947034) 。

Windows PowerShell を使用した AD DS の削除の詳細については、「[Windows PowerShell を使用して AD DS を削除する](assetId:///99b97af0-aa7e-41ed-8c81-4eee6c03eb4c#BKMK_RemovePS)」を参照してください。

最初に、Windows PowerShell を使用して AD DS の役割を追加します。 次のコマンドは、AD DS のサーバーの役割と、AD DS と AD LDS のサーバー管理ツール ("Active Directory ユーザーとコンピューター" などの GUI ベースのツールと、dcdia.exe などのコマンド ライン ツール) をインストールします。 Windows PowerShell を使用する場合、サーバー管理ツールは既定ではインストールされません。 ローカルサーバーを管理する場合は **"Includemanagementtools**を指定し、リモートサーバーを管理する場合は[リモートサーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=28972)をインストールする必要があります。

```
Install-windowsfeature -name AD-Domain-Services -IncludeManagementTools
<<Windows PowerShell cmdlet and arguments>>
```

AD DS のインストールが完了するまで再起動は要求されません。

インストールの完了後に次のコマンドを実行すると、ADDSDeployment モジュールで使用できるコマンドレットを確認できます。

```
Get-Command -Module ADDSDeployment
```

特定のコマンドレットの引数と構文を確認するには、次のように入力します。

```
Get-Help <cmdlet name>
```

たとえば、使用されていない読み取り専用ドメイン コントローラー (RODC) アカウントを作成するための引数を確認するには、次のように入力します。

```
Get-Help Add-ADDSReadOnlyDomainControllerAccount
```

省略可能な引数は角かっこで囲まれています。

Windows PowerShell コマンドレットの最新のヘルプの例と概念説明をダウンロードすることもできます。 詳しくは、「[about_Updatable_Help](/powershell/module/microsoft.powershell.core/about/about_updatable_help?view=powershell-5.1)」をご覧ください。

Windows PowerShell コマンドレットは、リモート サーバーに対して実行できます。

-   Windows PowerShell では、ADDSDeployment コマンドレットで Invoke コマンドを使用します。 たとえば、contoso.com ドメインの ConDC3 というリモート サーバーに AD DS をインストールするには、次のように入力します。

    ```
    Invoke-Command { Install-ADDSDomainController -DomainName contoso.com -Credential (Get-Credential) } -ComputerName ConDC3
    ```

または

-   サーバー マネージャーで、リモート サーバーを含むサーバー グループを作成します。 リモート サーバーの名前を右クリックし、**[Windows PowerShell]** をクリックします。

以降では、ADDSDeployment モジュールのコマンドレットを実行して AD DS をインストールする方法について説明します。

-   [ADDSDeployment コマンドレットの引数](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)

-   [Windows PowerShell の資格情報を指定する](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSCreds)

-   [テスト コマンドレットを使用する](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_TestCmdlets)

-   [Windows PowerShell を使用して新しいフォレスト ルート ドメインをインストールする](../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSForest)

-   [Windows PowerShell を使用して新しい子ドメインまたはツリー ドメインをインストールする](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSDomain)

-   [Windows PowerShell を使用して追加の (レプリカ) ドメイン コントローラーをインストールする](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_PSReplica)

### <a name="addsdeployment-cmdlet-arguments"></a><a name="BKMK_Params"></a>ADDSDeployment コマンドレットの引数
次の表は、Windows PowerShell の ADDSDeployment コマンドレットの引数の一覧です。 太字の引数は必須です。 dcpromo.exe の対応する引数の名前が Windows PowerShell とは異なる場合は、その名前がかっこ内に示されています。

Windows PowerShell のスイッチは、引数として $TRUE または $FALSE を受け取ります。 既定で $TRUE される引数を指定する必要はありません。

既定値をオーバーライドするには、値を $False にして引数を指定します。 たとえば、**-installdns** は、新しいフォレストのインストール時に指定しないと自動的に実行されるため、新しいフォレストのインストール時に実行されないようにするには、次のように指定する必要があります。**

```
-InstallDNS:$false
```

同様に、 **"installdns**の既定値は $False です。これは、WINDOWS server DNS サーバーをホストしない環境にドメインコントローラーをインストールする場合、dns サーバーをインストールするために次の引数を指定する必要があるためです。

```
-InstallDNS:$true
```


|                                                                                                                 引数                                                                                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **ADPrepCredential <PS Credential> ****注:** ドメインまたはフォレストに最初の Windows Server 2012 ドメインコントローラーをインストールしていて、現在のユーザーの資格情報で操作を実行するのに十分でない場合は必須です。 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    [Get-Credential](/previous-versions/dd315327(v=technet.10)) と PSCredential オブジェクトの規則に従って、Enterprise Admins グループと Schema Admins グループのメンバーである、フォレストを準備できるアカウントを指定します。<p>値が指定されていない場合は、 **"credential**引数の値が使用されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                      AllowDomainControllerReinstall                                                                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    同じ名前を持つ別の書き込み可能ドメイン コントローラー アカウントが検出された場合でも、この書き込み可能ドメイン コントローラーのインストールを続行するかどうかを指定します。<p>**$True** を使用するのは、そのアカウントが現在別の書き込み可能ドメイン コントローラーによって使用されていないことがわかっている場合だけにしてください。<p>既定値は **$False** です。<p>この引数は、RODC に対しては無効です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                           AllowDomainReinstall                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        既存ドメインを作成し直すかどうかを指定します。<p>既定値は **$False** です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
|                                                                                             AllowPasswordReplicationAccountName <文字列 []>                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         パスワードを当該 RODC にレプリケートできるユーザー アカウント、グループ アカウント、およびコンピューター アカウントの名前を指定します。 値を空にしておく場合は、空の文字列 "" を使用します。 既定では、Allowed RODC Password Replication Group のみが許可されます。このグループは、最初は空です。<p>値は、文字列の配列として指定します。 例:<p>コード-AllowPasswordReplicationAccountName "JSmith"、"JSmithPC"、"Branch Users"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                      ApplicationPartitionsToReplicate <string [] >**メモ:** UI には同等のオプションはありません。 UI または IFM を使用してインストールする場合は、すべてのアプリケーション パーティションがレプリケートされます。                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    レプリケートするアプリケーション ディレクトリ パーティションを指定します。 この引数が適用されるのは、**-InstallationMediaPath** 引数を指定してメディアからのインストール (IFM) を行う場合だけです。 既定では、すべてのアプリケーション パーティションがそれぞれのスコープに基づいてレプリケートされます。<p>値は、文字列の配列として指定します。 例:<p>コード<p>-ApplicationPartitionsToReplicate "partition1", "partition2", "partition3"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                                                 Confirm                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        コマンドレットの実行前に確認を求めるメッセージが表示されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                         CreateDnsDelegation **Note:** add-addsreadonlydomaincontroller コマンドレットを実行するときに、この引数を指定することはできません。                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                   ドメイン コントローラーと共にインストールする新しい DNS サーバーを参照する DNS 委任を作成するかどうかを指定します。 Active Directory "統合 DNS のみ" に対して有効です。 委任レコードを作成できるのは、オンラインかつアクセス可能な Microsoft DNS サーバーだけです。 また、トップレベル ドメイン (.com、.gov、.biz、.edu など) または 2 文字の国コード ドメイン (.nz、.au など) のすぐ下にあるドメインの委任レコードは作成できません。<p>既定値は、環境に基づいて自動的に計算されます。                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                 **資格 <PS Credential> 情報****注:** 現在のユーザーの資格情報で操作を実行するには不十分な場合にのみ必要です。                                                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                [Get-Credential](/previous-versions/dd315327(v=technet.10)) と PSCredential オブジェクトの規則に従って、ドメインにログオンできるドメイン アカウントを指定します。<p>値を指定しない場合は、現在のユーザーの資格情報が使用されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                         CriticalReplicationOnly                                                                                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         AD DS のインストール操作において、再起動の前に重要なレプリケーションだけを実行して続行するかどうかを指定します。 重要ではないレプリケーションについては、インストールが完了し、コンピューターが再起動してから実行されます。<p>この引数を使用することはお勧めしません。<p>ユーザー インターフェイス (UI) には、このオプションに対応するものはありません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|                                                                                                          DatabasePath <string>                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                      ドメインデータベースを含むローカルコンピューターの固定ディスク上にあるディレクトリへの完全修飾されていない汎用名前付け規則 (UNC) パスを指定します。たとえば、 **c:\windows\ntds**のように指定します。<p>既定値は **%SYSTEMROOT%\NTDS** です。 **重要:** AD DS データベースとログファイルを弾力性のあるファイルシステム (ReFS) でフォーマットされたボリュームに格納することはできますが、refs でデータをホストする場合、回復性の通常の利点以外に、refs で AD DS をホストするための具体的な利点はありません。                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                                DelegatedAdministratorAccountName <string>                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                RODC のインストールおよび管理を実行できるユーザーまたはグループの名前を指定します。<p>既定では、Domain Admins グループのメンバーのみが RODC を管理できます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                              DenyPasswordReplicationAccountName <文字列 []>                                                                                              |                                                                                                                                                                                                                                                                                                           パスワードが当該 RODC にレプリケートされないユーザー アカウント、グループ アカウント、およびコンピューター アカウントの名前を指定します。 いずれのユーザーやコンピューターについても資格情報のレプリケーションを拒否しない場合は、空の文字列 "" を使用します。 既定では、Administrators、Server Operators、Backup Operators、Account Operators、および Denied RODC Password Replication Group が拒否されます。 Denied RODC Password Replication Group には、Cert Publishers、Domain Admins、Enterprise Admins、Enterprise Domain Controllers、Enterprise Read-Only Domain Controllers、Group Policy Creator Owners、krbtgt アカウント、Schema Admins が既定で含まれます。<p>値は、文字列の配列として指定します。 例:<p>コード<p>-デ Ypasswordreplicationaccountname "RegionalAdmins", "AdminPCs"                                                                                                                                                                                                                                                                                                            |
|                                               DnsDelegationCredential <PS Credential> **Note:** add-addsreadonlydomaincontroller コマンドレットを実行するときに、この引数を指定することはできません。                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      [Get-Credential](/previous-versions/dd315327(v=technet.10)) と PSCredential オブジェクトの規則に従って、DNS 委任を作成するためのユーザー名とパスワードを指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                        DomainMode <DomainMode> {Win2003 &#124; Win2008 &#124; Win2008R2 &#124; Win2012 &#124; Win2012R2}<p>または<p>DomainMode <DomainMode> {2 &#124; 3 &#124; 4 &#124; 5 &#124; 6}                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             新しいドメインの作成時にドメインの機能レベルを指定します。<p>ドメインの機能レベルは、フォレストの機能レベルより低くすることはできませんが、それより高くすることはできます。<p>既定値は自動的に計算され、既存のフォレストの機能レベルか、**-ForestMode** に設定されている値に設定されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|                                                                   **DomainName**<p>Install-ADDSForest コマンドレットと Install-ADDSDomainController コマンドレットで必須。                                                                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     追加のドメイン コントローラーをインストールするドメインの FQDN を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                       **DomainNetbiosName<string>**<p>FQDN のプレフィックス名が 15 文字を超えている場合に Install-ADDSForest で必須。                                                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Install-ADDSForest で使用します。 新しいフォレスト ルート ドメインに NetBIOS 名を割り当てます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                              DomainType <DomainType> {childdomain &#124; treedomain} または {child &#124; tree}                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  作成するドメインの種類を指定します (既存のフォレストの新しいドメイン ツリー、既存のドメインの子、または新しいフォレスト)。<p>DomainType の既定値は ChildDomain です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                                  Force                                                                                                                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             このパラメーターを指定すると、ドメイン コントローラーのインストールおよび追加の際に通常表示される警告が表示されなくなるため、コマンドレットを最後まで実行できます。 スクリプトでインストールを実行する場合に便利です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                        ForestMode <ForestMode> {Win2003 &#124; Win2008 &#124; Win2008R2 &#124; Win2012 &#124; Win2012R2}<p>または<p>ForestMode <ForestMode> {2 &#124; 3 &#124; 4 &#124; 5 &#124; 6}                        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              新しいフォレストの作成時にフォレストの機能レベルを指定します。<p>既定値は Win2012 です。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|                                                                                                          InstallationMediaPath                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 新しいドメイン コントローラーのインストールに使用されるインストール メディアの場所を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                                                                                                                InstallDns                                                                                                                |                                                                                                                                                                                                                                                                                                                      ドメイン コントローラーに DNS サーバー サービスをインストールして構成するかどうかを指定します。<p>新しいフォレストにおける既定値は **$True** で、DNS サーバーがインストールされます。<p>新しい子ドメインまたはドメイン ツリーにおける既定値は、そのドメインの DNS 名が既に親ドメイン (ドメイン ツリーの場合はフォレスト ルート ドメイン) でホストおよび格納されている場合は $True です。<p>既存のドメインにドメイン コントローラーをインストールする場合の既定値は、ドメインの DNS 名が既に現在のドメインでホストおよび格納されている場合は **$True** です。 DNS ドメイン名が Active Directory の外部でホストされている場合の既定値は **$False** で、DNS サーバーはインストールされません。                                                                                                                                                                                                                                                                                                                      |
|                                                                                                             LogPath <string>                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            ローカル コンピューターの固定ディスク上にある、ドメイン ログ ファイルを含んだディレクトリの UNC 表記ではない、完全修飾パスを指定します。たとえば、**C:\Windows\Logs** のように指定します。<p>既定値は **%SYSTEMROOT%\NTDS** です。 **重要:** 弾力性のあるファイルシステム (ReFS) でフォーマットされたデータボリュームに Active Directory ログファイルを格納しないでください。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                             MoveInfrastructureOperationMasterRoleIfNecessary                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                  インフラストラクチャマスター操作マスターの役割 (フレキシブルシングルマスター操作または FSMO とも呼ばれます) を作成しているドメインコントローラーに転送するかどうかを指定します。この役割は、グローバルカタログサーバーで現在ホストされている場合に使用します。また、グローバルカタログサーバーを作成するドメインコントローラーを作成する予定はありません。 作成するドメイン コントローラーにインフラストラクチャ マスターの役割を必要に応じて転送する場合は、このパラメーターを指定します。その場合、インフラストラクチャ マスターの役割を現在の場所に残すには **NoGlobalCatalog** オプションを指定します。                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                **Newdomainname <string> ****注:** Install-ADDSDomain にのみ必要です。                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           新しいドメインの単一のドメイン名を指定します。<p>たとえば、**emea.corp.fabrikam.com** という名前の新しい子ドメインを作成する場合は、この引数の値として **emea** を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                      **NewDomainNetbiosName<string>**<p>FQDN のプレフィックス名が 15 文字を超えている場合に Install-ADDSDomain で必須。                                                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               Install-ADDSDomain で使用します。 新しいドメインに NetBIOS 名を割り当てます。 既定値は、 **"Newdomainname"** の値から派生します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|                                                                                                              NoDnsOnNetwork                                                                                                              |                                                                                                                                                                                                                                                                                                                                    ネットワーク上で DNS サービスが利用できないことを指定します。 このパラメーターは、当該コンピューターのネットワーク アダプターの IP 設定に、名前解決用の DNS サーバーの名前が構成されていない場合にのみ使用されます。 このパラメーターを指定すると、名前解決用に、このコンピューター上に DNS サーバーがインストールされます。 このパラメーターを指定しない場合は、先にネットワーク アダプターの IP 設定に DNS サーバーのアドレスを指定する必要があります。<p>このパラメーターを省略すると (既定値)、当該サーバー コンピューターのネットワーク アダプターの TCP/IP クライアント設定が DNS サーバーとの通信に使用されます。 したがって、このパラメーターを指定しない場合は、先に TCP/IP クライアント設定に優先 DNS サーバーのアドレスを指定する必要があります。                                                                                                                                                                                                                                                                                                                                     |
|                                                                                                             NoGlobalCatalog                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   ドメイン コントローラーをグローバル カタログ サーバーにしないように指定します。<p>Windows Server 2012 を実行するドメインコントローラーは、既定ではグローバルカタログと共にインストールされます。 したがって、次のように指定しない限り、その操作が計算なしで自動的に実行されます。<p>コード<p>-NoGlobalCatalog                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                                                                                                           NoRebootOnCompletion                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     コマンドが正常に終了したかどうかにかかわらず、完了時にコンピューターを再起動するかどうかを指定します。 既定では、コンピューターが再起動します。 サーバーが再起動しないようにするには、次のように指定します。<p>コード<p>-NoRebootOnCompletion: $True<p>ユーザー インターフェイス (UI) には、このオプションに対応するものはありません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
|                                                                              **Parentdomainname <string> ****注:** Install に必要です-ADDSDomain コマンドレット                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 既存の親ドメインの FQDN を指定します。 この引数は、子ドメインまたは新しいドメイン ツリーをインストールするときに使用します。<p>たとえば、**emea.corp.fabrikam.com** という名前の新しい子ドメインを作成する場合は、この引数の値として **corp.fabrikam.com** を指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                                                                                             ReadOnlyReplica                                                                                                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   読み取り専用ドメイン コントローラー (RODC) をインストールするかどうかを指定します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                       ReplicationSourceDC <string>                                                                                                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              ドメイン情報のレプリケート元とするパートナー ドメイン コントローラーの FQDN を指定します。 既定値は自動的に計算されます。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                             **SafeModeAdministratorPassword<securestring>**                                                                                             | セーフ モードまたはそれに準ずるディレクトリ サービス復元モードなどでコンピューターを起動したときの管理者アカウントのパスワードを指定します。<p>既定値は空のパスワードで、 パスワードを指定する必要があります。 パスワードは、System.Security.SecureString 形式 (read-host -assecurestring や ConvertTo-SecureString によって提供される形式) で指定する必要があります。<p>SafeModeAdministratorPassword 引数の操作は特殊です。この引数を指定しない場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。この引数を値なしで指定して、ほかに引数を指定しない場合は、マスクされたパスワードの入力を求められますが、確認入力は求められません。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。この引数を値と共に指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。たとえば、Read-Host コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます (-safemodeadministratorpassword (read-host -prompt "Password:" -assecurestring))。セキュリティで保護された文字列を、変換されるクリア テキストの変数として指定することもできますが、この方法はお勧めしません (-safemodeadministratorpassword (convertto-securestring "Password1" -asplaintext -force))。 |
|                                                                     **SiteName<string>**<p>Add-addsreadonlydomaincontrolleraccount コマンドレットで必須                                                                     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  ドメイン コントローラーのインストール先となるサイトを指定します。 **インストール-ADDSForest**を実行すると、 **"sitename**引数がありません。これは、最初に作成されたサイトが既定の優先名であるためです。<p>**-sitename** に引数として指定するサイト名は既に存在している必要があります。 コマンドレットでは作成されません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|                                                                                                           SkipAutoConfigureDNS                                                                                                           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           DNS クライアント設定、フォワーダー、ルート ヒントの自動構成を省略します。 この引数が有効になるのは、DNS サーバー サービスが既にインストールされているか、**-InstallDNS** で自動的にインストールされる場合だけです。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                            SystemKey <string>                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            データのレプリケート元とするメディアのシステム キーを指定します。<p>既定値は **none** です。<p>データは、read-host -assecurestring や ConvertTo-SecureString によって提供される形式である必要があります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|                                                                                                           SysvolPath <string>                                                                                                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     ローカル コンピューターの固定ディスク上にあるディレクトリの UNC 表記ではない完全修飾パスを指定します。たとえば、**C:\Windows\SYSVOL** のように指定します。<p>既定値は **%SYSTEMROOT%\SYSVOL** です。 **重要:** 回復性のあるファイルシステム (ReFS) でフォーマットされたデータボリュームに SYSVOL を格納することはできません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|                                                                                                              SkipPreChecks                                                                                                               |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              インストールを開始する前に前提条件のチェックを実行しません。 この設定を使用することはお勧めしません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|                                                                                                                  WhatIf                                                                                                                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   コマンドレットの実行時に発生する内容を示します。 このコマンドレットは実行されません。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

### <a name="specifying-windows-powershell-credentials"></a><a name="BKMK_PSCreds"></a>Windows PowerShell の資格情報を指定する
[Get-credential](/previous-versions/dd315327(v=technet.10)) を使用すると、画面にプレーンテキストで表示されないようにして資格情報を指定できます。

-SafeModeAdministratorPassword 引数と LocalAdministratorPassword 引数の操作は特殊です。

-   この引数を指定しない場合は、マスクされたパスワードの入力と確認入力を求められます。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法です。

-   この引数を値と共に指定する場合は、セキュリティで保護された文字列を指定する必要があります。 これは、コマンドレットを対話的に実行する場合に推奨される使用方法ではありません。

たとえば、**Read-Host** コマンドレットを使用してユーザーにセキュリティで保護された文字列の入力を求めることにより、手動でパスワードの入力を求めることができます。

```
-SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString)
```

> [!WARNING]
> この方法ではパスワードの確認入力が行われないため、細心の注意が必要です。パスワードは表示されません。

セキュリティで保護された文字列を、変換されるクリア テキストの変数として指定することもできますが、この方法はお勧めしません。

```
-SafeModeAdministratorPassword (ConvertTo-SecureString "Password1" -AsPlainText -Force)
```

> [!WARNING]
> クリア テキストのパスワードを指定したり格納したりすることはお勧めしません。 このコマンドをスクリプトで実行する人や入力をそばで見ている人に、そのドメイン コントローラーの DSRM パスワードを知られてしまいます。 ドメイン コントローラーの DSRM パスワードがわかれば、ドメイン コントローラーそのものを偽装して、自分の権限を Active Directory フォレストで最も高いレベルに昇格させることができます。

### <a name="using-test-cmdlets"></a><a name="BKMK_TestCmdlets"></a>テスト コマンドレットを使用する
各 ADDSDeployment コマンドレットには、対応するテスト コマンドレットがあります。 テスト コマンドレットでは、そのインストール操作の前提条件のチェックのみが実行されます。インストール設定は構成されません。 各テストコマンドレットの引数は、対応するインストールコマンドレットと同じですが、 **"Skipprechecks**はテストコマンドレットでは使用できません。

|テスト コマンドレット|説明|
|---------------|---------------|
|Test-ADDSForestInstallation|新しい Active Directory フォレストをインストールするための前提条件を確認します。|
|Test-ADDSDomainInstallation|Active Directory の新しいドメインをインストールするための前提条件を確認します。|
|Test-ADDSDomainControllerInstallation|Active Directory のドメイン コントローラーをインストールするための前提条件を確認します。|
|Test-ADDSReadOnlyDomainControllerAccountCreation|読み取り専用ドメイン コントローラー (RODC) アカウントを追加するための前提条件を確認します。|

### <a name="installing-a-new-forest-root-domain-using-windows-powershell"></a><a name="BKMK_PSForest"></a>Windows PowerShell を使用して新しいフォレスト ルート ドメインをインストールする
新しいフォレストをインストールするためのコマンド構文を次に示します。 省略可能な引数は角かっこで囲まれています。

```
Install-ADDSForest [-SkipPreChecks] -DomainName <string> -SafeModeAdministratorPassword <SecureString> [-CreateDNSDelegation] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-DomainNetBIOSName <string>] [-ForestMode <ForestMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [-InstallDNS] [-LogPath <string>] [-NoRebootOnCompletion] [-SkipAutoConfigureDNS] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

> [!NOTE]
> -DomainNetBIOSName 引数は、DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合と、名前が 15 文字を超えている場合に必須です。

たとえば、corp.contoso.com という名前の新しいフォレストをインストールし、安全な方法で DSRM パスワードの入力を求めるには、次のように入力します。

```
Install-ADDSForest -DomainName "corp.contoso.com"
```

> [!NOTE]
> Install-ADDSForest を実行すると、既定で DNS サーバーがインストールされます。

corp.contoso.com という名前の新しいフォレストをインストールし、contoso.com ドメインに DNS 委任を作成し、ドメインの機能レベルを Windows Server 2008 R2 に、フォレストの機能レベルを Windows Server 2008 に設定し、Active Directory データベースと SYSVOL を D:\ ドライブに、ログ ファイルを E:\ ドライブにインストールし、ディレクトリ サービス復元モードのパスワードの入力を求めるには、次のように入力します。

```
Install-ADDSForest -DomainName corp.contoso.com -CreateDNSDelegation -DomainMode Win2008 -ForestMode Win2008R2 -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"
```

### <a name="installing-a-new-child-or-tree-domain-using-windows-powershell"></a><a name="BKMK_PSDomain"></a>Windows PowerShell を使用して新しい子ドメインまたはツリー ドメインをインストールする
新しいドメインをインストールするためのコマンド構文を次に示します。 省略可能な引数は角かっこで囲まれています。

```
Install-ADDSDomain [-SkipPreChecks] -NewDomainName <string> -ParentDomainName <string> -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainReinstall] [-CreateDNSDelegation] [-Credential <PS Credential>] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-DomainMode <DomainMode> {Win2003 | Win2008 | Win2008R2 | Win2012}] [DomainType <DomainType> {Child Domain | TreeDomain} [-InstallDNS] [-LogPath <string>] [-NoGlobalCatalog] [-NewDomainNetBIOSName <string>] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-Systemkey <SecureString>] [-SYSVOLPath] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

> [!NOTE]
> **-credential** 引数は、現在 Enterprise Admins グループのメンバーとしてログオンしていない場合にのみ必須です。
>
> **-NewDomainNetBIOSName** 引数は、DNS ドメイン名のプレフィックスに基づいて自動的に生成される 15 文字の名前を変更する場合と、名前が 15 文字を超えている場合に必須です。

たとえば、corp\EnterpriseAdmin1 の資格情報を使用して child.corp.contoso.com という名前の新しい子ドメインを作成し、DNS サーバーをインストールし、corp.contoso.com ドメインに DNS 委任を作成し、ドメインの機能レベルを Windows Server 2003 に設定し、ドメイン コントローラーを Houston というサイトのグローバル カタログ サーバーにし、DC1.corp.contoso.com をレプリケーション ソース ドメイン コントローラーとして使用し、Active Directory データベースと SYSVOL を D:\ ドライブに、ログ ファイルを E:\ ドライブにインストールし、ディレクトリ サービス復元モードのパスワードの入力のみを求めて確認入力は求めない場合は、次のように入力します。

```
Install-ADDSDomain -SafeModeAdministratorPassword -Credential (get-credential corp\EnterpriseAdmin1) -NewDomainName child -ParentDomainName corp.contoso.com -InstallDNS -CreateDNSDelegation -DomainMode Win2003 -ReplicationSourceDC DC1.corp.contoso.com -SiteName Houston -DatabasePath "d:\NTDS" "SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs" -Confirm:$False
```

### <a name="installing-an-additional-replica-domain-controller-using-windows-powershell"></a><a name="BKMK_PSReplica"></a>Windows PowerShell を使用して追加の (レプリカ) ドメイン コントローラーをインストールする
追加のドメイン コントローラーをインストールするためのコマンド構文を次に示します。 省略可能な引数は角かっこで囲まれています。

```
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-AllowDomainControllerReinstall] [-ApplicationPartitionsToReplicate <string[]>] [-CreateDNSDelegation] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-DNSDelegationCredential <PS Credential>] [-NoDNSOnNetwork] [-NoGlobalCatalog] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SiteName <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

corp.contoso.com ドメインにドメイン コントローラーと DNS サーバーをインストールし、ドメイン管理者の資格情報と DSRM パスワードの入力を求めるには、次のように入力します。

```
Install-ADDSDomainController -Credential (Get-Credential CORP\Administrator) -DomainName "corp.contoso.com"
```

コンピューターが既にドメインに参加していて、ユーザーが Domain Admins グループのメンバーになっている場合は、次のコマンドを使用できます。

```
Install-ADDSDomainController -DomainName "corp.contoso.com"
```

ドメイン名の入力を求めるには、次のように入力します。

```
Install-ADDSDomainController -Credential (Get-Credential) -DomainName (Read-Host "Domain to promote into")
```

次のコマンドは、Contoso\EnterpriseAdmin1 の資格情報を使用して Boston という名前のサイトに書き込み可能ドメイン コントローラーとグローバル カタログ サーバーをインストールし、DNS サーバーをインストールし、contoso.com ドメインに DNS 委任を作成し、c:\ADDS IFM フォルダーに格納されているメディアからのインストールを実行し、Active Directory データベースと SYSVOL を D:\ ドライブに、ログ ファイルを E:\ ドライブにインストールし、AD DS のインストールが完了したらサーバーを自動的に再起動し、ディレクトリ サービス復元モードのパスワードの入力を求めます。

```
Install-ADDSDomainController -Credential (Get-Credential CONTOSO\EnterpriseAdmin1) -CreateDNSDelegation -DomainName corp.contoso.com -SiteName Boston -InstallationMediaPath "c:\ADDS IFM" -DatabasePath "d:\NTDS" -SYSVOLPath "d:\SYSVOL" -LogPath "e:\Logs"
```

### <a name="performing-a-staged-rodc-installation-using-windows-powershell"></a>Windows PowerShell を使用して RODC の段階的なインストールを実行する
RODC アカウントを作成するためのコマンド構文を次に示します。 省略可能な引数は角かっこで囲まれています。

```
Add-ADDSReadOnlyDomainControllerAccount [-SkipPreChecks] -DomainControllerAccuntName <string> -DomainName <string> -SiteName <string> [-AllowPasswordReplicationAccountName <string []>] [-NoGlobalCatalog] [-Credential <PS Credential>] [-DelegatedAdministratorAccountName <string>] [-DenyPasswordReplicationAccountName <string []>] [-InstallDNS] [-ReplicationSourceDC <string>] [-Force] [-WhatIf] [-Confirm] [<Common Parameters>]
```

サーバーを RODC アカウントに関連付けるためのコマンド構文を次に示します。 省略可能な引数は角かっこで囲まれています。

```
Install-ADDSDomainController -DomainName <string> [-SkipPreChecks] -SafeModeAdministratorPassword <SecureString> [-ADPrepCredential <PS Credential>] [-ApplicationPartitionsToReplicate <string[]>] [-Credential <PS Credential>] [-CriticalReplicationOnly] [-DatabasePath <string>] [-NoDNSOnNetwork] [-InstallationMediaPath <string>] [-InstallDNS] [-LogPath <string>] [-MoveInfrastructureOperationMasterRoleIfNecessary] [-NoRebootOnCompletion] [-ReplicationSourceDC <string>] [-SkipAutoConfigureDNS] [-SystemKey <SecureString>] [-SYSVOLPath <string>] [-UseExistingAccount] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]
```

たとえば、RODC1 という名前の RODC アカウントを作成するには、次のように入力します。

```
Add-ADDSReadOnlyDomainControllerAccount -DomainControllerAccountName RODC1 -DomainName corp.contoso.com -SiteName Boston DelegatedAdministratoraccountName PilarA
```

次に、RODC1 アカウントに関連付けるサーバーで、次のコマンドを実行します。 このサーバーをドメインに参加させることはできません。 最初に、AD DS サーバーの役割と管理ツールをインストールします。

```
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools
```

次のコマンドを実行して RODC を作成します。

```
Install-ADDSDomainController -DomainName corp.contoso.com -SafeModeAdministratorPassword (Read-Host -Prompt "DSRM Password:" -AsSecureString) -Credential (Get-Credential Corp\PilarA) -UseExistingAccount
```

確認メッセージが表示されないようにするには、 **Y**キーを押して [引数の**確認]** をクリックします。

## <a name="installing-ad-ds-by-using-server-manager"></a><a name="BKMK_GUI"></a>サーバー マネージャーを使用して AD DS をインストールする
サーバーマネージャーの役割の追加ウィザードを使用して Windows Server 2012 に AD DS をインストールできます。その後、Windows Server 2012 以降の新しい Active Directory Domain Services 構成ウィザードを使用します。 Active Directory ドメインサービスインストールウィザード (dcpromo.exe) は、Windows Server 2012 以降では非推奨とされます。

以降では、AD DS を複数のサーバーにインストールして管理するためにサーバー プールを作成する方法と、ウィザードを使用して AD DS をインストールする方法について説明します。

### <a name="creating-server-pools"></a><a name="BKMK_ServerPools"></a>サーバー プールを作成する
サーバー マネージャーでは、ネットワーク上の他のサーバーをプールすることができます (サーバー マネージャーを実行しているコンピューターからアクセスできる場合)。 プールしたサーバーは、AD DS のリモート インストールなど、サーバー マネージャーで使用できる構成オプションの対象として選択できます。 サーバー マネージャーを実行しているコンピューターは自動的にプールされます。 サーバー プールの詳細については、「[サーバー マネージャーへのサーバーの追加](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831453(v=ws.11))」を参照してください。

> [!NOTE]
> ワークグループ サーバーでサーバー マネージャーを利用してドメインに参加しているコンピューターを管理するには、またはその逆を行うには、追加の構成手順が必要です。 詳細については、「[サーバーマネージャーへのサーバーの追加](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831453(v=ws.11))」の「ワークグループのサーバーの追加と管理」を参照してください。

### <a name="installing-ad-ds"></a><a name="BKMK_installADDSGUI"></a>AD DS をインストールする
**管理資格情報**

AD DS をインストールするための資格情報の要件は、選択する配置構成によって変わります。 詳細については、「[Adprep.exe を実行して Active Directory Domain Services をインストールするための資格情報要件](../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)」を参照してください。

GUI の方法を使用して AD DS をインストールするには、次の手順を実行します。 これらの手順は、ローカルでもリモートでも実行できます。 これらの手順の詳細については、以下のトピックを参照してください。

-   [サーバー マネージャーを使用してフォレストを展開する](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md#BKMK_SMForest)

-   [レプリカ Windows Server 2012 ドメインコントローラーを既存のドメイン &#40;レベル 200&#41;にインストールする](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)

-   [&#40;レベル 200&#41;新しい Windows Server 2012 Active Directory 子ドメインまたはツリードメインをインストールし](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)

-   [RODC&#41; &#40;レベル 200 &#40;Windows Server 2012 Active Directory 読み取り専用ドメインコントローラーをインストール&#41;](../../ad-ds/deploy/RODC/Install-a-Windows-Server-2012-Active-Directory-Read-Only-Domain-Controller--RODC---Level-200-.md)

##### <a name="to-install-ad-ds-by-using-server-manager"></a>サーバー マネージャーを使用して AD DS をインストールするには

1.  サーバー マネージャーで、**[管理]** をクリックし、**[役割と機能の追加]** をクリックして、役割の追加ウィザードを起動します。

2.  **[開始する前に]** ページで、 **[次へ]** をクリックします。

3.  **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** をクリックし、**[次へ]** をクリックします。

4.  **[対象サーバーの選択]** ページで **[サーバー プールからサーバーを選択]** をクリックし、AD DS をインストールするサーバーの名前をクリックしてから、**[次へ]** をクリックします。

    リモート サーバーを選択するには、先にサーバー プールを作成し、そこにリモート サーバーを追加します。 サーバー プールの作成の詳細については、「[サーバー マネージャーへのサーバーの追加](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831453(v=ws.11))」を参照してください。

5.  **[サーバーの役割の選択]** ページで **[Active Directory ドメイン サービス]** をクリックし、**[役割と機能の追加ウィザード]** ダイアログ ボックスで **[機能の追加]** をクリックして、**[次へ]** をクリックします。

6.  **[機能の選択]** ページで、インストールする追加機能を選択し、**[次へ]** をクリックします。

7.  **[Active Directory ドメイン サービス]** ページの情報を確認し、**[次へ]** をクリックします。

8.  **[インストール オプションの確認]** ページで、**[インストール]** をクリックします。

9. **[結果]** ページで、インストールが成功したことを確認し、**[このサーバーをドメイン コントローラーに昇格する]** をクリックして Active Directory ドメイン サービス構成ウィザードを起動します。

    ![AD DS のインストール](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_SMPromotes.gif)

    > [!IMPORTANT]
    > Active Directory ドメイン サービス構成ウィザードを起動せずにこの時点で役割の追加ウィザードを閉じる場合、後からウィザードを再開するには、サーバー マネージャーで [タスク] をクリックします。

    ![AD DS のインストール](media/Install-Active-Directory-Domain-Services--Level-100-/ADDS_SMI_Tasks.gif)

10. **[配置構成]** ページで、次のいずれかのオプションを選択します。

    -   既存のドメインに追加のドメインコントローラーをインストールする場合は、[**既存のドメインにドメインコントローラーを追加する**] をクリックし、ドメインの名前 (emea.corp.contoso.com など) を入力するか、[**選択**] をクリックしてドメインと資格情報を選択します (たとえば、domain Admins グループのメンバーであるアカウントを指定**します)**。

        > [!NOTE]
        > ドメインの名前と現在のユーザーの資格情報が既定で指定されるのは、コンピューターがドメインに参加していて、ローカル インストールを実行している場合だけです。 リモート サーバーに AD DS をインストールする場合は、資格情報を指定する必要があります。これは仕様です。 現在のユーザーの資格情報ではインストールを実行できない場合は、[**変更...** ] をクリックして別の資格情報を指定します。

        詳細については、「 [Install a Replica Windows Server 2012 Domain Controller in a Existing domain &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)」を参照してください。

    -   新しい子ドメインをインストールする場合は、**[新しいドメインを既存のフォレストに追加する]** をクリックします。**[ドメインの種類を選択]** で **[子ドメイン]** を選択して、親ドメインの DNS 名 (corp.contoso.com など) を入力するか参照し、新しい子ドメインの相対名 (emea など) を入力します。新しいドメインを作成するために使用する資格情報を入力し、**[次へ]** をクリックします。

        詳細については、「 [Install a New Windows Server 2012 Active Directory Child Or Tree Domain &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)」を参照してください。

    -   新しいドメイン ツリーをインストールする場合は、**[新しいドメインを既存のフォレストに追加する]** をクリックします。**[ドメインの種類を選択]** で **[ツリー ドメイン]** を選択して、ルート ドメインの名前 (corp.contoso.com など) を入力し、新しいドメインの DNS 名 (fabrikam.com など) を入力します。新しいドメインを作成するために使用する資格情報を入力し、**[次へ]** をクリックします。

        詳細については、「 [Install a New Windows Server 2012 Active Directory Child Or Tree Domain &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md)」を参照してください。

    -   新しいフォレストをインストールする場合は、**[新しいフォレストを追加する]** をクリックし、ルート ドメインの名前 (corp.contoso.com など) を入力します。

        詳細については、「 [Install a New Windows Server 2012 Active Directory Forest &#40;Level 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md)」を参照してください。

11. **[ドメイン コントローラー オプション]** ページで、次のいずれかのオプションを選択します。

    -   新しいフォレストまたはドメインを作成する場合は、ドメインとフォレストの機能レベルを選択し、**[ドメイン ネーム システム (DNS) サーバー]** をクリックします。DSRM パスワードを指定し、**[次へ]** をクリックします。

    -   既存のドメインにドメイン コントローラーを追加する場合は、**[ドメイン ネーム システム (DNS) サーバー]**、**[グローバル カタログ (GC)]**、または **[読み取り専用ドメイン コントローラー (RODC)]** を必要に応じてクリックし、サイト名を選択します。DSRM パスワードを入力し、**[次へ]** をクリックします。

    さまざまな条件の下で利用できる、または利用できない本ページのオプションの詳細については、「[ドメイン コントローラー オプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DCOptionsPage)」を参照してください。

12. **[DNS オプション]** ページ (DNS サーバーをインストールする場合にのみ表示されます) で、必要に応じて **[DNS 委任を更新する]** をクリックします。 クリックした場合は、親 DNS ゾーン内に DNS 委任レコードを作成するアクセス許可がある資格情報を指定します。

    親ゾーンをホストする DNS サーバーに接続できない場合、**[DNS 委任を更新する]** オプションは利用できません。

    DNS 委任を更新する必要があるかどうかの詳細については、「[ゾーンの委任とは](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771640(v=ws.11))」を参照してください。 DNS 委任を更新しようとしてエラーが表示された場合は、「[DNS のオプション](../../ad-ds/deploy/AD-DS-Installation-and-Removal-Wizard-Page-Descriptions.md#BKMK_DNSOptionsPage)」を参照してください。

13. **[RODC オプション]** ページ (RODC をインストールする場合にのみ表示されます) で、この RODC を管理するグループまたはユーザーの名前を指定し、Allowed password replication グループまたは Denied password replication グループのアカウントを追加または削除して、**[次へ]** をクリックします。

    詳細については、「[パスワード レプリケーション ポリシー](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730883(v=ws.10))」を参照してください。

14. **[追加オプション]** ページで、次のいずれかのオプションを選択します。

    -   新しいドメインを作成する場合は、ドメインの新しい NetBIOS 名を入力するか、既定の NetBIOS 名を確認し、**[次へ]** をクリックします。

    -   既存のドメインにドメイン コントローラーを追加する場合は、AD DS インストール データのレプリケート元となるドメイン コントローラーを選択します (またはウィザードに任意のドメイン コントローラーを選択させます)。 メディアからインストールする場合は、**[メディアからのインストール パス]** をクリックし、インストール ソース ファイルのパスを入力および確認して、**[次へ]** をクリックします。

        メディアからのインストール (IFM) は、ドメインの最初のドメイン コントローラーのインストールには使用できません。 IFM は、バージョンが異なるオペレーティング システム間では機能しません。 つまり、IFM を使用して Windows Server 2012 を実行する追加のドメインコントローラーをインストールするには、Windows Server 2012 ドメインコントローラー上にバックアップメディアを作成する必要があります。 IFM の詳細については、[IFM を使用した追加ドメイン コントローラーのインストール](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816722(v=ws.10))に関するトピックを参照してください。

15. **[パス]** ページで、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力し (または既定の場所を受け入れて)、**[次へ]** をクリックします。

    > [!IMPORTANT]
    > Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory データベース、ログ ファイル、または SYSVOL フォルダーを格納しないでください。

16. **[準備オプション]** ページで、adprep を実行するのに十分な資格情報を入力します。 詳細については、「[Adprep.exe を実行して Active Directory Domain Services をインストールするための資格情報要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)」を参照してください。

17. **[オプションの確認]** ページで選択内容を確認し、設定を Windows PowerShell スクリプトにエクスポートする場合は **[スクリプトの表示]** をクリックして、**[次へ]** をクリックします。

18. **[前提条件のチェック]** ページで、前提条件の検証が完了していることを確認し、**[インストール]** をクリックします。

19. **[結果]** ページで、サーバーがドメイン コントローラーとして正しく構成されたことを確認します。 サーバーは、AD DS のインストールを完了するために自動的に再起動します。

## <a name="performing-a-staged-rodc-installation-using-the-graphical-user-interface"></a><a name="BKMK_UIStaged"></a>グラフィカル ユーザー インターフェイスを使用して RODC の段階的なインストールを実行する
RODC の段階的なインストールを使用すると、RODC を 2 段階に分けて作成できます。 1 番目の段階では、Domain Admins グループのメンバーが RODC アカウントを作成します。 2 番目の段階では、その RODC アカウントにサーバーを関連付けます。 2 番目の段階は、Domain Admins グループのメンバーか、委任されたドメイン ユーザーまたはグループが実行できます。

#### <a name="to-create-an-rodc-account-by-using-the-active-directory-management-tools"></a>Active Directory 管理ツールを使用して RODC アカウントを作成するには

1.  Active Directory 管理センターまたは Active Directory ユーザーとコンピューターを使用して RODC アカウントを作成できます。

    1.  **[スタート]** ボタンをクリックし、**[管理ツール]**、**[Active Directory 管理センター]** の順にクリックします。

    2.  ナビゲーション ウィンドウ (左側のウィンドウ) で、ドメインの名前をクリックします。

    3.  管理の一覧 (中央のウィンドウ) で、**[Domain Controllers]** OU をクリックします。

    4.  [タスク] ウィンドウ (右側のウィンドウ) で、**[読み取り専用ドメイン コントローラー アカウントの事前作成]** をクリックします。

    または

    1.  [**スタート**]、[**管理ツール**] の順にクリックし、[**Active Directory ユーザーとコンピュータ**] をクリックします。

    2.  **[Domain Controllers]** 組織単位 (OU) を右クリックするか、**[Domain Controllers]** OU をクリックして **[操作]** をクリックします。

    3.  **[読み取り専用ドメイン コントローラー アカウントの事前作成]** をクリックします。

2.  **[Active Directory ドメイン サービス インストール ウィザードの開始]** ページで、既定のパスワード レプリケーション ポリシー (PRP) を変更する場合は **[詳細モード インストールを使用する]** チェック ボックスをオンにし、**[次へ]** をクリックします。

3.  **[ネットワーク資格情報]** ページの **[インストールを実行するために使用するアカウントの資格情報を指定してください]** で、**[現在のログオン資格情報]** または **[代替の資格情報]** をクリックし、**[設定]** をクリックします。 **[Windows セキュリティ]** ダイアログ ボックスで、追加のドメイン コントローラーをインストールできるアカウントのユーザー名およびパスワードを指定します。 追加のドメイン コントローラーをインストールするには、Enterprise Admins グループまたは Domain Admins グループのメンバーである必要があります。 資格情報を入力し終わったら、**[次へ]** をクリックします。

4.  **[コンピューター名の指定]** ページで、RODC となるサーバーのコンピューター名を入力します。

5.  **[サイトの選択]** ページで、一覧からサイトを選択するか、ウィザードを実行しているコンピューターの IP アドレスに対応するサイト内にドメイン コントローラーをインストールするオプションを選択し、**[次へ]** をクリックします。

6.  **[追加のドメイン コントローラー オプション]** ページで、次の項目を適宜選択してから **[次へ]** をクリックします。

    -   **[DNS サーバー]**: このオプションは、ドメイン コントローラーがドメイン ネーム システム (DNS) サーバーとして機能できるように既定でオンになっています。 ドメイン コントローラーを DNS サーバーとして使用しない場合はオフにします。 ただし、RODC 上に DNS サーバーの役割をインストールしない場合、ブランチ オフィス内にあるドメイン コントローラーがその RODC のみであると、ハブ サイトへのワイド エリア ネットワーク (WAN) がオフラインのときはブランチ オフィス内のユーザーが名前の解決を実行できません。

    -   **[グローバル カタログ]**: このオプションは既定でオンになっています。 これにより、グローバル カタログ、読み取り専用ディレクトリ パーティションがドメイン コントローラーに追加され、グローバル カタログ検索機能が有効になります。 ドメイン コントローラーをグローバル カタログ サーバーにしない場合は、このオプションをオフにします。 ただし、ブランチ オフィス内にグローバル カタログ サーバーを 1 つもインストールしない場合や、該当する RODC を含んだサイトに対してユニバーサル グループ メンバーシップのキャッシュを有効にする場合、ハブ サイトへの WAN がオフラインのときはブランチ オフィス内のユーザーがドメインにログオンできません。

    -   **[読み取り専用ドメイン コントローラー]**: RODC アカウントを作成する場合、このオプションは既定でオンになっており、オフにはできません。

7.  **[Active Directory ドメイン サービス インストール ウィザードの開始]** ページで **[詳細モード インストールを使用する]** チェック ボックスをオンにした場合は、**[パスワード レプリケーション ポリシーの指定]** ページが表示されます。 既定では、アカウントのパスワードは RODC には一切レプリケートされず、セキュリティ上機密性の高いアカウント (Domain Admins グループのメンバーなど) のパスワードが RODC にレプリケートされることは、明示的に拒否されます。

    ポリシーにその他のアカウントを追加するには、**[追加]** をクリックし、**[この RODC に対するアカウントのパスワードのレプリケートを許可する]** をクリックするか、**[この RODC に対するアカウントのパスワードのレプリケートを拒否する]** をクリックしてから、アカウントを選択します。

    完了したら (または既定の設定をそのまま使用する場合は)、**[次へ]** をクリックします。

8.  **[RODC のインストールと管理の委任]** ページで、作成している RODC アカウントに対するサーバーの関連付けを実行するユーザーまたはグループの名前を入力します。 ここで入力できるセキュリティ プリンシパルの名前は 1 つだけです。

    特定のユーザーまたはグループをディレクトリで検索するには、**[設定]** をクリックします。 **[ユーザーまたはグループの選択]** に、ユーザーまたはグループの名前を入力します。 RODC のインストールと管理については、グループに委任することをお勧めします。

    このユーザーまたはグループに、インストール後、当該 RODC 上のローカル管理者権限も付与されます。 ユーザーまたはグループを指定しない場合は、Domain Admins グループまたは Enterprise Admins グループのメンバーだけがサーバーをアカウントに関連付けできます。

    構成し終わったら、 **[次へ]** をクリックします。

9. **[概要]** ページで、選択内容を確認します。 選択内容を変更する場合は、**[戻る]** をクリックします。

    選択した設定内容を、以降の AD DS 操作を自動化するために使用できる応答ファイルに保存するには、**[設定のエクスポート]** をクリックします。 応答ファイルの名前を入力し、**[保存]** をクリックします。

    選択した内容が正しいことを確認したら、**[次へ]** をクリックして RODC アカウントを作成します。

10. **[Active Directory ドメイン サービス インストール ウィザードの完了]** ページで、**[完了]** をクリックします。

RODC アカウントの作成が完了したら、サーバーをアカウントに関連付けて RODC のインストールを完了できます。 この 2 番目の段階は、RODC を配置するブランチ オフィスで実行できます。 この手順を実行するサーバーは、ドメインに参加していない必要があります。 Windows Server 2012 以降では、サーバーマネージャーの役割の追加ウィザードを使用して、サーバーを RODC アカウントに接続します。

#### <a name="to-attach-a-server-to-an-rodc-account-using-server-manager"></a>サーバー マネージャーを使用してサーバーを RODC アカウントに関連付けるには

1.  ローカルの Administrator としてログオンします。

2.  サーバー マネージャーで [**役割と機能の追加**] をクリックします。

3.  **[開始する前に]** ページで、 **[次へ]** をクリックします。

4.  **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** をクリックし、**[次へ]** をクリックします。

5.  **[対象サーバーの選択]** ページで **[サーバー プールからサーバーを選択]** をクリックし、AD DS をインストールするサーバーの名前をクリックしてから、**[次へ]** をクリックします。

6.  **[サーバーの役割の選択]** ページで **[Active Directory ドメイン サービス]** をクリックし、**[機能の追加]** をクリックして、**[次へ]** をクリックします。

7.  **[機能の選択]** ページで、インストールする追加機能を選択し、**[次へ]** をクリックします。

8.  **[Active Directory ドメイン サービス]** ページの情報を確認し、**[次へ]** をクリックします。

9. **[インストール オプションの確認]** ページで、**[インストール]** をクリックします。

10. **[結果]** ページで、インストールが成功したことを確認し****、**[このサーバーをドメイン コントローラーに昇格する]** をクリックして Active Directory ドメイン サービス構成ウィザードを起動します。

    > [!IMPORTANT]
    > Active Directory ドメイン サービス構成ウィザードを起動せずにこの時点で役割の追加ウィザードを閉じる場合、後からウィザードを再開するには、サーバー マネージャーで [タスク] をクリックします。

    (media/Install-Active-Directory-Domain-Service--Level-100-/ADDS_SMI_Tasks.gif)

11. **[配置構成]** ページで、**[既存のドメインにドメイン コントローラーを追加する]** をクリックして、ドメインの名前 (emea.contoso.com など) と資格情報 (RODC の管理とインストールを委任されているアカウントなど) を入力し、**[次へ]** をクリックします。

12. **[ドメイン コントローラー オプション]** ページで、**[既存の RODC アカウントを使用する]** をクリックして、ディレクトリ サービス復元モードのパスワードを入力および確認入力し、**[次へ]** をクリックします。

13. **[追加オプション]** ページで、メディアからインストールする場合は、**[メディアからのインストール パス]** をクリックし、インストール ソース ファイルのパスを入力および確認します。AD DS インストール データのレプリケート元となるドメイン コントローラーを選択し (またはウィザードに任意のドメイン コントローラーを選択させ)、**[次へ]** をクリックします。

14. **[パス]** ページで、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力し (または既定の場所を受け入れて)、**[次へ]** をクリックします。

15. **[オプションの確認]** ページで選択内容を確認し、設定を Windows PowerShell スクリプトにエクスポートする場合は **[スクリプトの表示]** をクリックして、**[次へ]** をクリックします。

16. **[前提条件のチェック]** ページで、前提条件の検証が完了していることを確認し、**[インストール]** をクリックします。

    サーバーは、AD DS のインストールを完了するために自動的に再起動します。

## <a name="see-also"></a>参照
[ドメインコントローラーの展開](Troubleshooting-Domain-Controller-Deployment.md) 
 のトラブルシューティング[新しい Windows Server 2012 Active Directory フォレスト &#40;レベル 200&#41;](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Forest--Level-200-.md) 
 をインストールします。[&#40;レベル 200&#41;新しい Windows Server 2012 Active Directory 子ドメインまたはツリードメインをインストールし](../../ad-ds/deploy/Install-a-New-Windows-Server-2012-Active-Directory-Child-or-Tree-Domain--Level-200-.md) 
[レプリカ Windows Server 2012 ドメインコントローラーを既存のドメイン &#40;レベル 200&#41;にインストールする](../../ad-ds/deploy/Install-a-Replica-Windows-Server-2012-Domain-Controller-in-an-Existing-Domain--Level-200-.md)
