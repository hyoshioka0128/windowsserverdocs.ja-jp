---
title: AD FS Powershell コマンドレットへのアクセスを管理者以外のユーザーに委任する
description: このドキュメントでは、AD FS PowerShell コマンドレットの管理者以外にアクセス許可を委任する方法について説明します。
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f4b8f09e5c75f3b9086847a47d33bd76775f3cd1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865500"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>AD FS Powershell コマンドレットへのアクセスを管理者以外のユーザーに委任する 
既定では、PowerShell を使用した AD FS 管理は、AD FS の管理者のみが実行できます。 多くの大規模な組織では、これは、ヘルプデスク担当者などの他のペルソナを扱うときに実行可能な運用モデルではない可能性があります。  

十分な管理 (JEA) だけで、お客様は特定のコマンドレットを異なる担当者グループに委任できるようになりました。  
このユースケースの好例として、ユーザーが吟味された後に、ヘルプデスク担当者が AD FS アカウントのロックアウト状態を照会し、AD FS でアカウントロックアウト状態をリセットできるようにすることが挙げられます。 この場合、コマンドレットを委任する必要があります。 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

この例は、このドキュメントの残りの部分で使用します。 ただし、これをカスタマイズして、委任によって証明書利用者のプロパティを設定し、それを組織内のアプリケーション所有者に渡すこともできます。  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>ユーザーにアクセス許可を付与するために必要なグループを作成する 
1. グループの管理された[サービスアカウント](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)を作成します。 GMSA アカウントは、JEA ユーザーが他のコンピューターや web サービスとしてネットワークリソースにアクセスできるようにするために使用されます。 ドメイン内の任意のコンピューター上のリソースに対する認証に使用できるドメイン id を提供します。 GMSA アカウントには、後でセットアップで必要な管理者権限が付与されます。 この例では、アカウント**gMSAContoso**を呼び出します。 
2. Active Directory グループを作成するには、委任されたコマンドへの権限を付与する必要があるユーザーを設定します。 この例では、ヘルプデスク担当者に、ADFS ロックアウト状態の読み取り、更新、およびリセットを行うためのアクセス許可が付与されています。 このグループは、例の**JEAContoso**と呼ばれています。 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>ADFS サーバーに gMSA アカウントをインストールします。 
ADFS サーバーに対する管理者権限を持つサービスアカウントを作成します。 これは、AD RSAT パッケージがインストールされている限り、ドメインコントローラーまたはリモートで実行できます。  サービスアカウントは、ADFS サーバーと同じフォレストに作成する必要があります。 例の値をファームの構成に変更します。 

```powershell
 # This command should only be run if this is the first time gMSA accounts are enabled in the forest 
Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))  
 
# Run this on every node that you want to have JEA configured on  
$adfsServer = Get-ADComputer server01.contoso.com  
 
# Run targeted at domain controller  
$serviceaccount = New-ADServiceAccount gMSAcontoso -DNSHostName <FQDN of the domain containing the KDS key> - PrincipalsAllowedToRetrieveManagedPassword $adfsServer –passthru 
 
# Run this on every node 
Add-ADComputerServiceAccount -Identity server01.contoso.com -ServiceAccount $ServiceAccount 
```

ADFS サーバーに gMSA アカウントをインストールします。  これは、ファーム内のすべての ADFS ノードで実行する必要があります。 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>GMSA アカウントに管理者権限を付与する 
ファームで代理管理を使用している場合は、管理者アクセスが委任されている既存のグループに gMSA アカウントの管理者権限を追加して付与します。  
 
ファームで代理管理を使用していない場合は、すべての ADFS サーバーでローカル管理グループを作成して、gMSA アカウントに管理者権限を付与します。 
 
 
### <a name="create-the-jea-role-file"></a>JEA ロールファイルを作成する 
 
AD FS サーバーで、メモ帳ファイルに JEA ロールを作成します。 ロールを作成する手順については、 [Jea ロール機能](https://docs.microsoft.com/powershell/jea/role-capabilities)に関する説明を参照してください。 
 
この例で委任されたコマンド`Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`レットは、です。 

サンプル JEA ロールは、' ADFSAccountLockout '、' ADFSAccountActivity '、および ' ADFSAccountActivity ' コマンドレットのアクセスを委任します。

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>JEA セッション構成ファイルを作成する 
手順に従って[Jea セッション構成](https://docs.microsoft.com/powershell/jea/session-configurations)ファイルを作成します。 この構成ファイルによって、JEA エンドポイントを使用できるユーザーと、ユーザーがアクセスできる機能が決まります。 

ロール機能は、ロール機能ファイルのフラット名 (拡張子なしのファイル名) によって参照されます。 同じフラット名を持つシステムで複数のロール機能を使用できる場合、PowerShell は暗黙的な検索順序を使用して有効なロール機能ファイルを選択します。 同じ名前のすべてのロール機能ファイルへのアクセス権は付与されません。 

パスでロール機能ファイルを指定するには、 `RoleCapabilityFiles`引数を使用します。 サブフォルダーの場合、jea は、 `RoleCapabilities`サブフォルダーを含む有効な Powershell モジュールを検索`RoleCapabilities`します。 `RoleCapabilityFiles`ここで、引数をに変更する必要があります。 

セッション構成ファイルのサンプル: 

```powershell
@{
SchemaVersion = '2.0.0.0'
GUID = '54c8d41b-6425-46ac-a2eb-8c0184d9c6e6'
SessionType = 'RestrictedRemoteServer'
GroupManagedServiceAccount =  'CONTOSO\gMSAcontoso'
RoleDefinitions = @{ JEAcontoso = @{ RoleCapabilityFiles = 'C:\Program Files\WindowsPowershell\Modules\AccountActivityJEA\RoleCapabilities\JEAAccountActivityResetRole.psrc' } }
}
```

セッション構成ファイルを保存します。 
 
構文が正しいことを確認するために、テキストエディターを使用して手動で .pssc ファイルを編集した場合は、[セッション構成ファイルをテスト](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1)することを強くお勧めします。 セッション構成ファイルがこのテストに合格しなかった場合は、システムに正常に登録されません。  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>AD FS サーバーに JEA セッション構成をインストールする 

AD FS サーバーに JEA セッション構成をインストールする 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>操作手順 
セットアップが完了したら、JEA のログ記録と監査を使用して、適切なユーザーが JEA エンドポイントにアクセスできるかどうかを判断できます。 

委任されたコマンドを使用するには: 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 


```
