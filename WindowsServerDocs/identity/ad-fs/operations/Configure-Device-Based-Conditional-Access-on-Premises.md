---
ms.assetid: 35de490f-c506-4b73-840c-b239b72decc2
title: "オンプレミス デバイス ベースの条件付きアクセスを構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/11/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 47afd0c6963bd8b8b4dde82650cf807c1954b40b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-on-premises-conditional-access-using-registered-devices"></a>登録済みデバイスを使用して構成する内部設置型条件付きアクセス

>適用対象: Windows Server 2016、Windows Server 2012 R2  

このドキュメントは、指示に従ってインストールおよび登録されているデバイスと内部設置型条件付きアクセスを構成します。

![条件付きアクセス](media/Using-Device-based-Conditional-Access-on-Premises/ADFS_ITPRO4.png)  

## <a name="infrastructure-pre-requisites"></a>インフラストラクチャの前提条件
内部設置型条件付きアクセス権を持つことができますを開始する前に、次ごとの前提条件は必要があります。 

|要件|説明
|-----|-----
|Azure AD Premium と Azure AD サブスクリプション | 内部設置型条件付きアクセスの上のデバイスの書き込みを有効にする[無料試用版に問題はありません](https://azure.microsoft.com/en-us/trial/get-started-active-directory/)  
|Intune のサブスクリプション|デバイス コンプライアンスのシナリオでの MDM 統合に必要なだけ[無料試用版に問題はありません](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0)
|Azure AD Connect|2015 年 11 月 QFE またはそれ以降。  最新バージョンを取得[ここ](https://www.microsoft.com/en-us/download/details.aspx?id=47594)します。  
|Windows Server 2016|ビルド 10586 以降の AD FS の  
|Windows Server 2016 の Active Directory スキーマ|スキーマ レベルが 85 以上が必要です。
|Windows Server 2016 ドメイン コント ローラー|これはこんにちはのビジネス キー信頼の展開に必要です。  追加情報をご覧[ここ](https://aka.ms/whfbdocs)します。  
|Windows 10 クライアント|ビルド 10586 またはそれ以降、上記のドメインに参加している作業シナリオのみに必要な Windows 10 ドメインに参加し、Microsoft Passport の  
|Azure AD Premium ライセンスが割り当てられている azure AD ユーザー アカウント|デバイスを登録するため  


 
## <a name="upgrade-your-active-directory-schema"></a>Active Directory スキーマがアップグレードします。
登録済みのデバイスで内部設置型条件付きアクセスを使用するためには、まず、AD スキーマをアップグレードする必要があります。  次の条件を満たす必要があります。
    - スキーマが 85 またはそれ以降のバージョンにする必要があります。
    - これは、フォレストに参加している AD FS に必要

> [!NOTE]
> Windows Server 2016 でのスキーマ バージョン (レベル 85 以上) にアップグレードする前に Azure AD Connect をインストールした場合は、Azure AD Connect のインストールを再実行して、内部設置型を更新する必要があります。AD スキーマを msDS KeyCredentialLink が構成されている同期規則を確認します。

### <a name="verify-your-schema-level"></a>スキーマ レベルを確認します。
スキーマ レベルを確認するには、次の操作を行います。

1.  ADSIEdit や LDP を使用し、スキーマ名前付けコンテキストに接続することができます。  
2.  右クリックし、ADSIEdit を使用して"CN = Schema, CN = Configuration, DC =<domain>、DC =<com>プロパティ] を選択します。  Relpace ドメインとフォレスト情報で com の一部です。
3.  属性エディター] の下 objectVersion 属性を見つけてするバージョンことが通知されます。  

![Adsi エディター](media/Configure-Device-Based-Conditional-Access-on-Premises/adsiedit.png)  

また、次の PowerShell コマンドレット (置換、スキーマ名前付けコンテキスト情報を持つオブジェクト) を使用することができます。

``` powershell
Get-ADObject "cn=schema,cn=configuration,dc=domain,dc=local" -Property objectVersion
    
```

![PowerShell](media/Configure-Device-Based-Conditional-Access-on-Premises/pshell1.png) 

アップグレードの詳細については、次を参照してください。[ドメイン コントローラーを Windows Server 2016 にアップグレード](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2016.md)します。 

## <a name="enable-azure-ad-device-registration"></a>Azure AD Device Registration を有効にします。  
このシナリオを構成するのには、Azure AD でデバイス登録の機能を構成する必要があります。  

これを行うには、下にある手順に従います[組織で Azure AD Join のセットアップ](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-setup/)  

## <a name="setup-ad-fs"></a>AD FS のセットアップ  
1. 作成、[新しい AD FS 2016 ファーム](https://technet.microsoft.com/library/dn486775.aspx)します。   
2.  または[移行](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)から AD FS 2012 R2 AD FS 2016 のファーム  
4. 展開[Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnectfed-whatis/)カスタム パスを使用して AD FS を Azure AD に接続します。  

## <a name="configure-device-write-back-and-device-authentication"></a>デバイスの書き戻しとデバイスの認証を構成します。  
> [!NOTE]
> Express 設定を使用して、Azure AD Connect を実行した場合は、正しい AD オブジェクトを作成されています。  ただし、ほとんどの AD FS のシナリオで Azure AD Connect して実行したカスタム設定の AD FS を構成するため、以下の手順が必要です。  

### <a name="create-ad-objects-for-ad-fs-device-authentication"></a>AD FS デバイス認証の AD オブジェクトを作成します。  
デバイス認証の AD FS ファームが既に構成されていない場合 (ご覧サービスで AD FS 管理コンソールでデバイスの登録]-> [)、適切な AD DS オブジェクトおよび構成を作成する、次の手順を使用します。  

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device1.png)

>注: 次のコマンドは、Active Directory 管理ツールを必要と、その場合は、フェデレーション サーバーは、また、ドメイン コント ローラーではない、まずツールをインストール、1 次の手順を使用しています。  それ以外の場合、手順 1. を省略できます。  

1.  実行、**追加の役割と機能**ウィザードと選択機能**リモート サーバー管理ツール** -> **役割管理ツール** -> **AD DS および AD LDS ツール**両方の選択]-> [、 **Windows PowerShell 用 Active Directory モジュール**と**AD DS ツール**します。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device2.png)
  
2.  AD FS のプライマリ サーバーで Enterprise Admin (EA) 特権を持つ AD DS ユーザーとしてログインして、管理者特権の powershell プロンプトを開きを確認します。  次に、次の PowerShell コマンドを実行します。  
    
    `Import-module activedirectory`  
    `PS C:\> Initialize-ADDeviceRegistration -ServiceAccountName "<your service account>" ` 
3.  ポップアップ ウィンドウで、[はい] を押します。

>注: AD FS サービスが GMSA アカウントを使用して構成されている場合、アカウント名を入力「domain \accountname$」の形式で

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device3.png)  

上記の PSH、次のオブジェクトを作成します。  


- AD ドメイン パーティション RegisteredDevices コンテナー  
- --> サービスのデバイス登録サービス コンテナーおよびオブジェクト [構成] でデバイス登録の構成-->  
- --> サービスのデバイス登録サービス DKM コンテナーとオブジェクト [構成] でデバイス登録の構成-->  

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device4.png)  

4.  これが完了すると、正常に完了メッセージが表示されます。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device5.png) 

###        <a name="create-service-connection-point-scp-in-ad"></a>AD でサービス接続ポイント (SCP) を作成します。  
Windows 10 ドメインへの参加 (Azure AD に自動登録) の手順に従ってここで使用する場合は、AD DS にサービス接続ポイントを作成するには、次のコマンドを実行します。  
1.  Windows PowerShell を開き、次を実行します。
    
    `PS C:>Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1" ` 

>注: 必要に応じて、コピー、AdSyncPrep.psm1 ファイル、Azure AD Connect サーバーからです。  このファイルはプログラム \microsoft Azure Active Directory Connect\AdPrep にあります。

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device6.png)   

2. Azure AD グローバル管理者の資格情報を提供します。  

    `PS C:>$aadAdminCred = Get-Credential`

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device7.png) 

3.  次の PowerShell コマンドを実行します。 

    `PS C:>Initialize-ADSyncDomainJoinedComputerSync -AdConnectorAccount [AD connector account name] -AzureADCredentials $aadAdminCred ` 

[AD コネクタ アカウント名] が、内部設置型を追加するときに、Azure AD Connect で構成したアカウントの名前をここでは AD DS ディレクトリ。
  
上記のコマンドは、Windows 10 クライアントが、適切な検索を有効にする Azure AD ドメインに AD DS に serviceConnectionpoint オブジェクトを作成することで参加します。  

### <a name="prepare-ad-for-device-write-back"></a>デバイスの書き戻しの AD を準備します。   
確実に AD DS オブジェクトおよびコンテナーの適切な状態で Azure AD からデバイスの背面の書き込みを次の手順を実行します。

1.  Windows PowerShell を開き、次を実行します。  

    `PS C:>Initialize-ADSyncDeviceWriteBack -DomainName <AD DS domain name> -AdConnectorAccount [AD connector account name] ` 

[AD コネクタ アカウント名] が、内部設置型を追加するときに、Azure AD Connect で構成したアカウントの名前は domain \accountname 形式での AD DS ディレクトリ  

上記のコマンドは、既に、存在しない場合、AD DS にバックアップ デバイスの書き込みの次のオブジェクトを作成でき、指定された AD コネクタ アカウント名へのアクセス  

- AD ドメイン パーティション RegisteredDevices コンテナー  
- --> サービスのデバイス登録サービス コンテナーおよびオブジェクト [構成] でデバイス登録の構成-->  

### <a name="enable-device-write-back-in-azure-ad-connect"></a>デバイスの書き込みを有効にする Azure AD に接続します。  
完了していない場合前に、もう一度ウィザードの実行を選択して Azure AD Connect でバックアップ デバイスの書き込みを有効にする**"同期オプションのカスタマイズ**、デバイスの書き戻しのチェック ボックスをオンし上記コマンドレットを実行したフォレストを選択します。  

### <a name="configure-device-authentication-in-ad-fs"></a>AD FS でデバイス認証を構成します。  
次のコマンドを実行して AD FS のポリシーを構成する管理者特権の PowerShell コマンド ウィンドウを使用して、  

`PS C:>Set-AdfsGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true -DeviceAuthenticationMethod All` 

### <a name="check-your-configuration"></a>構成を確認します  
リファレンスについては、以下に示します、AD DS のデバイス、コンテナーとデバイスの書き戻しと認証の動作に必要なアクセス許可の包括的な一覧
 


- オブジェクトの種類 ms-DS-DeviceContainer CN で RegisteredDevices, DC = =&lt;ドメイン&gt;        
    - AD FS サービス アカウントに読み取りアクセス権   
    - Azure AD Connect sync AD コネクタ アカウントへのアクセスを読み取り/書き込み</br></br>

- コンテナーの CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;ドメイン&gt;  
- 上記のコンテナーでコンテナー デバイス登録サービス コンテナー DKM

![デバイスの登録](media/Configure-Device-Based-Conditional-Access-on-Premises/device8.png) 
 


- CN で型 serviceconnectionpoint オブジェクト =&lt;guid&gt;、CN = デバイスの登録

- 構成、CN = Services, CN = Configuration, DC =&lt;ドメイン&gt;  
 - 読み取り/書き込みアクセスを新しいオブジェクトに指定された AD コネクタ アカウント名</br></br> 


- オブジェクト CN で型 msDS-DeviceRegistrationServiceContainer のデバイスの登録 Services, CN = Device Registration Configuration, CN = Services, CN = Configuration, DC = = & ltdomain >  


- 種類 msDS-DeviceRegistrationService 上記のコンテナー内のオブジェクト  

### <a name="see-it-work"></a>動作を参照してください。  
を新しい信頼性情報とポリシーを評価するには、最初にデバイスを登録します。  たとえば、システムで、設定アプリを使用して Windows 10 コンピューターは、に関する]-> [Azure AD への参加することができますか追加の手順に従って、デバイスの自動登録と Windows 10 ドメインへの参加をセットアップすることができます[ここ](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)します。  モバイル デバイスは、Windows 10 を結合する方法については、ドキュメントを参照してください[ここ](https://technet.microsoft.com/itpro/windows/manage/join-windows-10-mobile-to-azure-active-directory)します。  

最も簡単な評価は、AD fs のクレームの一覧を表示するテスト アプリケーションを使用してサインオンします。 IsManaged、isCompliant、trusttype など、新しい信頼性情報を表示することができます。  作業の Microsoft Passport を有効にした場合は要求 prt も表示されます。  
 

## <a name="configure-additional-scenarios"></a>その他のシナリオを構成します。  
### <a name="automatic-registration-for-windows-10-domain-joined-computers"></a>自動登録の Windows 10 ドメインに参加しているコンピューター  
Windows 10 ドメインのデバイスの自動登録を有効にするには、コンピューターを参加させました。 は、次の手順 1 と 2[ここ](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)します。   
これによって、次を実現します。  

1. AD DS に、サービス接続ポイントが存在し、適切なアクセス許可を持つことを確認 (上、このオブジェクトを作成しましたはない悪影響を及ぼしている再確認)。  
2. AD FS が正しく構成されていることを確認します。  
3. AD FS システムが、正しいエンドポイントを有効になっていることを確認し、要求規則の構成   
4. ドメインに参加しているコンピューターのデバイスの自動登録のために必要なグループ ポリシー設定を構成します。   

### <a name="microsoft-passport-for-work"></a>Microsoft Passport for Work   
Microsoft Passport for Work と Windows 10 を有効にする方法については、次を参照してください。 [、組織での作業の Microsoft Passport を有効にします。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)  

### <a name="automatic-mdm-enrollment"></a>MDM の自動登録   
IsCompliant 要求は、アクセス制御ポリシーで使用できるように、登録済みデバイスの MDM の自動登録を有効にする手順を実行、[次のとおりです。](https://blogs.technet.microsoft.com/ad/2015/08/14/windows-10-azure-ad-and-microsoft-intune-automatic-mdm-enrollment-powered-by-the-cloud/)  

## <a name="troubleshooting"></a>トラブルシューティング  
1.  エラーが発生した場合`Initialize-ADDeviceRegistration`は既になど、正しくない状態で、既存のオブジェクトに関する苦情を「drs サービス オブジェクトが見つかったすべての必要な属性のない」、powershell コマンドを以前と AD DS の部分的な構成を使用して、Azure AD Connect を実行する場合があります。  下にあるオブジェクトを手動で削除してみてください**CN = Device Registration Configuration, CN = Services, CN = Configuration, DC =&lt;ドメイン&gt;**してからもう一度します。  
2.  Windows 10 ドメインに追加のクライアント  
    1. テスト ユーザー アカウントとそのデバイス認証が動作していることを確認するには、ドメインに参加しているクライアントにサインオンします。 迅速なプロビジョニングをトリガーするには、ロックし、少なくとも 1 回、デスクトップのロックを解除します。   
    2. Stk キーの資格情報を確認する手順については、AD DS オブジェクトにリンク (同期も実行する必要が 2 回ですか?)  
3.  デバイスが既に登録されているが、できないか、デバイスを登録解除が既に Windows コンピューターを登録しているときにエラーが発生する場合は、レジストリでデバイス登録の構成の一部があります。  調査し、これを削除するには、次の手順を使用します。  
    1. Windows コンピューターで、[Regedit を開きを**\software\microsoft\enrollments**   
    2. このキーの下のサブキーがあります多く GUID 形式でします。  約 17 の値が含まれると、「6」[参加している MDM] の"EnrollmentType"を持つサブキーまたは「13」(Azure AD に参加している) に移動  
    3. 変更**EnrollmentType**に**0** 
    4. デバイスの登録または登録をもう一度やり直してください。  

### <a name="related-articles"></a>関連する記事  
* [Azure Active Directory に接続されている Office 365 やその他のアプリへのアクセスをセキュリティで保護します。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)  
* [Office 365 サービスのデバイス ポリシーの条件付きアクセス](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-device-policies/)  
* [Azure Active Directory Device Registration を使用して内部設置型条件付きアクセスのセットアップ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-device-registration-on-premises-setup)  
* [ドメインに参加しているデバイスを Windows 10 エクスペリエンスのための Azure AD に接続します。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)  
