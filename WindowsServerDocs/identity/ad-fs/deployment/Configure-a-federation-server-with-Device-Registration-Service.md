---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: デバイス登録サービスを使用してフェデレーション サーバーを構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 511a039afd47cf7570fffdcaf17842e0eccc5683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843063"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>デバイス登録サービスを使用してフェデレーション サーバーを構成する

>適用先:Windows Server 2012 R2

デバイス登録サービスを有効にすることができます\(DRS\)フェデレーション サーバーでの手順が完了した後で[手順 4。Configure a Federation Server](https://technet.microsoft.com/library/dn303424.aspx)します。 デバイス登録サービスがシームレスな第 2 のオンボード メカニズムを提供要素認証、永続的なシングル サインオン\-で\(SSO\)、および企業へのアクセスを必要とするコンシューマーに条件付きアクセスリソース。 DRS の詳細については、次を参照してください[SSO およびシームレスな第 2 要素認証用アプリケーション間の任意のデバイスから社内への参加。](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>デバイスをサポートする Active Directory フォレストを準備します。  
  
> [!NOTE]  
> これは、1 つ\-時刻の操作のデバイスをサポートするために Active Directory フォレストを準備するために実行する必要があります。 エンタープライズ管理者権限でログオンする必要があり、Active Directory フォレストには、この手順を実行する Windows Server 2012 R2 スキーマが必要です。 します。  
>   
> さらに、DRS は、フォレスト ルート ドメインに少なくとも 1 つのグローバル カタログ サーバーがあることが必要です。 グローバル カタログ サーバーが初期化を実行するために必要な\-ADDeviceRegistration と AD FS の認証時にします。 AD FS を初期化しますで\-DRS の構成のメモリ表現が各認証要求のオブジェクトし、を DRS オブジェクトが GC に対して要求が試行された場合は、DRS の構成オブジェクトは、現在のドメインの DC で見つかりません、初期化中にプロビジョニングされた\-ADDeviceRegistration します。  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory フォレストを準備するには  
  
1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウと種類を開きます。  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  ServiceAccountName が表示されたら、AD FS のサービス アカウントとして選択したサービス アカウントの名前を入力します。  GMSA アカウントである場合、アカウントを入力します。、**ドメイン\\accountname**形式。 ドメイン アカウントでは、形式を使用して**ドメイン\\accountname**します。  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>フェデレーション サーバー ファーム ノードでデバイス登録サービスを有効にします。  
  
> [!NOTE]  
> この手順を実行するドメイン管理者権限でログオンする必要があります。  
  
#### <a name="to-enable-device-registration-service"></a>デバイス登録サービスを有効にするには  
  
1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウと種類を開きます。  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  AD FS ファーム内の各フェデレーション ファーム ノードでこの手順を繰り返す.  
  
## <a name="enable-seamless-second-factor-authentication"></a>有効にするシームレスな第 2 要素認証  
シームレスな第 2 要素認証は、それらにアクセスしようとしている外部デバイスから会社のリソースやアプリケーションへのアクセス保護の追加レベルを提供する AD FS での拡張機能。 個人所有のデバイスがワークプ レースに参加している場合は、"不明と"デバイスになり、管理者はこの情報を使用して、リソースへの条件付きアクセスとアクセスのドライブです。  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>シームレスな 2 つ目を有効に authentication、永続的なシングル サインイン\-で\(SSO\)とワークプ レース参加済みデバイスの条件付きアクセス  
  
1.  AD FS 管理コンソールでは、認証ポリシーに移動します。 グローバル プライマリ認証の編集を選択します。 デバイス認証の有効化、横のチェック ボックスを選択し、[ok] をクリックします。  
  
## <a name="update-the-web-application-proxy-configuration"></a>Web アプリケーション プロキシの構成を更新します。  
  
> [!IMPORTANT]  
> Web アプリケーション プロキシにデバイス登録サービスを発行する必要はありません。  フェデレーション サーバーで有効にした後に、デバイス登録サービスは、Web アプリケーション プロキシを介して使用可能になります。  デバイス登録サービスを有効にする前に配置されている場合は、Web アプリケーション プロキシの構成を更新するには、この手順を完了する必要があります。  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>Web アプリケーション プロキシ構成を更新するには  
  
1.  Web アプリケーション プロキシ サーバーで、Windows PowerShell コマンド ウィンドウを開き  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  資格情報が表示されたら、フェデレーション サーバーに管理者権限を持つアカウントの資格情報を入力します。  
  
## <a name="see-also"></a>関連項目 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームのデプロイ](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

