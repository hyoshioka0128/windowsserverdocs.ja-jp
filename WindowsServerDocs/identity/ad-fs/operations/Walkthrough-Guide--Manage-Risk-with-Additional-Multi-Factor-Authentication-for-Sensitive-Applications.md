---
ms.assetid: 5fd4063d-34dc-4b15-9a88-cc6c1fff455a
title: "チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 414f37e86f0072863e5fa2f107c39e5518e560ec
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理します。

>Windows Server 2012 R2 の適用対象:


## <a name="about-this-guide"></a>このガイドについて
このチュートリアルでは、Active Directory フェデレーション サービス (AD FS) Windows Server 2012 R2 での多要素認証 (MFA) を構成する手順については、ユーザーのグループ メンバーシップ データに基づくを提供します。

AD FS での MFA および認証メカニズムの詳細については、次を参照してください。[による追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。

このチュートリアルでは、次のセクションで構成されます。

-   [手順 1: ラボ環境のセットアップ](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [手順 2: は、既定の AD FS の認証メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)

-   [手順 3: フェデレーション サーバーで MFA を構成します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_3)

-   [手順 4: MFA メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_4)

## <a name="BKMK_1"></a>手順 1: ラボ環境のセットアップ
このチュートリアルを完了するためには、次のコンポーネントで構成される環境が必要です。

-   テスト ユーザーとグループ アカウント、Windows Server 2012 R2 または Windows Server 2012 R2 にアップグレード対象のスキーマと Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されている Active Directory ドメインで実行されている Active Directory ドメイン

-   Windows Server 2012 R2 で実行されているフェデレーション サーバー

-   サンプル アプリケーションをホストする web サーバー

-   元のサンプル アプリケーションにアクセスできるクライアント コンピューター

> [!WARNING]
> 強くお勧め (実稼働し、テスト環境での両方) も、フェデレーション サーバーと web サーバーを同じコンピューターを使用しないことです。

この環境では、フェデレーション サーバーは、ユーザーが、サンプル アプリケーションにアクセスできるように必要とされる信頼性情報を発行します。 Web サーバーは、フェデレーション サーバーが発行した要求を提示するユーザーを信頼するサンプル アプリケーションをホストします。

この環境をセットアップする方法については、次を参照してください。 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

## <a name="BKMK_2"></a>手順 2: は、既定の AD FS の認証メカニズムを確認します。
この手順では、AD FS の既定のアクセス制御メカニズムを確認します (**フォーム認証**のエクストラネットおよび**Windows 認証**イントラネットで)、場所、ユーザー、AD FS サインイン ページにリダイレクトされ、有効な資格情報を入力およびアプリケーションへのアクセス権が付与されます。 使用することができます、 **Robert Hatley** AD アカウントと**claimapp**サンプル アプリケーションで構成した[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

1.  クライアント コンピューターに、ブラウザー ウィンドウを開き、サンプル アプリケーションに移動します。 **https://webserv1.contoso.com/claimapp**します。

    この操作が自動的に要求をフェデレーション サーバーにリダイレクトし、ユーザー名とパスワードを使用してサインインを求められます。

2.  資格情報を入力、 **Robert Hatley**で作成した AD アカウント[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

## <a name="BKMK_3"></a>手順 3: フェデレーション サーバーで MFA を構成します。
Windows Server 2012 R2 の AD FS で MFA を構成する 2 つの部分があります。

-   [追加の認証方法を選択します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_5)

-   [MFA ポリシーを設定します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_6)

### <a name="BKMK_5"></a>追加の認証方法を選択します。
MFA を設定するために追加の認証方法を選択する必要があります。 このチュートリアルでは、追加の認証方法の場合は、次のオプションの間で選択できます。

-   選択[証明書の認証](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_7)既定では、Windows Server 2012 R2 の AD FS で使用できるメソッド

-   構成および選択[Windows Azure Multi-factor Authentication](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_8)

#### <a name="BKMK_7"></a>証明書の認証
追加の認証方法として証明書の認証を選択するのには、次の手順のいずれかの操作を行います。

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用して追加の認証方法として証明書の認証を構成するには

1.  移動し、AD FS 管理コンソールで、フェデレーション サーバーで、**認証ポリシー**ノード、し、[ **multi-factor Authentication**セクションで、をクリックして、**編集**] の横にリンク、**グローバル設定**サブセクションします。

2.  **グローバル認証ポリシーの編集**ウィンドウで、**証明書の認証**をクリックし、追加の認証方法として**OK**します。

###### <a name="to-configure-certificate-authentication-as-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell を使用して追加の認証方法として証明書の認証を構成するには

1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。

    ```
    Set-AdfsGlobalAuthenticationPolicy -AdditionalAuthenticationProvider CertificateAuthentication

    ```

    > [!WARNING]
    > このコマンドが正常に実行された、実行できることを確認する、`Get-AdfsGlobalAuthenticationPolicy`コマンド。

#### <a name="BKMK_8"></a>Windows Azure Multi-factor Authentication
ダウンロードし、構成を選択するために、次の手順を完了**Windows Azure Multi-factor Authentication**としてフェデレーション サーバーで追加の認証。

1.  [Windows によって、Multi-factor Authentication プロバイダーを作成する Azure ポータル](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_a)

2.  [Windows Azure Multi-factor Authentication Server をダウンロードします。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_b)

3.  [フェデレーション サーバーで Windows Azure Multi-factor Authentication Server をインストールします。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_c)

4.  [追加の認証方法として Windows Azure Multi-factor Authentication を構成します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_d)

##### <a name="BKMK_a"></a>Windows によって、Multi-factor Authentication プロバイダーを作成する Azure ポータル

1.  Windows Azure にログオンし、管理者としてポータルです。

2.  左側の [Active Directory を選択します。

3.  [Active Directory] ページの上部で、次のように選択します。**多要素認証プロバイダー**します。  下部にある、] をクリックして**新規**します。

4.  下にある**アプリ サービスに Active Directory]-> [**[**多要素認証プロバイダー**、] を選択し、**簡易作成**します。

5.  下にある**アプリ サービス**[**アクティブな認証プロバイダー**、] を選択し、**簡易作成**します。

6.  次のフィールドと選択を入力**作成**します。

    1.  **名前**-多要素認証プロバイダーの名前。

    2.  **使用モデル**-Multi-factor Authentication プロバイダーの使用モデル。

        -   **認証ごと**-認証ごとに課金される購入モデル。 消費者向けのアプリケーションで Windows Azure Multi-factor Authentication を使用するシナリオで通常使用されます。

        -   **有効なユーザーあたり**-有効なユーザーごとに課金される購入モデル。  通常、Office 365 などの従業員向けのシナリオに使用されます。

        使用モデルの詳細については、次を参照してください。 [Windows Azure の料金詳細](http://www.windowsazure.com/pricing/details/active-directory/)します。

    3.  **ディレクトリ**-多要素認証プロバイダーが関連付けられている、Windows Azure の Active Directory テナント。 これは、プロバイダーがセキュリティで保護する内部設置型アプリケーションと Windows Azure Active Directory にリンクする必要はありません、省略可能です。

7.  作成] をクリックすると、Multi-factor Authentication プロバイダーが作成され、ようにというメッセージが表示されます: 多要素認証プロバイダーが正常に作成します。  をクリックして**OK**します。

次に、Windows Azure Multi-factor Authentication Server をダウンロードする必要があります。 Windows Azure ポータルから Windows Azure Multi-factor Authentication ポータルを起動して、これを行うことができます。

##### <a name="BKMK_b"></a>Windows Azure Multi-factor Authentication Server をダウンロードします。

1.  管理者は、Windows Azure ポータルにログオンし、上記の手順で作成した Multi-factor Authentication プロバイダーをクリックします。 をクリックし、**管理**ボタンをクリックします。

    これにより、起動、 **Windows Azure Multi-factor Authentication**ポータルです。

2.  **Windows Azure Multi-factor Authentication**ポータル、] をクリック**ダウンロード**、] をクリックし、**ダウンロード**Windows Azure Multi-factor Authentication Server のコピーをダウンロードします。

Windows Azure Multi-factor Authentication Server の実行可能ファイルをダウンロードした場合は、フェデレーション サーバーにインストールする必要があります。

##### <a name="BKMK_c"></a>フェデレーション サーバーで Windows Azure Multi-factor Authentication Server をインストールします。

1.  ダウンロードして、Windows Azure Multi-factor Authentication Server の実行可能ファイルをダブルクリックします。  これにより、インストールが開始されます。

2.  [使用許諾契約書] 画面で、契約を読み選択**同意**] をクリック**次**します。

3.  移行先のフォルダーが正しいことを確認し] をクリックして**次**します。

4.  インストールが完了したら、クリックして**完了**します。

フェデレーション サーバーにインストールされている Windows Azure Multi-factor Authentication server を起動し、追加の認証方法として構成する準備が整いました。

##### <a name="BKMK_d"></a>追加の認証方法として Windows Azure Multi-factor Authentication を構成します。

1.  起動**Windows Azure Multi-factor Authentication**からインストールした場所、フェデレーション サーバーで、[ようこそ] ページで、確認、**認証構成ウィザードを使用してをスキップ**チェック ボックスをオン] をクリック**[次へ]**します。

2.  Multi-factor Authentication Server をアクティブ化するページに戻り、Multi-factor Authentication 管理ポータルで、Multi-factor Authentication Server をダウンロードして] をクリックして、**アクティブ化資格情報の生成**ボタンをクリックします。 Multi-factor Authentication Server ユーザー インターフェイスで生成された資格情報を入力し、クリックして**Activate**します。

3.  次に、 **Multi-factor Authentication Server**ユーザー インターフェイスを実行するように求められます、**マルチ サーバー構成ウィザード**します。  選択**いいえ**します。

    > [!IMPORTANT]
    > 完了をスキップすることができます、**マルチ サーバー構成ウィザード**このチュートリアルを完了するために使用する 1 つだけのフェデレーション サーバーとラボ環境を指定します。 ただし場合は、環境にいくつかのフェデレーション サーバーが含まれている必要があります、Multi-factor Authentication Server をインストールし、完了した、**マルチ サーバー構成ウィザード**、フェデレーション サーバーで実行されている Multi-factor サーバー間のレプリケーションを有効にするには、各フェデレーション サーバーにします。

4.  **Multi-factor Authentication Server**ユーザー インターフェイス、**ユーザー**アイコン、] をクリックして**Active Directory からインポート**を選択、 **Robert Hatley**クリックして、Windows Azure の Multi-factor Authentication でプロビジョニングするアカウント**インポート**します。

5.  **ユーザー**一覧で、[、 **Robert Hatley**アカウント] をクリックして**編集**、し、[、**ユーザーの編集**] ウィンドウで、このアカウントの携帯電話番号を提供することを確認、**有効**] チェック ボックスがオンになっているし] をクリックして**適用**します。

6.  **ユーザー**一覧で、[、 **Robert Hatley**アカウント、およびクリックして**テスト**します。 **テスト ユーザー** ] ウィンドウの資格情報を提供する、 **Robert Hatley**アカウント。 携帯電話の呼び出し回数がキーを押してアカウントの確認を完了するには、「#」.

7.  **Multi-factor Authentication Server**ユーザー インターフェイスで、 **AD FS**アイコン、ことを確認して**ユーザー登録を許可する**、**方法を選択できるように**(を含む**電話による認証**と**テキスト メッセージ**)、**代替のセキュリティの質問を使用して**と**ログ記録を有効にする**チェック ボックスをオン] をクリックして**AD FS アダプターのインストール**、完了と、 **Multi-factor Authentication AD FS アダプター**インストール ウィザード。

    > [!NOTE]
    > **Multi-factor Authentication AD FS アダプター**インストール ウィザードと呼ばれるセキュリティ グループを作成する**PhoneFactor Admins** Active Directory でし、フェデレーション サービスの AD FS サービス アカウントをこのグループに追加します。
    > 
    > ドメイン コント ローラーを確認することをお勧めする、 **PhoneFactor Admins**グループが実際に作成され、このグループのメンバーであること、AD FS サービス アカウント。
    > 
    > 必要に応じて、AD FS サービス アカウントを追加、 **PhoneFactor Admins** 、ドメイン コント ローラーを手動でグループ化します。

    AD FS アダプターのインストールについて詳しくは、Multi-factor Authentication Server の右上隅にある [ヘルプ] リンクをクリックします。

8.  アダプターをフェデレーション サーバーで、フェデレーション サービスに登録する、Windows PowerShell コマンド ウィンドウを起動し、次のコマンドを実行します。`\Program Files\Multi-Factor Authentication Server\Register-MultiFactorAuthenticationAdfsAdapter.ps1`します。 アダプターとして登録**WindowsAzureMultiFactorAuthentication**します。  登録を有効に、AD FS サービスを再起動する必要があります。

9. 移動し、AD FS 管理コンソールで、追加の認証方法として Windows Azure Multi-factor Authentication を構成する、**認証ポリシー**ノード、し、[ **multi-factor Authentication**セクションで、をクリックして、**編集**] の横にリンク、**グローバル設定**サブセクションします。 **グローバル認証ポリシーの編集**ウィンドウで、 **Multi-factor Authentication**をクリックし、追加の認証方法として**OK**します。

    > [!NOTE]
    > 名をカスタマイズしてを実行して、AD FS の UI に表示される、Windows Azure Multi-factor Authentication メソッドと同様のいずれかの説明にサード パーティの認証方法、構成されている、 **Set-adfsauthenticationproviderwebcontent**コマンドレット。 詳細については、次を参照してください[https://technet.microsoft.com/library/dn479401.aspx。](https://technet.microsoft.com/library/dn479401.aspx)

### <a name="BKMK_6"></a>MFA ポリシーを設定します。
MFA を有効にするために、フェデレーション サーバーで MFA ポリシーを設定する必要があります。 このチュートリアルでは、MFA ポリシーごとに、 **Robert Hatley** MFA を受けるために属しているアカウントが必要な**Finance**で設定したグループ[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

AD FS 管理コンソールまたは Windows PowerShell を使用して MFA ポリシーを設定することができます。

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用して 'claimapp' 用のユーザーのグループ メンバーシップ データに基づく MFA ポリシーを構成するには

1.  AD FS の管理コンソールで、フェデレーション サーバーに移動**認証ポリシー**\\**あたり証明書利用者信頼**ノードを展開し、証明書利用者信頼を表す、サンプル アプリケーションを選択 (**claimapp**)。

2.  いずれか、**アクション**ページ、または右クリックして**claimapp**[**カスタム多要素認証の編集**します。

3.  **証明書利用者の信頼の編集 claimapp** ] ウィンドウで、をクリックして、**追加**ボタンの横に、**ユーザー/グループ**一覧します。 入力**Finance**で作成した AD グループの名前を[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)、] をクリック**名前の確認**、名前が解決されたら、] をクリック**OK**します。

4.  をクリックして**OK**で、**証明書利用者の信頼の編集 claimapp**ウィンドウ。

##### <a name="to-configure-the-mfa-policy-based-on-users-group-membership-data-for-claimapp--via-windows-powershell"></a>Windows PowerShell を使用して 'claimapp' 用のユーザーのグループ メンバーシップ データに基づく MFA ポリシーを構成するには

1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。

    ```
    $rp = Get-AdfsRelyingPartyTrust -Name claimapp
    ```

2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。

    ```
    $GroupMfaClaimTriggerRule = 'c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i) <group_SID>$"] => issue(Type = "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", Value = "https://schemas.microsoft.com/claims/multipleauthn");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -AdditionalAuthenticationRules $GroupMfaClaimTriggerRule

    ```

    > [!NOTE]
    > < Group_SID > を AD グループの SID の値に置き換えます確認**Finance**します。

## <a name="BKMK_4"></a>手順 4: MFA メカニズムを確認します。
この手順では、前の手順で設定した MFA 機能を確認します。 次の手順を使用していることを確認することができます**Robert Hatley** AD ユーザーはサンプル アプリケーションにアクセスできるし、今回は MFA を受けるために属しているために必要な**Finance**グループ。

1.  クライアント コンピューターに、ブラウザー ウィンドウを開き、サンプル アプリケーションに移動します。 **https://webserv1.contoso.com/claimapp**します。

    この操作が自動的に要求をフェデレーション サーバーにリダイレクトし、ユーザー名とパスワードを使用してサインインを求められます。

2.  資格情報を入力、 **Robert Hatley** AD アカウントです。

    この時点では、ユーザーはポリシーのため、MFA を構成している、追加の認証を受けるに求められます。 既定のメッセージ テキストは**セキュリティ上の理由から、アカウントを検証するための追加情報が必要です。** ただし、このテキストはカスタマイズできます。 サインイン エクスペリエンスをカスタマイズする方法の詳細については、次を参照してください。 [AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。

    追加の認証方法として証明書の認証を構成する場合、既定のメッセージ テキストは**に認証を使用する証明書を選択します。操作をキャンセルする場合は、お使いのブラウザーを閉じて、もう一度やり直してくださいしてください。**

    追加の認証方法として Windows Azure Multi-factor Authentication を構成する場合、既定のメッセージ テキストは**、電話、認証を完了するには電話がかけられます。** Windows Azure Multi-factor Authentication でのサインインおよび優先検証方法のさまざまなオプションの使用に関する詳細については、次を参照してください。 [Windows Azure Multi-factor Authentication の概要](https://technet.microsoft.com/library/dn249479.aspx)します。

## <a name="see-also"></a>参照してください。
[追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



