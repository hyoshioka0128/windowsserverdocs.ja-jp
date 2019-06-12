---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: オンプレミスのデバイス ベースの条件付きアクセスを構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bcb6c415aae33b9742d7a7080ec169ca947098b9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445001"
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>登録済みデバイスを使用して、構成、オンプレミスの条件付きアクセス


次のドキュメントはのインストールと登録済みデバイスとオンプレミスの条件付きアクセスを構成する手順を紹介します。

![条件付きアクセス](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>インフラストラクチャの前提条件
オンプレミスの条件付きアクセスを始める前に、ごとの前提条件は次が必要です。 

|要件|説明
|-----|-----
|Azure AD Premium の Azure AD サブスクリプション | オンプレミスの条件付きアクセス - 上のデバイスの書き込みを有効にする[無料評価版は正常](https://azure.microsoft.com/trial/get-started-active-directory/)  
|Intune サブスクリプション|デバイス コンプライアンスのシナリオ - MDM 統合に必要なだけ[無料評価版は正常](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD Connect|2015 年 11 月 QFE またはそれ以降。  最新バージョンの取得[ここ](https://www.microsoft.com/en-us/download/details.aspx?id=47594)します。  
|Windows Server 2016|ビルド 10586 以降の AD FS  
|Windows Server 2016 の Active Directory スキーマ|スキーマ レベルが 85 以上が必要です。
|Windows Server 2016 のドメイン コント ローラー|これはこんにちは For Business のキーに信頼された展開に必要です。  追加情報をご覧[ここ](https://aka.ms/whfbdocs)します。  
|Windows 10 クライアント|ビルド 10586 または新しい、上記のドメインに参加しているが Windows 10 ドメインに参加し、Microsoft Passport の作業シナリオのみ必要です。  
|Azure AD Premium ライセンスが割り当てられて使用の azure AD ユーザー アカウント|デバイスを登録します。  


 
## <a name="upgrade-your-active-directory-schema"></a>Active Directory スキーマをアップグレードします。
で登録されたデバイスをオンプレミスの条件付きアクセスを使用するためには、まず、AD スキーマをアップグレードする必要があります。  次の条件を満たす必要があります。
    - スキーマが 85 またはそれ以降のバージョンにする必要があります。
    - これは、フォレストに参加している AD FS の要求

> [!NOTE]
> Windows Server 2016 でのスキーマ バージョン (レベル 85 以上) にアップグレードする前に Azure AD Connect をインストールした場合は、Azure AD Connect のインストールを再実行し、オンプレミスを更新する必要があります AD スキーマの同期規則を確認するには。msDS KeyCredentialLink が構成されます。

### <a name="verify-your-schema-level"></a>スキーマのレベルを確認します。
スキーマのレベルを確認するには、次の操作を行います。

1.  ADSIEdit または LDP を使用し、スキーマの名前付けコンテキストに接続することができます。  
2.  右クリックし、ADSIEdit を使用して"CN = Schema, CN = Configuration, DC =<domain>、DC =<com>プロパティを選択します。  Relpace のドメインとフォレストの情報で com の一部です。
3.  属性エディター の下 objectVersion 属性を見つけて、お使いのバージョンであることが通知されます。  

![ADSI エディター](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

次の PowerShell コマンドレット (実際、スキーマの名前付けコンテキスト情報を持つオブジェクト) を使用することもできます。

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

アップグレードする方法の詳細については、次を参照してください。[ドメイン コント ローラーを Windows Server 2016 にアップグレード](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md)します。 

## <a name="enable-azure-ad-device-registration"></a>Azure AD Device Registration を有効にします。  
このシナリオを構成するには、Azure AD でデバイスの登録機能を構成する必要があります。  

この場合の手順に従います[組織で Azure AD 参加の設定](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>AD FS の設定  
1. 作成、[新しい AD FS 2016 ファーム](https://technet.microsoft.com/library/dn486775.aspx)します。   
2.  または[移行](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)から AD FS 2012 R2 ad FS 2016 ファーム  
4. デプロイ[Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/)カスタム パスを使用して、AD FS を Azure AD に接続します。  

## <a name="configure-device-write-back-and-device-authentication"></a>デバイスの書き戻しとデバイスの認証を構成します。  
> [!NOTE]
> Express 設定を使用して、Azure AD Connect を実行すると場合、正しい AD オブジェクトが作成されています。  ただし、ほとんどの AD FS のシナリオで Azure AD Connect 実行された AD FS を構成するカスタム設定のため、以下の手順が必要です。  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>AD FS デバイス認証用の AD オブジェクトの作成  
AD FS ファームがまだデバイス認証用に構成されていない場合 (これは AD FS 管理コンソールで [サービス] の [デバイスの登録] から確認できます)、以下の手順に従って適切な AD DS オブジェクトと構成を作成します。  

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>注:注: 以下のコマンドでは Active Directory 管理ツールが必要であるため、フェデレーション サーバーがドメイン コントローラーではない場合は、次の手順 1. に従ってツールをインストールします。  それ以外の場合、手順 1. を省略できます。  

1.  **役割と機能の追加**ウィザードを実行して、 **[リモート サーバー管理ツール]**  ->  **[役割管理ツール]**  ->  **[AD DS および AD LDS ツール]** の機能を選択し、 **[Windows PowerShell の Active Directory モジュール]** と **[AD DS ツール]** の両方を選択します。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2. AD FS プライマリ サーバーでは Enterprise Admin (EA) 特権を持つ AD DS ユーザーとしてログインし、管理者特権で powershell プロンプトを開くを確認します。  次に、次の PowerShell コマンドを実行します。  
    
   `Import-module activedirectory`  
   `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3. ポップアップ ウィンドウで、[はい] をクリックします。

>注:AD FS サービスが GMSA アカウントを使用するように構成されている場合、アカウント名を「domain \accountname$」の形式で入力します。

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

>注: 必要に応じて、Azure AD Connect サーバーから、AdSyncPrep.psm1 ファイルをコピーします。  このファイルは、Program Files\Microsoft Azure Active Directory Connect\AdPrep にあります。

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


- オブジェクトの CN で型 msDS-DeviceRegistrationServiceContainer Device Registration Services, CN = Device Registration Configuration, CN = Services, CN = Configuration, DC = = (& a) ltdomain >  


- 上記のコンテナー内の msDS-DeviceRegistrationService 型のオブジェクト  

### <a name="see-it-work"></a>動作を確認します。  
新しいクレームとポリシーを評価するには、デバイスをまず登録します。  例については、[システム設定] アプリを使用して Windows 10 コンピューター]、[Azure AD Join を実行できますまたは Windows 10 ドメイン参加を設定するには追加の手順に従って自動デバイス登録を[ここ](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)します。  Windows 10 を結合する方法については、モバイル デバイスは、ドキュメントを参照してください。[ここ](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)します。  

最も簡単な評価のためには、要求の一覧を表示するテスト アプリケーションを使用して AD FS にサインオンします。 IsManaged、isCompliant、trusttype など、新しい要求を確認できるようにします。  作業の Microsoft Passport を有効にした場合は要求 prt も表示されます。  
 

## <a name="configure-additional-scenarios"></a>その他のシナリオを構成します。  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>自動登録の Windows 10 ドメイン参加しているコンピューター  
参加しているコンピューターの Windows 10 のドメインの自動デバイス登録を有効にする、次の手順 1. および 2.[ここ](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)します。   
これは、以下を実現するのに役立ちます。  

1. AD DS のサービス接続ポイントが存在し、適切なアクセス許可を持ちます (上、このオブジェクトを作成しましたが、二重にチェックを悪くはありません)。  
2. AD FS が正しく構成されていることを確認します。  
3. AD FS システムが、正しいエンドポイントを有効になっていることを確認し、要求規則の構成   
4. ドメイン参加済みコンピューターの自動デバイス登録に必要なグループ ポリシー設定を構成します。   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Microsoft Passport for Work と Windows 10 を有効にする方法の詳細については、次を参照してください。 [Microsoft passport For Work、組織でを有効にします。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>自動 MDM 登録   
手順に従って isCompliant 要求は、アクセス制御ポリシーで使用できるように、登録済みデバイスの自動 MDM 登録を有効にする、[ここです。](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>トラブルシューティング  
1.  エラーが発生する場合`Initialize-ADDeviceRegistration`既になど、正しくない状態で、既存のオブジェクトに関する文句を言うを「drs サービス オブジェクトが必要なすべての属性のない検出されました」、する可能性がありますが以前に実行された Azure AD Connect powershell コマンドとAD DS の部分構成があります。  下にあるオブジェクトを手動で削除してみてください**CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;ドメイン&gt;** から再試行してください。  
2.  Windows 10 ドメインに追加のクライアント  
    1. そのデバイス認証が動作していることを確認するには、テスト ユーザーのアカウントとドメイン参加しているクライアントにサインオンします。 迅速なプロビジョニングをトリガーするには、ロックし、少なくとも 1 回、デスクトップのロックを解除します。   
    2. Stk キー資格情報を確認する手順については、AD DS オブジェクトにリンク (同期も実行する必要が 2 回ですか?)  
3.  しようとしているデバイスが既に登録されているものの、できないか、デバイスを登録解除が既に Windows コンピューターの登録時にエラーが発生する場合は、レジストリにデバイス登録の構成の一部があります。  調査し、これを削除するには、次の手順を使用します。  
    1. Windows コンピューターの Regedit を開きに移動**hklm \software\microsoft\enrollments**   
    2. このキーの下のサブキーがあります多く GUID 形式でします。  約 17 の値が含まれ、「6」[参加している MDM] の"EnrollmentType"を持つサブキーまたは「13」(Azure AD に参加) に移動します  
    3. 変更**EnrollmentType**に**0** 
    4. デバイスの登録または登録をもう一度やり直してください。  

### <a name="related-articles"></a>関連資料  
* [Azure Active Directory に接続されている Office 365 やその他のアプリへのアクセスをセキュリティで保護します。](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access/)  
* [Office 365 サービス用条件付きアクセス デバイス ポリシー](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Azure Active Directory Device Registration を使用して、オンプレミス条件付きアクセスの設定](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [Windows 10 エクスペリエンスのために Azure AD にドメイン参加済みデバイスを接続します。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
