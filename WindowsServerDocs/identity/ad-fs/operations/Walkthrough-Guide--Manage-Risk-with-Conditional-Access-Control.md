---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: "チュートリアル ガイドの条件付きアクセス制御によるリスクを管理します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 11d2d567f9264dca53a3426263a172649d7d7c11
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>チュートリアル ガイド: 条件付きアクセス制御によるリスクを管理します。

>Windows Server 2012 R2 の適用対象:


## <a name="about-this-guide"></a>このガイドについて
このチュートリアルでは、Active Directory フェデレーション サービス (AD FS) Windows Server 2012 R2 での条件付きアクセス制御メカニズムを通じて使用可能な要素 (ユーザー データ) のいずれかのリスクを管理するための指示を提供します。 Windows Server 2012 R2 で AD FS での条件付きアクセス制御と認証メカニズムの詳細については、次を参照してください。[条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)します。

このチュートリアルでは、次のセクションで構成されます。

-   [手順 1: ラボ環境のセットアップ](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [手順 2: AD FS の既定のアクセス制御メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [手順 3: ユーザー データに基づく条件付きアクセス制御ポリシーを構成します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [手順 4: 条件付きアクセス制御メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>手順 1: ラボ環境のセットアップ
このチュートリアルを完了するためには、次のコンポーネントで構成される環境が必要です。

-   テスト ユーザーとグループ アカウント、Windows Server 2012 R2 または Windows Server 2012 R2 で実行されている Active Directory ドメインをアップグレード対象のスキーマと Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されている Active Directory ドメイン

-   Windows Server 2012 R2 で実行されているフェデレーション サーバー

-   サンプル アプリケーションをホストする web サーバー

-   元のサンプル アプリケーションにアクセスできるクライアント コンピューター

> [!WARNING]
> 強くお勧め (運用環境またはテスト環境での両方) も、フェデレーション サーバーと web サーバーを同じコンピューターを使用しないことです。

この環境では、フェデレーション サーバーは、ユーザーが、サンプル アプリケーションにアクセスできるように必要とされる信頼性情報を発行します。 Web サーバーは、フェデレーション サーバーが発行した要求を提示するユーザーを信頼するサンプル アプリケーションをホストします。

この環境をセットアップする方法については、次を参照してください。 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

## <a name="BKMK_2"></a>手順 2: AD FS の既定のアクセス制御メカニズムを確認します。
この手順では、既定で、ユーザーは、AD FS サインイン ページにリダイレクトは、AD FS アクセス制御メカニズムが有効な資格情報を入力し、アプリケーションへのアクセス権が付与を確認します。 使用することができます、 **Robert Hatley** AD アカウントと**claimapp**サンプル アプリケーションで構成した[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>AD FS のアクセス制御メカニズムを既定値を確認するには

1.  クライアント コンピューターに、ブラウザー ウィンドウを開き、サンプル アプリケーションに移動します。 **https://webserv1.contoso.com/claimapp**します。

    この操作が自動的に要求をフェデレーション サーバーにリダイレクトし、ユーザー名とパスワードを使用してサインインを求められます。

2.  資格情報を入力、 **Robert Hatley**で作成した AD アカウント[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

## <a name="BKMK_3"></a>手順 3: ユーザー データに基づく条件付きアクセス制御ポリシーを構成します。
この手順では、ユーザーのグループ メンバーシップ データに基づくアクセス制御ポリシーを設定します。 つまり、構成する、**発行承認規則**証明書利用者信頼を表す、サンプル アプリケーションでのフェデレーション サーバーで**claimapp**します。 この規則のロジックにより、 **Robert Hatley** AD ユーザーに属しているために、このアプリケーションにアクセスするために必要な要求を発行する、 **Finance**グループ。 追加した、 **Robert Hatley**アカウントを**Finance**グループに[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

いずれかの AD FS 管理コンソールを使用してこのタスクを完了することができます、または Windows PowerShell を使用しています。

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用してユーザー データに基づく条件付きアクセス制御ポリシーを構成するには

1.  移動し、AD FS 管理コンソールで**信頼関係**、し、**証明書利用者信頼**します。

2.  サンプル アプリケーションを表す証明書利用者のパーティ信頼を選択 (**claimapp**)、し、**アクション**ウィンドウまたはこの証明書利用者信頼を右クリックして、選択**要求規則の編集**します。

3.  **Claimapp の要求規則の編集**ウィンドウで、**発行承認規則**タブし、をクリックして**規則の追加**します。

4.  **追加発行承認要求規則ウィザード**] の [、**規則テンプレートの選択] ページ**[**の許可または拒否に基づいてユーザー入力方向の要求**要求規則テンプレートをクリックして**[次へ]**します。

5.  **規則の構成**] ページで、次のすべてを実行して、をクリックして**完了**:

    1.  たとえば、要求規則の名前を入力**TestRule**します。

    2.  選択**グループ SID**として**入力方向の要求の種類**します。

    3.  をクリックして**参照**に入力**Finance**広告の名前のテスト グループ、および解決、**入力方向の要求値**フィールド。

    4.  選択、**この入力方向の要求を持つユーザーにアクセス権の拒否**オプションです。

6.  **Claimapp の要求規則の編集**ウィンドウで、削除することを確認、**すべてのユーザーへのアクセスを許可**が、この証明書利用者信頼を作成したときに既定で作成されたルール。

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>Windows PowerShell を使用してユーザー データに基づく条件付きアクセス制御ポリシーを構成するには

1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。


    `$rp = Get-AdfsRelyingPartyTrust -Name claimapp`


2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。


    `$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
    Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`

> [!NOTE]
> 広告の SID の値に置き換える必要 < group_SID > を必ず**Finance**グループ。

## <a name="BKMK_4"></a>手順 4: 条件付きアクセス制御メカニズムを確認します。
この手順では、前の手順で設定した条件付きアクセス制御ポリシーを確認します。 次の手順を使用していることを確認することができます**Robert Hatley** AD ユーザーに属しているためサンプル アプリケーションにアクセスできます、 **Finance**グループとに属していない AD ユーザー、 **Finance**グループは、サンプル アプリケーションにアクセスできません。

1.  クライアント コンピューターに、ブラウザー ウィンドウを開き、サンプル アプリケーションに移動します**https://webserv1.contoso.com/claimapp。**

    この操作が自動的に要求をフェデレーション サーバーにリダイレクトし、ユーザー名とパスワードを使用してサインインを求められます。

2.  資格情報を入力、 **Robert Hatley**で作成した AD アカウント[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

3.  属していない別の AD ユーザーの資格情報を入力、 **Finance**グループ。 (AD でユーザー アカウントを作成する方法について詳しくは、次を参照してください。[https://technet.microsoft.com/library/cc7833232.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)します。

    この時点では、前の手順で設定したアクセス制御ポリシー、ため、「アクセスが拒否されました」メッセージが表示に属していない AD ユーザー、 **Finance**グループ。 既定のメッセージ テキストは**このサイトにアクセスする権限がありません。ここをクリックしてサインアウトし、もう一度サインインまたはアクセス許可を管理者に連絡します。** ただし、このテキストはカスタマイズできます。 サインイン エクスペリエンスをカスタマイズする方法の詳細については、次を参照してください。 [AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。

## <a name="see-also"></a>参照してください。
[条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
[Windows Server 2012 R2 の AD FS のラボ環境を設定](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



