---
ms.assetid: 3a840b63-78b7-4e62-af7b-497026bfdb93
title: 'チュートリアル ガイド: 条件付きアクセス制御によるリスクを管理します。'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7e6e1c97ccc903ca3aff558354941e6a84d3fb79
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444736"
---
# <a name="walkthrough-guide-manage-risk-with-conditional-access-control"></a>チュートリアル ガイド:条件付きアクセス制御によってリスクを管理する




## <a name="about-this-guide"></a>このガイドについて
このチュートリアルでは、Windows Server 2012 R2 で Active の Directory フェデレーション サービス (AD FS) で、条件付きアクセス制御メカニズムを通じて使用可能な要素 (ユーザー データ) のいずれかのリスクを管理するための手順を提供します。 Windows Server 2012 R2 で AD FS での条件付きアクセス制御と認証メカニズムの詳細については、次を参照してください。[条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)します。

このチュートリアルは次のセクションで構成されています。

-   [ステップ 1: ラボ環境のセットアップ](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [手順 2:AD FS の既定のアクセス制御メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

-   [手順 3:ユーザー データに基づく条件付きアクセス制御ポリシーを構成します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_3)

-   [手順 4:条件付きアクセス制御メカニズムを確認します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md#BKMK_4)

## <a name="BKMK_1"></a>手順 1:ラボ環境のセットアップ
このチュートリアルを完了するには、次のコンポーネントで構成された環境が必要です。

-   テスト ユーザーとグループ アカウント、Windows Server 2012 R2 または Windows Server 2012 R2 で実行されている Active Directory ドメインにアップグレードする、スキーマを持つ、Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 で実行されている Active Directory ドメイン

-   Windows Server 2012 R2 で実行されているフェデレーション サーバー

-   サンプル アプリケーションをホストする Web サーバー。

-   サンプル アプリケーションにアクセスできるクライアント コンピューター。

> [!WARNING]
> 運用環境でもテスト環境でも、フェデレーション サーバーと Web サーバーに同じコンピューターを使用しないことを強くお勧めします。

この環境では、フェデレーション サーバーは、ユーザーがサンプル アプリケーションにアクセスできるように、必要な要求を発行します。 Web サーバーはサンプルのアプリケーションをホストします。このアプリケーションは、フェデレーション サーバーが発行した要求を提示するユーザーを信頼します。

このような環境を設定する方法については、次を参照してください。 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

## <a name="BKMK_2"></a>手順 2:AD FS の既定のアクセス制御メカニズムを確認する
この手順では、AD FS の既定のアクセス制御メカニズムにより、ユーザーが AD FS のサインイン ページにリダイレクトされ、有効な資格情報を入力するとアプリケーションへのアクセスが許可されることを確認します。 使用することができます、 **Robert Hatley** AD アカウントと **claimapp** サンプル アプリケーションで構成した [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

#### <a name="to-verify-the-default-ad-fs-access-control-mechanism"></a>AD FS の既定のアクセス制御メカニズムを確認するには

1.  クライアント コンピューターに、ブラウザー ウィンドウを開くし、サンプル アプリケーションに移動します:  **https://webserv1.contoso.com/claimapp** します。

    この操作により、要求がフェデレーション サーバーの役割に自動的にリダイレクトされた後、ユーザー名とパスワードでサインインするように求められます。

2.  資格情報を入力、 **Robert Hatley** で作成した AD アカウント [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

## <a name="BKMK_3"></a>手順 3:手順 3: ユーザー データに基づく条件付きアクセス制御ポリシーを構成する
この手順では、ユーザーのグループ メンバーシップ データに基づくアクセス制御ポリシーを設定します。 つまり、サンプル アプリケーションである **claimapp** を表す証明書利用者信頼について、フェデレーション サーバーで **発行承認規則**を構成します。 この規則のロジックにより、 **Robert Hatley**に属しているため、このアプリケーションにアクセスするために必要なクレームが AD ユーザーに発行されます、 **Finance**グループ。 追加した、 **Robert Hatley**アカウントを**Finance**グループ[Windows Server 2012 R2 で AD FS のラボ環境をセットアップ](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

AD FS 管理コンソールまたは Windows PowerShell のいずれかを使用してこのタスクを完了できます。

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-the-ad-fs-management-console"></a>AD FS 管理コンソールを使用して、ユーザー データに基づく条件付きアクセス制御ポリシーを構成するには

1.  AD FS 管理コンソールで、 **[信頼関係]** 、 **[証明書利用者信頼]** の順に移動します。

2.  サンプル アプリケーション (**claimapp**) を表す証明書利用者信頼を選択し、 **[操作]** ウィンドウで、またはこの証明書利用者信頼を右クリックして、 **[要求規則の編集]** を選択します。

3.  **[claimapp の要求規則の編集]** ウィンドウで、 **[発行承認規則]** タブを選択し、 **[規則の追加]** をクリックします。

4.  **発行承認要求規則の追加ウィザード**の **[規則テンプレートの選択]** ページで、 **[入力方向の要求に基づいてユーザーを許可または拒否]** 要求規則テンプレートを選択し、 **[次へ]** をクリックします。

5.  **[規則の構成]** ページで、次のすべての操作を実行してから、 **[完了]** をクリックします。

    1.  要求規則の名前 (**TestRule** など) を入力します。

    2.  **[入力方向の要求の種類]** として **[グループ SID]** を選択します。

    3.  **[参照]** をクリックし、AD テスト グループの名前として「 **Finance** 」と入力します。この名前は **[入力方向の要求の値]** に解決されます。

    4.  **[この入力方向の要求を行ったユーザーのアクセスを拒否]** オプションを選択します。

6.  **[claimapp の要求規則の編集]** ウィンドウで、この証明書利用者信頼を作成したときに既定で作成された **[すべてのユーザーにアクセス許可]** 規則を必ず削除します。

#### <a name="to-configure-conditional-access-control-policy-based-on-user-data-via-windows-powershell"></a>Windows PowerShell を使用して、ユーザー データに基づく条件付きアクセス制御ポリシーを構成するには

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。


~~~
`$rp = Get-AdfsRelyingPartyTrust -Name claimapp`
~~~


2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。


~~~
`$GroupAuthzRule = '@RuleTemplate = "Authorization" @RuleName = "Foo" c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "^(?i)<group_SID>$"] =>issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");'
Set-AdfsRelyingPartyTrust -TargetRelyingParty $rp -IssuanceAuthorizationRules $GroupAuthzRule`
~~~

> [!NOTE]
> <group_SID> を必ず AD グループ **Finance** の SID の値に置き換えます。

## <a name="BKMK_4"></a>手順 4:条件付きアクセス制御メカニズムを確認する
この手順では、前の手順で設定した条件付きアクセス制御ポリシーを確認します。 次の手順を使用して、**Finance** グループに属している AD ユーザー **Robert Hatley** はサンプル アプリケーションにアクセスでき、**Finance** グループに属していない AD ユーザーはサンプル アプリケーションにアクセスできないことを確認できます。

1.  クライアント コンピューターに、ブラウザー ウィンドウを開き、サンプル アプリケーションに移動します。 **https://webserv1.contoso.com/claimapp**

    この操作により、要求がフェデレーション サーバーの役割に自動的にリダイレクトされた後、ユーザー名とパスワードでサインインするように求められます。

2.  資格情報を入力、 **Robert Hatley** で作成した AD アカウント [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

    アプリケーションへのアクセスが許可されます。

3.  **Finance** グループに属していない別の AD ユーザーの資格情報を入力します (AD でユーザー アカウントを作成する方法の詳細については、次を参照してください。 [ https://technet.microsoft.com/library/cc7833232.aspx](https://technet.microsoft.com/library/cc783323%28v=ws.10%29.aspx)します。

    この時点では、前の手順で設定したアクセス制御ポリシー、ため、'アクセス拒否' メッセージが表示されますに属していない AD ユーザーはこの、 **Finance**グループ。 既定のメッセージ テキストは**このサイトにアクセスする権限がありません。ここをクリックしてサインアウトし、もう一度サインインまたはアクセス許可については、管理者にお問い合わせください。** " です。ただし、このテキストはカスタマイズできます。 サインイン エクスペリエンスのカスタマイズ方法については、「 [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)」を参照してください。

## <a name="see-also"></a>関連項目
[条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
[Windows Server 2012 R2 で AD FS のラボ環境のセットアップ](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



