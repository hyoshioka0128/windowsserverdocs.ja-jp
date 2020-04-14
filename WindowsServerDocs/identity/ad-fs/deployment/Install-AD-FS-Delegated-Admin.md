---
ms.assetid: 46725afe-8652-4cd7-928c-93b98f7fbae3
title: ドメイン管理者特権を使用せずに AD FS ファームを作成する
description: AdfsFarm コマンドレットとスクリプトを使用した、委任された管理者資格情報を使用した AD FS ファームの作成
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/01/2020
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1716c1e3684ed09d051970a2ab3b43938b5eeb5e
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269443"
---
# <a name="creating-an-ad-fs-farm-without-domain-admin-privileges"></a>ドメイン管理者特権を使用せずに AD FS ファームを作成する

>適用対象: Windows Server 2019 および2016

## <a name="overview"></a>概要
Windows Server 2016 の AD FS 以降では、ドメイン管理者が Active Directory を準備している場合、フェデレーションサーバーのローカル管理者として AdfsFarm コマンドレットを実行できます。  この記事の次のスクリプトを使用すると、AD を準備できます。  手順は次のとおりです。

1) ドメイン管理者として、スクリプトを実行します (または、Active Directory オブジェクトとアクセス許可を手動で作成します)。
2) このスクリプトは、新しく作成された AD オブジェクトの DN を含む AdminConfiguration オブジェクトを返します。
3) フェデレーションサーバーで、ローカル管理者としてログオンしているときに AdfsFarm コマンドレットを実行し、上記の #2 からオブジェクトを AdminConfiguration パラメーターとして渡します。

## <a name="assumptions"></a>前提条件
- Contoso\localadmin は、フェデレーションサーバー上のドメイン管理者以外の管理者です。
- Contoso\FsSvcAcct は、AD FS サービスアカウントとなるドメインアカウントです。
- Contoso\FsGmsaAcct $ は、AD FS サービスアカウントとなる gMSA アカウントです
- $svcCred は AD FS サービスアカウントの資格情報です
- $localAdminCred は、フェデレーションサーバーのローカル (DA) 以外の管理者アカウントの資格情報です。

## <a name="using-a-domain-account-as-ad-fs-service-account"></a>ドメインアカウントを AD FS サービスアカウントとして使用する
### <a name="prepare-ad"></a>AD の準備
ドメイン管理者として次を実行します。
```
PS:\>$adminConfig=(.\New-AdfsDkmContainer.ps1 -ServiceAccount contoso\fssvcacct -AdfsAdministratorAccount contoso\localadmin)
```
### <a name="sample-output"></a>サンプル出力
```
$adminconfig.DkmContainerDN
CN=9530440c-bc84-4fe6-a3f9-8d60162a7bcf,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com
```
### <a name="create-the-ad-fs-farm"></a>AD FS ファームを作成する
ローカル管理者としてのフェデレーションサーバーで、管理者特権の PowerShell コマンドウィンドウで次のコマンドを実行します。

最初に、フェデレーションサーバー管理者が上記のドメイン管理者と同じ PowerShell セッションを使用していない場合は、上記の出力を使用して adminConfig オブジェクトを再作成します。
```
PS:\>$adminConfig = @{"DKMContainerDn"="CN=9530440c-bc84-4fe6-a3f9-8d60162a7bcf,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com"}
```

次に、ファームを作成します。
```
PS:\>$svcCred = (get-credential)
PS:\>$localAdminCred = (get-credential)
PS:\>Install-AdfsFarm -CertificateThumbprint 270D041785C579D75C1C981DA0F9C36ECFDB65E0 -FederationServiceName "fs.contoso.com" -ServiceAccountCredential $svcCred -Credential $localAdminCred -OverwriteConfiguration -AdminConfiguration $adminConfig -Verbose
```
## <a name="using-a-gmsa-as-the-ad-fs-service-account"></a>AD FS サービスアカウントとしての gMSA の使用
### <a name="prepare-ad"></a>AD の準備
```
PS:\>$adminConfig=(.\New-AdfsDkmContainer.ps1 -ServiceAccount contoso\FsGmsaAcct$ -AdfsAdministratorAccount contoso\localadmin)
```

### <a name="sample-output"></a>サンプル出力
```
$adminconfig.DkmContainerDN
CN=8065f653-af9d-42ff-aec8-56e02be4d5f3,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com
```

### <a name="create-the-ad-fs-farm"></a>AD FS ファームを作成する
ローカル管理者としてのフェデレーションサーバーで、管理者特権の PowerShell コマンドウィンドウで次のコマンドを実行します。

最初に、フェデレーションサーバー管理者が上記のドメイン管理者と同じ PowerShell セッションを使用していない場合は、上記の出力を使用して adminConfig オブジェクトを再作成します。
```
PS:\>$adminConfig = @{"DKMContainerDn"="CN=8065f653-af9d-42ff-aec8-56e02be4d5f3,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com"}
```

次に、ファームを作成します。ローカルコンピューターアカウントと ADFS 管理者アカウントには、gMSA の [パスワードの取得] および [アカウントへの委任] 権限が付与されている必要があることに注意してください。
```
PS:\>$localadminobj = get-aduser "localadmin"
PS:\>$adfsnodecomputeracct = get-adcomputer "contoso_adfs_node"
PS:\>Set-ADServiceAccount -Identity fsgmsaacct -PrincipalsAllowedToRetrieveManagedPassword @( add=$localadmin.sid.value, $computeracct.sid.value) -PrincipalsAllowedToDelegateToAccount @( add=$localadmin.sid.value, $computeracct.sid.value)
PS:\>$localAdminCred = (get-credential)
PS:\>Install-AdfsFarm -CertificateThumbprint 270D041785C579D75C1C981DA0F9C36ECFDB65E0 -FederationServiceName "fs.contoso.com" -Credential $localAdminCred -GroupServiceAccountIdentifier "contoso\fsgmsaacct$" -OverwriteConfiguration -AdminConfiguration $adminConfig
```

## <a name="script-for-preparing-ad"></a>AD を準備するためのスクリプト
次の PowerShell スクリプトを使用すると、上記の例を実行できます。

```
[CmdletBinding(SupportsShouldProcess=$true)]
param (
   [Parameter(Mandatory=$True)]
   [string]$ServiceAccount,
   [Parameter(Mandatory=$True)]
   [string]$AdfsAdministratorAccount
)

$ServiceAccountSplit = $ServiceAccount.Split("\");
if ($ServiceAccountSplit.Length -ne 2)
{
    Write-error "Specify the ServiceAccount identifier in 'domain\username' format"
    exit 1
}

$AdfsAdministratorAccountSplit = $AdfsAdministratorAccount.Split("\");
if ($AdfsAdministratorAccountSplit.Length -ne 2)
{
    Write-error "Specify the AdfsAdministratorAccount identifier in 'domain\username' format"
    exit 1
}

#######################################
## Verify AD module is installed
#######################################
$m = "ActiveDirectory"
if (Get-Module | Where-Object {$_.Name -eq $m})
{
    write-verbose "Module $m is already imported."
}
else
{
    if (Get-Module -ListAvailable | Where-Object {$_.Name -eq $m})
    {
        Import-Module $m -Verbose
    }
    else
    {
        write-error "Module $m was not imported, install the Active Directory RSAT package and retry."
        exit 1
    }
}

push-location ad:

#######################################
## Generate random DKM container name
## The OU Name is a randomly generated Guid
#######################################
[string]$guid = [Guid]::NewGuid()
write-verbose ("OU Name" + $guid)

$ouName = $guid
$initialPath = "CN=Microsoft,CN=Program Data," + (Get-ADDomain).DistinguishedName
$ouPath = "CN=ADFS," + $initialPath
$ou = "CN=" + $ouName + "," + $ouPath

#######################################
## Create DKM container and assign default ACE which allows adfs admin read access
#######################################

if ($pscmdlet.ShouldProcess("$ou", "Creating DKM container and assinging access"))
{
    Write-Verbose ("Creating organizational unit with DN: " + $ou)

    if ($AdfsAdministratorAccount.EndsWith("$"))
    {
        write-verbose "ADFS administrator account passed with $ suffix indicating a computer account"
        $userNameSplit = $AdfsAdministratorAccount.Split("\");
        $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
    }
    else
    {
        write-verbose "ADFS administrator account is a standard AD user"    
        $objUser = New-Object System.Security.Principal.NTAccount($AdfsAdministratorAccount)
        $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
    }

    if ($null -eq (Get-ADObject -Filter {distinguishedName -eq $ouPath}))
    {
        Write-Verbose ("First creating initial path " + $ouPath)
        New-ADObject -Name "ADFS" -Type Container -Path $initialPath
    }

    $acl = get-acl -Path $ouPath
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum

    $acl.AddAccessRule($ace1)
    set-acl -Path $ouPath -AclObject $acl

    New-ADObject -Name $ouName -Type Container -Path $ouPath
}


#######################################
## Grant the following permission to the service account
# Read
# Create Child
# Write Owner
# Delete Tree
# Write DACL
# Write Property
#######################################
if ($ServiceAccount.EndsWith("$"))
{
    write-verbose "service account passed with $ suffix indicating a gMSA"
    $userNameSplit = $ServiceAccount.Split("\");
    $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
}
else
{
    write-verbose "service account is a standard AD user"
    $objUser = New-Object System.Security.Principal.NTAccount($ServiceAccount)
    $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
}

if ($pscmdlet.ShouldProcess("$strSID", "Granting GenericRead, CreateChild, WriteOwner, DeleteTree, WriteDacl and WriteProperty"))
{
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum
    $ace2 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"CreateChild","Allow",$adSecInEnum
    $ace3 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteOwner","Allow",$adSecInEnum
    $ace4 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"DeleteTree","Allow",$adSecInEnum
    $ace5 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteDacl","Allow",$adSecInEnum
    $ace6 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteProperty","Allow",$adSecInEnum

    $acl = get-acl -Path $ou

    $acl.AddAccessRule($ace1)
    $acl.AddAccessRule($ace2)
    $acl.AddAccessRule($ace3)
    $acl.AddAccessRule($ace4)
    $acl.AddAccessRule($ace5)
    $acl.AddAccessRule($ace6)

    $acl.SetOwner($strSID)

    set-acl -Path $ou -AclObject $acl
}

#######################################
## Grant the following permission to the adfs admin account
# Read
# Create Child
# Write Owner
# Delete Tree
# Write DACL
# Write Property
#######################################

if ($AdfsAdministratorAccount.EndsWith("$"))
{
    write-verbose "ADFS administrator account passed with $ suffix indicating a gMSA"
    $userNameSplit = $AdfsAdministratorAccount.Split("\");
    $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
}
else
{
    write-verbose "ADFS administrator account is a standard AD user"
    $objUser = New-Object System.Security.Principal.NTAccount($AdfsAdministratorAccount)
    $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
}

if ($pscmdlet.ShouldProcess("$strSID", "Granting GenericRead, CreateChild, WriteOwner, DeleteTree, WriteDacl and WriteProperty"))
{
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum
    $ace2 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"CreateChild","Allow",$adSecInEnum
    $ace3 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteOwner","Allow",$adSecInEnum
    $ace4 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"DeleteTree","Allow",$adSecInEnum
    $ace5 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteDacl","Allow",$adSecInEnum
    $ace6 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteProperty","Allow",$adSecInEnum

    $acl = get-acl -Path $ou

    $acl.AddAccessRule($ace1)
    $acl.AddAccessRule($ace2)
    $acl.AddAccessRule($ace3)
    $acl.AddAccessRule($ace4)
    $acl.AddAccessRule($ace5)
    $acl.AddAccessRule($ace6)

    $acl.SetOwner($strSID)

    set-acl -Path $ou -AclObject $acl

    $adminConfig = @{"DKMContainerDn"=$ou}

    Write-Output $adminConfig
}

pop-location

```
