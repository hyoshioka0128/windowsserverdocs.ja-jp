---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: デバイス登録サービスを使用してフェデレーション サーバーを構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c7775801940faeba07ad91aa81434a34c97eb6bc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855515"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>デバイス登録サービスを使用してフェデレーション サーバーを構成する

[「手順 4: フェデレーションサーバーを構成](https://technet.microsoft.com/library/dn303424.aspx)する」の手順を完了した後に、フェデレーションサーバーでデバイス登録サービス \(DRS\) を有効にすることができます。 デバイス登録サービスは、シームレスな第2要素認証、\(SSO\)での永続的シングルサイン\-、および会社のリソースへのアクセスを必要とするコンシューマーへの条件付きアクセスのためのオンボードメカニズムを提供します。 DRS の詳細については、「[任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>デバイスをサポートするために Active Directory フォレストを準備する  
  
> [!NOTE]  
> これは、デバイスをサポートするために Active Directory フォレストを準備するために実行する必要がある\-の1つの時間の操作です。 この手順を実行するには、エンタープライズ管理者のアクセス許可を使用してログオンする必要があります。また、Active Directory フォレストには、Windows Server 2012 R2 スキーマが含まれている必要があります。  
>   
> さらに、DRS では、フォレストのルートドメインに少なくとも1つのグローバルカタログサーバーが必要です。 初期化\-Initialize-addeviceregistration を実行して AD FS 認証を実行するには、グローバルカタログサーバーが必要です。 AD FS によって、各認証要求で DRS config オブジェクトの\-メモリ表現が初期化されます。また、現在のドメインの DC で DRS 構成オブジェクトが見つからない場合、Initialize\-Initialize-addeviceregistration の実行中に DRS オブジェクトがプロビジョニングされた GC に対して要求が試行されます。  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory フォレストを準備するには  
  
1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のように入力します。  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  [ServiceAccountName] が要求されたら、AD FS のサービス アカウントとして選択したサービス アカウントの名前を入力します。  GMSA アカウントの場合は、**ドメイン\\accountname $** 形式でアカウントを入力します。 ドメインアカウントの場合は、**ドメイン\\accountname**という形式を使用します。  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>フェデレーションサーバーファームノードでデバイス登録サービスを有効にする  
  
> [!NOTE]  
> この手順を実行するには、ドメイン管理者のアクセス許可を使用してログオンする必要があります。  
  
#### <a name="to-enable-device-registration-service"></a>デバイス登録サービスを有効にするには  
  
1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のように入力します。  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  AD FS ファームの各フェデレーションファームノードで、この手順を繰り返します。  
  
## <a name="enable-seamless-second-factor-authentication"></a>シームレスな2要素認証を有効にする  
シームレスな2要素認証は AD FS の拡張機能であり、企業のリソースやアプリケーションにアクセスしようとしている外部デバイスからのアクセス保護レベルを追加します。 個人用デバイスが社内参加している場合は、"既知の" デバイスになり、管理者はこの情報を使用して、リソースへの条件付きアクセスやゲートアクセスを行うことができます。  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>シームレスな第2要素認証を有効にするには \(SSO\) での永続的シングルサイン\-と社内参加デバイスの条件付きアクセス  
  
1.  AD FS 管理コンソールで、[認証ポリシー] に移動します。 [グローバル プライマリ認証の編集] を選択します。 [デバイス認証の有効化] の横にあるチェック ボックスをオンにして、[OK] をクリックします。  
  
## <a name="update-the-web-application-proxy-configuration"></a>Web アプリケーションプロキシの構成を更新する  
  
> [!IMPORTANT]  
> デバイス登録サービスを Web アプリケーションプロキシに発行する必要はありません。  デバイス登録サービスは、フェデレーションサーバーで有効にされると、Web アプリケーションプロキシ経由で使用できるようになります。  デバイス登録サービスを有効にする前に Web アプリケーションプロキシの構成を更新するには、この手順を完了する必要があります。  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>Web アプリケーションプロキシの構成を更新するには  
  
1.  Web アプリケーションプロキシサーバーで、Windows PowerShell コマンドウィンドウを開き、「」と入力します。  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  資格情報の入力を求められたら、フェデレーションサーバーに対する管理者権限を持つアカウントの資格情報を入力します。  
  
## <a name="see-also"></a>参照 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

