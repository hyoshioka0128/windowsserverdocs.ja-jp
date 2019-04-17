---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: "デバイス登録サービスによるフェデレーション サーバーを構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 511a039afd47cf7570fffdcaf17842e0eccc5683
ms.sourcegitcommit: 9278435cbfa8dbeb30d0557ed0d27832b154edd2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2018
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>デバイス登録サービスによるフェデレーション サーバーを構成します。

>Windows Server 2012 R2 の適用対象:

手順を完了したら、フェデレーション サーバーでデバイス登録サービス \(DRS\) を有効にすることができます[手順 4: フェデレーション サーバーを構成する](https://technet.microsoft.com/library/dn303424.aspx)します。 デバイス登録サービス シームレスな第 2 のオンボード メカニズムを提供する認証、永続的な単一の sign\ \(SSO\)、および会社のリソースへのアクセスを必要とするコンシューマーに条件付きアクセスを考慮します。 DRS の詳細については、次を参照してください[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加。](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>デバイスをサポートする Active Directory フォレストを準備します。  
  
> [!NOTE]  
> これは、デバイスをサポートするために、Active Directory フォレストを準備する実行しなければならない特定時間操作です。 エンタープライズ管理者のアクセス許可でログオンする必要があり、Active Directory フォレストには、この手順を実行する Windows Server 2012 R2 スキーマが必要です。します。  
>   
> さらに、DRS では、フォレスト ルート ドメインに少なくとも 1 つのグローバル カタログ サーバーがあることが必要です。 グローバル カタログ サーバーが初期化 ADDeviceRegistration を実行するために必要な AD FS の認証中にします。 AD FS は、インメモリ オブジェクトの表現、DRS の構成の各認証要求を初期化し、DRS の構成オブジェクトが見つからない、DC で現在のドメインに初期化 ADDeviceRegistration 中にプロビジョニングされた DRS オブジェクトを GC に対して要求が試行します。  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory フォレストを準備するには  
  
1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウと種類を開きます。  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  ServiceAccountName のメッセージが表示されたら、AD FS のサービス アカウントとして選択したサービス アカウントの名前を入力します。  GMSA アカウントである場合にアカウントを入力、**domain\\accountname$**形式です。 ドメイン アカウントの形式を使用して**domain\\accountname**します。  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>フェデレーション サーバーのファーム ノードでデバイス登録サービスを有効にします。  
  
> [!NOTE]  
> この手順を実行するドメイン管理者のアクセス許可を持つログオンする必要があります。  
  
#### <a name="to-enable-device-registration-service"></a>デバイス登録サービスを有効にするには  
  
1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウと種類を開きます。  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  AD FS ファーム内の各フェデレーション ファーム ノードでこの手順を繰り返します。  
  
## <a name="enable-seamless-second-factor-authentication"></a>有効にするシームレスな第 2 要素認証  
シームレスな第 2 要素認証は、拡張機能の追加にアクセスしようとしている外部のデバイスから社内リソースとアプリケーションにアクセス保護のレベルを提供する AD FS でします。 個人のデバイスが職場に参加しているときは、'既知' のデバイスになります、管理者は、この情報を使用してドライブのリソースへの条件付きアクセスとゲート アクセスすることができます。  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>シームレスな第 2 を有効にする要素認証、永続的な単一の sign\ \(SSO\) とワークプ レースに参加しているデバイスの条件付きアクセス  
  
1.  AD FS 管理コンソールで、認証ポリシーに移動します。 グローバル プライマリ認証の編集を選択します。 デバイス認証を有効にする、横のチェック ボックスを選択し、[OK] をクリックします。  
  
## <a name="update-the-web-application-proxy-configuration"></a>Web アプリケーション プロキシの構成を更新します。  
  
> [!IMPORTANT]  
> Web アプリケーション プロキシは、デバイス登録サービスに発行する必要はありません。  フェデレーション サーバーで有効になっていると、デバイス登録サービスは Web アプリケーション プロキシ経由で利用可能なされます。  デバイス登録サービスを有効にする前に展開された場合は、Web アプリケーション プロキシの構成を更新するには、この手順を実行する必要があります。  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>Web アプリケーション プロキシ構成を更新するには  
  
1.  Web アプリケーション プロキシ サーバーで、Windows PowerShell コマンド ウィンドウを開いてください。  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  資格情報が表示されたら、フェデレーション サーバーに管理者権限を持つアカウントの資格情報を入力します。  
  
## <a name="see-also"></a>参照してください。 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

