---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: 'チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理します。'
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: f651f60b5ba9e871a88a2df15d87b6819e851642
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956289"
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>チュートリアル ガイド:追加の多要素認証による個人情報アプリケーションのリスク管理




## <a name="about-this-guide"></a>このガイドについて
このチュートリアルでは、Active Directory フェデレーション サービス (AD FS) Windows Server 2012 R2 での多要素認証 (MFA) を構成する手順については、ユーザーのグループ メンバーシップ データに基づくを提供します。

AD FS での MFA と認証メカニズムの詳細については、次を参照してください。 [慎重を期するアプリケーションの追加の多要素認証によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。

このチュートリアルは次のセクションで構成されています。

-   [手順 1:ラボ環境のセットアップ](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [手順 2:AD FS での既定の認証メカニズムを確認する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [手順 3:フェデレーション サーバーで MFA を構成する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [手順 4:MFA メカニズムを確認する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="step-1-setting-up-the-lab-environment"></a><a name="BKMK_1"></a>手順 1:ラボ環境のセットアップ
このチュートリアルを完了するには、次のコンポーネントで構成された環境が必要です。

-   テスト ユーザー アカウントとグループ アカウント、Windows Server 2012 R2 または Windows Server 2012 R2 へのアップグレード対象のスキーマと Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されている Active Directory ドメインで実行されていると、Active Directory ドメイン

-   Windows Server 2012 R2 で実行されているフェデレーション サーバー

-   サンプル アプリケーションをホストする Web サーバー。

-   サンプル アプリケーションにアクセスできるクライアント コンピューター。

> [!WARNING]
> 運用環境でもテスト環境でも、フェデレーション サーバーと Web サーバーに同じコンピューターを使用しないことを強くお勧めします。

この環境では、フェデレーション サーバーは、ユーザーがサンプル アプリケーションにアクセスできるように、必要な要求を発行します。 Web サーバーはサンプルのアプリケーションをホストします。このアプリケーションは、フェデレーション サーバーが発行した要求を提示するユーザーを信頼します。

このような環境を設定する方法については、次を参照してください。 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

## <a name="step-2-verify-the-default-ad-fs-authentication-mechanism"></a><a name="BKMK_2"></a>手順 2:AD FS での既定の認証メカニズムを確認する
この手順では、AD FS の既定のアクセス制御メカニズム (エクストラネットの場合は **[フォーム認証]**、イントラネットの場合は **[Windows 認証]**) により、ユーザーが AD FS のサインイン ページにリダイレクトされ、有効な資格情報を入力するとアプリケーションへのアクセスが許可されることを確認します。 使用することができます、 **Robert Hatley** AD アカウントと **claimapp** サンプル アプリケーションで構成した [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

1.  クライアントコンピューターで、ブラウザーウィンドウを開き、サンプルアプリケーション () に移動し **https://webserv1.contoso.com/claimapp** ます。

    この操作により、要求がフェデレーション サーバーの役割に自動的にリダイレクトされた後、ユーザー名とパスワードでサインインするように求められます。

2.  資格情報を入力、 **Robert Hatley** で作成した AD アカウント [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

## <a name="step-3-configure-mfa-on-your-federation-server"></a><a name="BKMK_3"></a>手順 3:フェデレーション サーバーで MFA を構成する
Windows Server 2012 R2 の AD FS で MFA を構成する 2 つの部分があります。

-   [追加の認証方法を選択する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [MFA ポリシーを設定する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="select-an-additional-authentication-method"></a><a name="BKMK_5"></a>追加の認証方法を選択する
MFA を設定するには、追加の認証方法を選択する必要があります。 このチュートリアルでは、追加の認証方法に次のいずれかのオプションを選択できます。

-   選択 [証明書の認証](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7) 既定では、Windows Server 2012 R2 の AD FS で使用できるメソッド

-   [Windows Azure の Multi-Factor Authentication](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8) を構成および選択する

#### <a name="certificate-authentication"></a><a name="BKMK_7"></a>証明書の認証
追加の認証方法として証明書の認証を選択するには、次のいずれかの手順を完了します。

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用して追加の認証方法として証明書の認証を構成するには

1.  フェデレーション サーバーで、AD FS 管理コンソールの **[認証ポリシー]** ノードに移動し、**[多要素認証]** セクションで **[グローバル設定]** サブセクションの横にある **[編集]** リンクをクリックします。

2.  **[グローバル認証ポリシーの編集]** ウィンドウで、追加の認証方法として **[証明書の認証]** を選択し、**[OK]** をクリックします。

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell を使用して追加の認証方法として証明書の認証を構成するには

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > このコマンドが正常に実行されたことを確認するには、 `Get-AdfsGlobalAuthenticationPolicy` コマンドを実行できます。

#### <a name="windows-azure-multi-factor-authentication"></a><a name="BKMK_8"></a>Windows Azure の Multi-Factor Authentication
フェデレーション サーバーで追加の認証として **Windows Azure の Multi-Factor Authentication** をダウンロード、構成、選択するには、次の手順を完了します。

1.  [Windows Azure ポータルで多要素認証プロバイダーを作成する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Windows Azure の Multi-Factor Authentication Server をダウンロードする](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [Windows Azure の Multi-Factor Authentication Server をフェデレーション サーバーにインストールする](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [Windows Azure の Multi-Factor Authentication を追加の認証方式として構成する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="create-a-multi-factor-authentication-provider-via-the-windows-azure-portal"></a><a name="BKMK_a"></a>Windows Azure ポータルで多要素認証プロバイダーを作成する

1.  Administrator として Windows Azure ポータルにログオンします。

2.  左側で、[Active Directory] を選択します。

3.  [Active Directory] ページで、1 番上にある **[Multi-Factor Authentication プロバイダー]** を選択します。  下部にある [新規****] をクリックします。

4.  **[アプリケーション サービス] -&gt; [Active Directory]** で **[Multi-Factor Authentication プロバイダー]**、**[簡易作成]** の順に選択します。

5.  [アプリ サービス****] の [アクティブな認証プロバイダー****] を選択し、[クイック作成****] を選択します。

6.  次のフィールドに入力し、[作成****] を選択します。

    1.  **名前**-Multi-factor authentication プロバイダーの名前。

    2.  **使用モデル**-Multi-Factor Authentication プロバイダーの使用モデル。

        -   **認証ごと**-認証ごとに課金される購入モデル。 一般ユーザー向けアプリケーションで Windows Azure の Multi-Factor Authentication を使用するシナリオで通常使用されます。

        -   **有効なユーザーごと**-有効になっているユーザーごとに課金される購入モデル。  Office 365 などの従業員向けのシナリオで通常使用されます。

        使用モデルの詳細については、「 [Active Directory の料金詳細](https://www.windowsazure.com/pricing/details/active-directory/)」を参照してください。

    3.  **Directory** -Multi-Factor Authentication プロバイダーが関連付けられている Windows Azure Active Directory テナント。 これは省略可能です。内部設置型アプリケーションを保護するときは、プロバイダーを Windows Azure Active Directory に関連付ける必要がないためです。

7.  [作成] をクリックすると、多要素認証プロバイダーが作成され、「多要素認証プロバイダーが正常に作成されました。」というメッセージが表示されます。  **[OK]** をクリックします。

次に、Windows Azure の Multi-Factor Authentication Server をダウンロードする必要があります。 そのためには、Windows Azure ポータルから Windows Azure の Multi-Factor Authentication ポータルを起動します。

##### <a name="download-the-windows-azure-multi-factor-authentication-server"></a><a name="BKMK_b"></a>Windows Azure の Multi-Factor Authentication Server をダウンロードする

1.  Windows Azure ポータルに Administrator としてログオンし、前に示した手順で作成した多要素認証プロバイダーをクリックします。 その後、**[管理]** ボタンをクリックします。

    これにより **Windows Azure の Multi-Factor Authentication** ポータルが開きます。

2.  **Windows Azure の Multi-Factor Authentication** ポータルで、**[ダウンロード]** をクリックします。次に、**[ダウンロード]** をクリックして、Windows Azure の Multi-Factor Authentication Server のコピーをダウンロードします。

Windows Azure の Multi-Factor Authentication Server の実行可能ファイルをダウンロードしたら、フェデレーション サーバーにインストールする必要があります。

##### <a name="install-the-windows-azure-multi-factor-authentication-server-on-your-federation-server"></a><a name="BKMK_c"></a>Windows Azure の Multi-Factor Authentication Server をフェデレーション サーバーにインストールする

1.  Windows Azure の Multi-Factor Authentication Server の実行可能ファイルをダウンロードしてダブルクリックします。  これによりインストールが開始されます。

2.  [使用許諾契約書] 画面で契約書を読んだら、**[同意します]** を選択し、**[次へ]** をクリックします。

3.  インストール先のフォルダーが正しいことを確認したら、**[次へ]** をクリックします。

4.  インストールが完了したら、**[完了]** をクリックします。

これで、フェデレーション サーバーにインストールした Windows Azure の Multi-Factor Authentication Server を起動し、追加の認証方法として構成する準備ができました。

##### <a name="configure-windows-azure-multi-factor-authentication-as-an-additional-authentication-method"></a><a name="BKMK_d"></a>Windows Azure の Multi-Factor Authentication を追加の認証方式として構成する

1.  **Windows Azure の Multi-Factor Authentication** をフェデレーション サーバーにインストールした場所から起動します。ようこそページで **[認証構成ウィザードの使用をスキップする]** チェック ボックスをオンにし、 **[次へ]** をクリックします。

2.  Multi-Factor Authentication Server をライセンス認証するには、Multi-Factor Authentication Server をダウンロードした Multi-Factor Authentication 管理ポータルのページに戻り、**[アクティブ化資格情報の生成]** ボタンをクリックします。 Multi-Factor Authentication Server のユーザー インターフェイスで、生成された資格情報を入力し、**[ライセンス認証]** をクリックします。

3.  次に、**Multi-Factor Authentication Server** のユーザー インターフェイスで、**マルチサーバー構成ウィザード**を実行するように求められます。  このため、 **[いいえ]** を選択します。

    > [!IMPORTANT]
    > このチュートリアルを完了するために使用するフェデレーション サーバーがラボ環境に 1 台しかない場合は、**マルチサーバー構成ウィザード**の手順の完了はスキップできます。 ただし、フェデレーション サーバーがラボ環境に複数台ある場合は、Multi-Factor Authentication Server をインストールした後、フェデレーション サーバーで実行されている Multi-Factor Authentication Server 間のレプリケーションを有効にするために、各フェデレーション サーバーで**マルチサーバー構成ウィザード**の手順を完了する必要があります。

4.  **Multi-Factor Authentication Server** のユーザー インターフェイスで、**[ユーザー]** アイコンを選択し、**[Active Directory からインポート]** をクリックします。次に、Windows Azure の Multi-Factor Authentication でプロビジョニングする **Robert Hatley** アカウントを選択して、**[インポート]** をクリックします。

5.  **[ユーザー]** ボックスの一覧で、**Robert Hatley** アカウントを選択し、**[編集]** をクリックします。**[ユーザーの編集]** ウィンドウで、このアカウントの携帯電話番号を入力します。**[有効]** チェック ボックスがオンになっていることを確認し、**[適用]** をクリックします。

6.  **[ユーザー]** ボックスの一覧で、**Robert Hatley** アカウントを選択し、**[テスト]** をクリックします。 **[ユーザーのテスト]** ウィンドウで、**Robert Hatley** アカウントの資格情報を入力します。 携帯電話の呼び出し回数がキーを押してアカウント認証を完了するには、' #' です。

7.  **Multi-Factor Authentication Server** のユーザー インターフェイスで、**[AD FS]** アイコンを選択し、**[ユーザー登録を許可する]**、**[ユーザーに認証方法の選択を許可する]** (**[電話]** や **[テキスト メッセージ]** など)、**[代替認証にセキュリティの質問を使用する]**、**[ログを有効にする]** のチェック ボックスがオンになっていることを確認します。**[AD FS アダプターのインストール]** をクリックし、**Multi-Factor Authentication AD FS アダプター**のインストール ウィザードの手順を完了します。

    > [!NOTE]
    > **Multi-Factor Authentication AD FS アダプター**のインストール ウィザードにより、Active Directory で **PhoneFactor Admins** というセキュリティ グループが作成され、このグループにフェデレーション サービスの AD FS サービス アカウントが追加されます。
    >
    > **PhoneFactor Admins** グループが実際に作成され、AD FS サービス アカウントがこのグループのメンバーであることをドメイン コントローラーで確認することをお勧めします。
    >
    > 必要に応じて、ドメイン コントローラーで AD FS サービス アカウントを **PhoneFactor Admins** グループに手動で追加します。

    AD FS アダプターのインストールに関するその他の詳細については、Multi-Factor Authentication Server の右上隅にある [ヘルプ] リンクをクリックしてください。

8.  フェデレーション サービスにアダプターを登録するには、フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、 `\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`コマンドを実行します。 これで、アダプターは **WindowsAzureMultiFactorAuthentication** として登録されました。  登録を有効にするには、AD FS サービスを再起動する必要があります。

9. Windows Azure の Multi-Factor Authentication を追加の認証方法として構成するには、AD FS 管理コンソールで **[認証ポリシー]** ノードに移動し、**[多要素認証]** セクションで **[グローバル設定]** サブセクションの横にある **[編集]** リンクをクリックします。 **[グローバル認証ポリシーの編集]** ウィンドウで、**Multi-Factor Authentication** を追加の認証方式として選択し、 **[OK]** をクリックします。

    > [!NOTE]
    > Windows Azure の Multi-Factor Authentication の名前と説明はカスタマイズできます。サード パーティの認証方法も同様です。この名前と説明は **Set-AdfsAuthenticationProviderWebContent** コマンドレットを実行することで AD FS の UI に表示されます。 詳細については、「」を参照してください。[https://technet.microsoft.com/library/dn479401.aspx](/powershell/module/adfs/set-adfsauthenticationproviderwebcontent?view=win10-ps)

### <a name="set-up-mfa-policy"></a><a name="BKMK_6"></a>MFA ポリシーを設定する
MFA を有効にするには、フェデレーション サーバーで MFA ポリシーを設定する必要があります。 このチュートリアルでは、MFA ポリシーごと、 **Robert Hatley** MFA を受けるために属しているアカウントが必要な **Finance** で設定したグループ [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

AD FS 管理コンソールまたは Windows PowerShell のいずれかを使用して MFA ポリシーを設定できます。

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用して 'claimapp' 用のユーザーのグループ メンバーシップ データに基づく MFA ポリシーを構成するには

1.  フェデレーションサーバーの AD FS 管理コンソールで、[ **Authentication Policies** \\ **証明書利用者信頼ごと**の認証ポリシー] ノードに移動し、サンプルアプリケーション (**claimapp**) を表す証明書利用者信頼を選択します。

2.  **[操作]** ページで、または **[claimapp]** を右クリックして、**[カスタム多要素認証の編集]** を選択します。

3.  **[claimapp の証明書利用者信頼の編集]** ウィンドウで、**[ユーザー/グループ]** ボックスの一覧の横にある **[追加]** ボタンをクリックします。 入力 **Finance** で作成した AD グループの名前を [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md), 、] をクリック **名前の確認**, 、名前が解決できたら、以下の] をクリック **[ok]** します。

4.  **[claimapp の証明書利用者信頼の編集]** ウィンドウで **[OK]** をクリックします。

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>Windows PowerShell を使用して 'claimapp' 用のユーザーのグループ メンバーシップ データに基づく MFA ポリシーを構成するには

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > <group_SID> は AD グループ **Finance** の SID の値に置き換えてください。

## <a name="step-4-verify-mfa-mechanism"></a><a name="BKMK_4"></a>手順 4:MFA メカニズムを確認する
この手順では、前の手順で設定した MFA 機能を確認します。 次の手順を使用して、AD ユーザー **Robert Hatley** がサンプル アプリケーションにアクセスできることを確認できますが、今回は MFA を受ける必要があります。このユーザーは **Finance** グループに属しているためです。

1.  クライアントコンピューターで、ブラウザーウィンドウを開き、サンプルアプリケーション () に移動し **https://webserv1.contoso.com/claimapp** ます。

    この操作により、要求がフェデレーション サーバーの役割に自動的にリダイレクトされた後、ユーザー名とパスワードでサインインするように求められます。

2.  AD アカウント **Robert Hatley** の資格情報を入力します。

    MFA のポリシーが構成されているため、この時点で、ユーザーは追加の認証を受けるよう求められます。 既定のメッセージ テキストは "**セキュリティ上の理由から、アカウントを確認するための追加の情報が必要です**" です。 " です。ただし、このテキストはカスタマイズできます。 サインイン エクスペリエンスのカスタマイズ方法については、「 [Customizing the AD FS Sign-in Pages](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11))」を参照してください。

    追加の認証方法として証明書の認証を構成した場合、既定のメッセージ テキストは "**認証に使用する証明書を選択してください。操作をキャンセルする場合は、ブラウザーを閉じてからやり直してください。**" です

    追加認証方法として Windows Azure の Multi-Factor Authentication を構成した場合、既定のメッセージ テキストは "**認証を完了するため、ユーザーに電話を差し上げます。**" です。 Windows Azure 多要素認証を使用してサインインし、検証の推奨方法のさまざまなオプションの使用に関する詳細については、次を参照してください。 [Windows Azure 多要素認証の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11))します。

## <a name="see-also"></a>参照
[機密アプリケーション](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md) 
 の追加 Multi-Factor Authentication によるリスク管理[Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
