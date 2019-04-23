---
title: 管理者以外のユーザーを AD FS の Powershell コマンドレットのアクセスを委任します。
description: これは、結果、AD FS PowerShell コマンドレットの非管理者のアクセス許可を委任する方法が descirbes に文書化します。
author: billmath
ms.author: billmath
manager: daveba
ms.reviewer: zhvolosh
ms.date: 01/31/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 265d22b045011e34192e56bdb970955b601cda56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883563"
---
# <a name="delegate-ad-fs-powershell-commandlet-access-to-non-admin-users"></a>管理者以外のユーザーを AD FS の Powershell コマンドレットのアクセスを委任します。 
既定では、AD FS 管理者が、PowerShell を使用して AD FS の管理を行うことのみできます。 多くの大規模な組織でこのできません実行可能な運用モデルをヘルプ デスク担当者などの他の人物を扱うとき。  

Just Enough Administration (JEA)、お客様は、さまざまな担当者グループに固有コマンドレットを委任できますようになりました。  
このユース ケースの好例がヘルプ デスク担当者に AD FS のクエリには、アカウントのロックアウト状態と、ユーザーを検査すると、AD FS でアカウントのロックアウト状態をリセットを許可します。 この場合、委任が必要となるコマンドレットには。 
- `Get-ADFSAccountActivity`
- `Set-ADFSAccountActivity` 
- `Reset-ADFSAccountLockout` 

この例は、このドキュメントの残りの部分で使用します。 ただしも証明書利用者のパーティのプロパティを設定し、このオプションをオフに、組織内のアプリケーション所有者への委任を許可するようにカスタマイズいずれかのことができます。  


##  <a name="create-the-required-groups-necessary-to-grant-users-permissions"></a>ユーザーのアクセス許可を付与するために必要な必要なグループを作成します。 
1. 作成、[グループ管理サービス アカウント](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)します。 JEA ユーザーが他のコンピューターや web サービスとしてネットワーク リソースにアクセスできるように、gMSA アカウントが使用されます。 ドメイン内のコンピューター上のリソースに対して認証するために使用できるドメイン id を提供します。 GMSA アカウントには、後で、セットアップ時に必要な管理権限が与えられます。 この例では、アカウントを呼び出して**gMSAContoso**します。 
2. Active Directory の作成コマンドを委任する権限を付与する必要があるユーザーとグループを設定できます。 この例では、ヘルプ デスクの担当者に読み取り、更新、および ADFS のロックアウト状態をリセットするアクセス許可が付与されます。 全体としての例では、このグループに言及**JEAContoso**します。 

### <a name="install-the-gmsa-account-on-the-adfs-server"></a>ADFS サーバーで、gMSA アカウントをインストールします。 
ADFS サーバーに対する管理者権限を持つサービス アカウントを作成します。 実行できますまたは long としてリモート ドメイン コント ローラーで、AD RSAT パッケージがインストールされています。  サービス アカウントは、ADFS サーバーと同じフォレストに作成する必要があります。 ファームの構成に、例の値を変更します。 

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

ADFS サーバーで、gMSA アカウントをインストールします。  これは、ファーム内のすべての ADFS ノードで実行する必要があります。 
 
```powershell
Install-ADServiceAccount gMSAcontoso 
```

### <a name="grant-the-gmsa-account-admin-rights"></a>GMSA アカウントの管理者権限を付与します。 
ファーム管理の委任を使用している場合、gMSA アカウント管理者権限を付与が、管理者アクセス権を委任する既存のグループに追加することによって。  
 
ファームが代理管理を使用していない場合、gMSA アカウント管理者権限を付与によってすべての ADFS サーバーのローカル管理グループを作成します。 
 
 
### <a name="create-the-jea-role-file"></a>JEA ロール ファイルを作成します。 
 
メモ帳ファイルには、JEA ロールを作成します。 手順については、ロールを作成するに収録されて[JEA ロール機能](https://docs.microsoft.com/powershell/jea/role-capabilities)します。 
 
この例では委任コマンドレットは`Reset-AdfsAccountLockout, Get-ADFSAccountActivity, and Set-ADFSAccountActivity`します。 

サンプルの JEA ロール 'リセット ADFSAccountLockout'、' Get-ADFSAccountActivity' および' セット ADFSAccountActivity' コマンドレットへのアクセスを委任する:

```powershell
@{
GUID = 'b35d3985-9063-4de5-81f8-241be1f56b52'
ModulesToImport = 'adfs'
VisibleCmdlets = 'Reset-AdfsAccountLockout', 'Get-ADFSAccountActivity', 'Set-ADFSAccountActivity'
}
```


### <a name="create-the-jea-session-configuration-file"></a>JEA セッション構成ファイルを作成します。 
作成する手順に従って、 [JEA セッション構成](https://docs.microsoft.com/powershell/jea/session-configurations)ファイル。 構成ファイルは、JEA エンドポイントを使用できるユーザーおよびへのアクセスがどのような機能を決定します。 

ロール機能は、ロール機能ファイルのフラットな名前 (拡張子を除いたファイル名) を参照します。 複数のロール機能が同じフラットな名前を持つシステムで使用できる場合は、PowerShell は暗黙的な検索順序を使用して、有効なロール機能ファイルを選択します。 同じ名前を持つすべてのロール機能ファイルへもアクセスは与えられません。 

パスを使用して、ロール機能ファイルを指定するには、使用、`RoleCapabilityFiles`引数。 サブフォルダー、JEA が含まれている有効な Powershell モジュールの検索、`RoleCapabilities`サブフォルダー、場所、`RoleCapabilityFiles`に引数を変更する必要があります`RoleCapabilities`します。 

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
 
強くお勧めします[、セッション構成ファイルをテスト](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Test-PSSessionConfigurationFile?view=powershell-5.1)pssc ファイルを手動で編集した場合は正しいがテキスト エディターを使用して、構文を確認します。 セッション構成ファイルがこのテストに合格していない場合は、登録されていない正常にシステムに。  
 
### <a name="install-the-jea-session-configuration-on-the-ad-fs-server"></a>AD FS サーバーで、JEA セッション構成をインストールします。 

AD FS サーバーで、JEA セッション構成をインストールします。 
 
```powershell
Register-PSSessionConfiguration -Path .\JEASessionConfig.pssc -name "AccountActivityAdministration" -force
``` 
## <a name="operational-instructions"></a>運用の処理 
セットアップ後、JEA のログ記録と監査に使用できる特定の場合は、適切なユーザーが JEA エンドポイントにアクセスします。 

委任されたコマンドを使用するには。 

```powershell
Enter-pssession -ComputerName server01.contoso.com -ConfigurationName "AccountActivityAdministration" -Credential <User Using JEA> 
Get-AdfsAccountActivity <User> 
```
