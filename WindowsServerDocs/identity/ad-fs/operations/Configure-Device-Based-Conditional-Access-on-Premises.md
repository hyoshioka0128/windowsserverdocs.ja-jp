---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: オンプレミスのデバイス ベースの条件付きアクセスを構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a7646144b591fd7327f881cb54489201140e9287
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358149"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>登録済みデバイスを使用したオンプレミスの条件付きアクセスの構成


次のドキュメントでは、登録されたデバイスでオンプレミスの条件付きアクセスをインストールして構成する手順について説明します。

![条件付きアクセス](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>インフラストラクチャの前提条件
オンプレミスの条件付きアクセスを開始するには、次の前提条件が必要です。 

|要件|説明
|-----|-----
|Azure AD Premium を使用した Azure AD サブスクリプション | オンプレミスの条件付きアクセスに対してデバイスの書き戻しを有効にするに[は、無料試用版に問題があり](https://azure.microsoft.com/trial/get-started-active-directory/)ます  
|Intune サブスクリプション|デバイスコンプライアンスシナリオの MDM 統合にのみ必要です。[無料試用版には問題あり](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)ません
|Azure AD Connect|2015年11月の QFE 以降。  [ここで](https://www.microsoft.com/en-us/download/details.aspx?id=47594)最新バージョンを入手してください。  
|Windows Server 2016|AD FS のビルド10586以降  
|Windows Server 2016 Active Directory スキーマ|スキーマレベル85以上が必要です。
|Windows Server 2016 ドメインコントローラー|これは、Hello For Business のキー信頼のデプロイにのみ必要です。  詳細については、[こちら](https://aka.ms/whfbdocs)を参照してください。  
|Windows 10 クライアント|上記のドメインに参加しているビルド10586以降は、Windows 10 ドメインへの参加と Microsoft Passport for Work のシナリオにのみ必要です  
|Azure AD Premium ライセンスが割り当てられているユーザーアカウントを Azure AD|デバイスを登録する場合  


 
## <a name="upgrade-your-active-directory-schema"></a>Active Directory スキーマをアップグレードする
登録済みデバイスでオンプレミスの条件付きアクセスを使用するには、最初に AD スキーマをアップグレードする必要があります。  次の条件を満たす必要があります。
    - スキーマはバージョン85以降である必要があります
    - これは、AD FS が参加しているフォレストに対してのみ必要です。

> [!NOTE]
> Windows Server 2016 でスキーマバージョン (レベル85以上) にアップグレードする前に Azure AD Connect をインストールした場合は、Azure AD Connect インストールを再実行し、オンプレミスの AD スキーマを更新して、の同期規則を確認する必要があります。' KeyCredentialLink ' が構成されています。

### <a name="verify-your-schema-level"></a>スキーマレベルを確認する
スキーマレベルを確認するには、次の手順を実行します。

1.  ADSIEdit または LDP を使用して、スキーマの名前付けコンテキストに接続することができます。  
2.  ADSIEdit を使用して、"CN = Schema, CN = Configuration, DC =<domain>, DC =<com> を右クリックし、[プロパティ] を選択します。  フォレスト情報がある relpace のドメインと com 部分。
3.  属性エディターの下で、objectVersion 属性を見つけ、そのバージョンを確認します。  

![ADSI エディター](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

次の PowerShell コマンドレットを使用することもできます (オブジェクトはスキーマの名前付けコンテキスト情報に置き換えてください)。

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

アップグレードの詳細については、「[ドメインコントローラーを Windows Server 2016 にアップグレードする](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md)」を参照してください。 

## <a name="enable-azure-ad-device-registration"></a>Azure AD Device Registration を有効にします。  
このシナリオを構成するには、Azure AD でデバイス登録機能を構成する必要があります。  

これを行うには、「[組織内の Azure AD 参加](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-setup/)をセットアップする」の手順に従います。  

## <a name="setup-ad-fs"></a>セットアップ AD FS  
1. [新しい AD FS 2016 ファーム](https://technet.microsoft.com/library/dn486775.aspx)を作成します。   
2.  または AD FS 2012 R2 から AD FS 2016 にファームを[移行](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)する  
4. AD FS を Azure AD に接続するには、カスタムパスを使用して[Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/)をデプロイします。  

## <a name="configure-device-write-back-and-device-authentication"></a>デバイスのライトバックとデバイスの認証を構成する  
> [!NOTE]
> 高速設定を使用して Azure AD Connect を実行した場合は、正しい AD オブジェクトが作成されています。  ただし、ほとんどの AD FS シナリオでは、AD FS を構成するためにカスタム設定を使用して Azure AD Connect を実行しているため、以下の手順を実行する必要があります。  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>AD FS デバイス認証用の AD オブジェクトの作成  
AD FS ファームがまだデバイス認証用に構成されていない場合 (これは AD FS 管理コンソールで [サービス] の [デバイスの登録] から確認できます)、以下の手順に従って適切な AD DS オブジェクトと構成を作成します。  

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>注: 次のコマンドは、Active Directory 管理ツールを必要と、ので場合は、フェデレーション サーバーは、また、ドメイン コント ローラーではない、まずツールをインストール、1 次の手順を使用しています。  それ以外の場合、手順 1. を省略できます。  

1.  **役割と機能の追加**ウィザードを実行して、 **[リモート サーバー管理ツール]**  ->  **[役割管理ツール]**  ->  **[AD DS および AD LDS ツール]** の機能を選択し、 **[Windows PowerShell の Active Directory モジュール]** と **[AD DS ツール]** の両方を選択します。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2. AD FS プライマリサーバーで、Enterprise Admin (EA) 特権を使用して AD DS ユーザーとしてログインしていることを確認し、管理者特権の powershell プロンプトを開きます。  次に、次の PowerShell コマンドを実行します。  
    
   `Import-module activedirectory`  
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3. ポップアップウィンドウで [はい] をクリックします。

>注: AD FS サービスが GMSA アカウントを使用するように構成されている場合は、アカウント名を "\\ アカウント名 $" の形式で入力します。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

上記の PSH によって、次のオブジェクトが作成されます。  


- AD ドメイン パーティションの RegisteredDevices コンテナー  
- [構成] --> [サービス] --> [Device Registration Configuration] の Device Registration Configuration コンテナーとオブジェクト  
- [構成] --> [サービス] --> [Device Registration Configuration] の Device Registration Configuration DKM コンテナーとオブジェクト  

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4. これが完了すると、正常に完了したことを示すメッセージが表示されます。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>AD 内のサービス接続ポイント (SCP) の作成します。  
ここで説明されているように、Windows 10 のドメインへの参加 (Azure AD への自動登録) を使用する場合は、以下のコマンドを実行して AD DS にサービス接続ポイントを作成します。  
1.  Windows PowerShell を開き、次のコマンドを実行します。
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>注: 必要に応じて、Azure AD Connect サーバーから AdSyncPrep. hbase-runner.psm1 ファイルをコピーします。  このファイルは、Program Files\Microsoft Azure Active Directory Connect\AdPrep にあります。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Azure AD の全体管理者の資格情報を入力します。  

    `PS C:>$aadAdminCred = Get-Credential`

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3. 次の PowerShell コマンドを実行します。 

   `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

ここで、[AD connector account name] は、オンプレミス AD DS ディレクトリを追加するときに、Azure AD Connect で構成したアカウントの名前です。
  
上記のコマンドは、AD DS に serviceConnectionpoint オブジェクトを作成することで、Windows 10 クライアントが参加する適切な Azure AD ドメインを検索できるようにします。  

### <a name="prepare-ad-for-device-write-back"></a>デバイスの書き戻しのための AD の準備   
AD DS オブジェクトおよびコンテナーが Azure AD からのデバイスの書き戻しに対して適切な状態であることを確認するには、次の操作を行います。

1.  Windows PowerShell を開き、次のコマンドを実行します。  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

ここで、[AD connector account name] は、オンプレミス AD DS ディレクトリを追加するときに、Azure AD Connect で構成した domain \accountname 形式のアカウントの名前です。  

上記のコマンドは、AD DS へのデバイスの書き戻しのために以下のオブジェクトを作成し (存在しない場合)、指定された AD コネクタ アカウント名へのアクセスを許可します。  

- AD ドメイン パーティションの RegisteredDevices コンテナー  
- [構成] --> [サービス] --> [Device Registration Configuration] の Device Registration Configuration コンテナーとオブジェクト  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>Azure AD Connect でのデバイスの書き戻しの有効化  
まだ行っていない場合は、Azure AD Connect でデバイスの書き戻しを有効にします。そのために、もう一度ウィザードを実行して **[同期オプションのカスタマイズ]** を選択した後、デバイスの書き戻しのチェック ボックスをオンにし、上記コマンドレットを実行したフォレストを選択します。  

### <a name="configure-device-authentication-in-ad-fs"></a>AD FS でデバイス認証を構成する  
管理者特権の PowerShell コマンド ウィンドウを使用し、次のコマンドを実行して AD FS ポリシーを構成します。  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>構成を確認する  
参考までに、デバイスの書き戻しと認証の動作に必要な AD DS デバイス、コンテナー、アクセス許可の一覧を以下に示します。
 


- CN=RegisteredDevices,DC=&lt;ドメイン&gt; の ms-DS-DeviceContainer 型のオブジェクト        
    - AD FS サービス アカウントへの読み取りアクセス権   
    - Azure AD Connect sync AD コネクタ アカウントへの読み取り/書き込みアクセス権</br></br>

- Container CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=&lt;ドメイン&gt;  
- 上記のコンテナーの下で、デバイスの登録サービス コンテナー DKM

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- CN=&lt;guid&gt;, CN=Device Registration の serviceConnectionpoint 型のオブジェクト

- Configuration,CN=Services,CN=Configuration,DC=&lt;ドメイン&gt;  
  - 新しいオブジェクトで指定された AD コネクタ アカウント名への読み取り/書き込みアクセス権</br></br> 


- DeviceRegistrationServiceContainer のオブジェクトは、CN = Device Registration Services, CN = Device Registration Configuration, CN = Services, CN = Configuration, DC = & ltdomain >  


- 上記のコンテナー内の msDS-DeviceRegistrationService 型のオブジェクト  

### <a name="see-it-work"></a>It の仕事を見る  
新しい要求とポリシーを評価するには、まずデバイスを登録します。  たとえば、> [バージョン情報] の下にある [設定] アプリを使用して Windows 10 コンピューターに参加 Azure AD ことができ[ます。また](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)、追加の手順に従って、windows 10 ドメイン参加と自動デバイス登録をセットアップすることもできます。  Windows 10 mobile デバイスの参加の詳細については、[こちら](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)のドキュメントを参照してください。  

最も簡単な評価を行うには、クレームの一覧を表示するテストアプリケーションを使用して AD FS にサインオンします。 IsManaged、Ismanaged、trusttype を含む新しい要求を表示できるようになります。  作業の Microsoft Passport を有効にした場合は要求 prt も表示されます。  
 

## <a name="configure-additional-scenarios"></a>その他のシナリオを構成します。  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>Windows 10 ドメインに参加しているコンピューターの自動登録  
Windows 10 ドメインに参加しているコンピューターの自動デバイス登録を有効にするには、[こちら](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)の手順 1. と 2. に従います。   
これは、次のことを実現するのに役立ちます。  

1. AD DS のサービス接続ポイントが存在し、適切なアクセス許可を持っていることを確認します (上記のオブジェクトを作成しましたが、二重チェックには害がありません)。  
2. AD FS が正しく構成されていることを確認する  
3. AD FS システムに正しいエンドポイントが有効になっていること、および要求規則が構成されていることを確認する   
4. ドメイン参加済みコンピューターの自動デバイス登録に必要なグループポリシー設定を構成する   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Microsoft Passport for Work で Windows 10 を有効にする方法の詳細については、「[組織内の Microsoft Passport for Work を有効にする](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)」を参照してください。  

### <a name="automatic-mdm-enrollment"></a>MDM の自動登録   
登録済みデバイスの MDM の自動登録を有効にして、アクセス制御ポリシーで isCompliant の要求を使用できるようにするには、こちらの手順に従って[ください。](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>トラブルシューティング  
1.  "drs サービスオブジェクトが見つかりましたが、必要な属性がありません" など、既に存在しているオブジェクトが誤った状態にあるという `Initialize-ADDeviceRegistration` エラーが発生した場合は、以前に Azure AD Connect powershell コマンドを実行し、AD DS で部分的な構成を行っている可能性があります。  **Cn = Device Registration configuration、cn = Services、CN = Configuration、DC =&lt;domain&gt;** のオブジェクトを手動で削除して、もう一度試してみてください。  
2.  Windows 10 ドメインに追加のクライアント  
    1. デバイスの認証が機能していることを確認するには、ドメインに参加しているクライアントにテストユーザーアカウントとしてサインオンします。 プロビジョニングをすばやくトリガーするには、デスクトップを少なくとも1回ロックしてロックを解除します。   
    2. AD DS オブジェクトの stk キー資格情報のリンクを確認する手順 (同期は2回実行する必要がありますか)  
3.  デバイスが既に登録されているが、まだデバイスを登録していない、または登録していない Windows コンピューターを登録しようとするとエラーが発生する場合は、レジストリにデバイス登録構成のフラグメントが含まれている可能性があります。  調査し、これを削除するには、次の手順を使用します。  
    1. Windows コンピューターで、Regedit を開き、 **HKLM\Software\Microsoft\Enrollments**に移動します。   
    2. このキーの下のサブキーがあります多く GUID 形式でします。  最大17の値を持ち、"6" の "EnrollmentType" (MDM 参加済み) または "13" (Azure AD 結合) のサブキーに移動します。  
    3. **EnrollmentType**を**0**に変更します。 
    4. デバイスの登録または登録をもう一度やり直してください。  

### <a name="related-articles"></a>関連資料  
* [Office 365 および Azure Active Directory に接続されているその他のアプリへのアクセスのセキュリティ保護](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)  
* [Office 365 サービスの条件付きアクセスデバイスポリシー](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Azure Active Directory Device Registration を使用したオンプレミスの条件付きアクセスの設定](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [Windows 10 エクスペリエンスのためにドメイン参加済みデバイスを Azure AD に接続する](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
