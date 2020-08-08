---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: デバイス登録サービスを使用してフェデレーション サーバーを構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: cba3f26a2c5e3d17e1c29609e44115c667838613
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963073"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>デバイス登録サービスを使用してフェデレーション サーバーを構成する

\( \) [「手順 4: フェデレーションサーバーを構成](/previous-versions/orphan-topics/ws.11/dn303424(v=ws.11))する」の手順を完了した後、フェデレーションサーバーでデバイス登録サービス DRS を有効にすることができます。 デバイス登録サービスは、シームレスな2要素認証、永続的シングルサイン \- オン \( SSO \) 、および会社のリソースへのアクセスを必要とするコンシューマーへの条件付きアクセスのためのオンボードメカニズムを提供します。 DRS の詳細については、「[任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

## <a name="prepare-your-active-directory-forest-to-support-devices"></a>デバイスをサポートするために Active Directory フォレストの準備を行う

> [!NOTE]
> これは、 \- デバイスをサポートするために Active Directory フォレストを準備するために実行する必要がある1回限りの操作です。 この手順を完了するには、エンタープライズ管理者権限を使用してログオンする必要があり、Active Directory フォレストに Windows Server 2012 R2 スキーマが組み込まれている必要があります。
>
> さらに、DRS では、フォレストのルートドメインに少なくとも1つのグローバルカタログサーバーが必要です。 Initialize Initialize-addeviceregistration を実行し AD FS 認証を実行するには、グローバルカタログサーバーが必要です \- 。 AD FS は、 \- 各認証要求で drs config オブジェクトのメモリ内表現を初期化します。また、現在のドメイン内の DC で drs 構成オブジェクトが見つからない場合は、initialize-addeviceregistration の初期化中に drs オブジェクトがプロビジョニングされた GC に対して要求が試行され \- ます。

#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory フォレストを準備するには

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のように入力します。

    ```
    Initialize-ADDeviceRegistration
    ```

2.  [ServiceAccountName] が要求されたら、AD FS のサービス アカウントとして選択したサービス アカウントの名前を入力します。  GMSA アカウントの場合は、**ドメイン \\ accountname $** 形式でアカウントを入力します。 ドメインアカウントの場合は、ドメインアカウント**の \\ **形式を使用します。

## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>フェデレーションサーバーファームノードでデバイス登録サービスを有効にする

> [!NOTE]
> この手順を実行するには、ドメイン管理者のアクセス許可を使用してログオンする必要があります。

#### <a name="to-enable-device-registration-service"></a>デバイス登録サービスを有効にするには

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のように入力します。

    ```
    Enable-AdfsDeviceRegistration
    ```

2.  AD FS ファームの各フェデレーションファームノードで、この手順を繰り返します。

## <a name="enable-seamless-second-factor-authentication"></a>シームレスな2要素認証を有効にする
シームレスな2要素認証は AD FS の拡張機能であり、企業のリソースやアプリケーションにアクセスしようとしている外部デバイスからのアクセス保護レベルを追加します。 個人用デバイスが社内参加している場合は、"既知の" デバイスになり、管理者はこの情報を使用して、リソースへの条件付きアクセスやゲートアクセスを行うことができます。

#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>シームレスな2要素認証を有効にするには、 \- \( \) ワークプレースジョインデバイスの SSO と条件付きアクセスを永続的に使用する

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

[Windows Server 2012 R2 AD FS の展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)

[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)

