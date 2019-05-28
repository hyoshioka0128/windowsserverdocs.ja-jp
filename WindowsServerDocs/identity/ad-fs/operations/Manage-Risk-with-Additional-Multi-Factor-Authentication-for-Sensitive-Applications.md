---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: 追加の多要素認証による個人情報アプリケーションのリスク管理
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a37c0b0a1de06b65e0cb867ec4d160bbb0373a15
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189072"
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>追加の多要素認証による個人情報アプリケーションのリスク管理




-   [Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [チュートリアル ガイド: 機密性の高いアプリケーションの追加の多要素認証によるリスクを管理します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [AD FS の追加の認証方法を構成します。](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>このガイドについて
このガイドでは、次の情報を提供します。

-   [AD FS での認証メカニズム](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1)-Windows Server 2012 R2 で Active の Directory フェデレーション サービス (AD FS) で使用できる認証メカニズムの説明

-   [シナリオの概要](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)-ユーザーのグループ メンバーシップに基づいて多要素認証 (MFA) を有効にする Active Directory フェデレーション サービス (AD FS) を使用するシナリオの説明。

    > [!NOTE]
    > Windows Server 2012 R2 で AD FS では、ネットワークの場所、デバイス id、およびユーザーの id またはグループのメンバーシップに基づく MFA を有効にできます。

    構成してこのシナリオを確認する詳細なステップ バイ ステップ チュートリアルについては、次を参照してください。[チュートリアル ガイド。機密性の高いアプリケーションの追加の多要素認証によるリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。

## <a name="BKMK_1"></a>主要な概念 - AD FS での認証メカニズム

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>AD FS での認証メカニズムの利点
Active Directory フェデレーション サービス (AD FS) Windows Server 2012 R2 では、企業リソースにアクセスするユーザーを認証するための柔軟性の高い、高度な一連のツールを IT 管理者を提供します。 プライマリと追加の認証方法に柔軟な制御により、認証を構成するための豊富な管理エクスペリエンス ポリシー (両方のユーザー インターフェイスと Windows PowerShell を通じて) についてを提供し、強化アプリケーションと AD FS によって保護されているサービスにアクセスするエンドユーザーのエクスペリエンス。 Windows Server 2012 R2 で AD FS サービス、アプリケーションを保護する利点の一部を次に示します。

-   グローバル認証ポリシー - サーバーの全体管理機能は、どのような認証方法は、保護されたリソースのアクセスに使用するネットワークの場所に基づくユーザーを認証に使用元となる IT 管理者が選択できます。 これにより、管理者は次のことを実行できます。

    -   エクストラネットへのアクセス要求に対してより安全な認証方法の使用を必須とする。

    -   シームレスな 2 要素認証に対してデバイス認証を有効にする。 これには、保護されたリソースにアクセスする前にそのためより安全な複合 id の検証を提供するリソースへのアクセスに使用される登録済みデバイスに、ユーザーの id が結び付いています。

        > [!NOTE]
        > シームレスな第 2 要素認証および SSO としてのデバイス オブジェクト、デバイス登録サービス、ワークプ レース ジョイン、およびデバイスの詳細については、次を参照してください[SSO およびシームレスな第 2 要素認証の任意のデバイスから社内への参加。会社のアプリケーション間で](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

    -   すべてのエクストラネット アクセス用の MFA 要件を設定またはユーザーの id、ネットワークの場所または保護されたリソースへのアクセスに使用されるデバイスに基づいて条件付きでします。

-   柔軟な認証ポリシーの構成: ビジネス価値をさまざまな AD FS で保護されたリソースのカスタム認証ポリシーを構成することができます。 たとえば、ビジネスに大きな影響を与えるアプリケーションに対して MFA を必須とすることができます。

-   使いやすさ: GUI ベースの AD FS の管理 MMC スナップインや Windows PowerShell コマンドレットなどのシンプルで直感的な管理ツールには、比較的簡単に認証ポリシーを構成する IT 管理者が有効にします。 Windows PowerShell でスクリプトを作成して、使用中のソリューションの代わりに使用したり、日常的な管理タスクを自動化したりできます。

-   企業資産をより細かく制御: 管理者は AD FS を使用するには、特定のリソースに適用される認証ポリシーを構成するがある大きいために制御による企業リソースをセキュリティで保護されています。 アプリケーションでは、IT 管理者によって指定された認証ポリシーを上書きすることはできません。 個人情報アプリケーションおよびサービスでは、リソースがアクセスされるたびに、MFA の要件、デバイス認証、さらに必要に応じて新しい認証を有効にすることができます。

-   カスタム MFA プロバイダーのサポート: サード パーティの MFA 方法を活用する組織では、AD FS を組み込み、これらの認証方法をシームレスに使用する機能を提供します。

### <a name="authentication-scope"></a>認証スコープ
Windows Server 2012 R2 で AD FS では、すべてのアプリケーションや AD FS によって保護されているサービスに適用されるグローバル スコープで認証ポリシーを指定できます。  特定のアプリケーションおよび AD FS によってセキュリティ保護された (信頼証明書利用者) サービスの認証ポリシーを設定することもできます。 特定のアプリケーションの認証ポリシー (証明書利用者信頼ごと) を指定しても、グローバル認証ポリシーは上書きされません。 認証ポリシーがグローバルであっても、証明書利用者信ごとであっても、MFA が必要である場合、ユーザーがこの証明書利用者信頼に対して認証しようとすると、MFA がトリガーされます。  グローバル認証ポリシーは、特定の認証ポリシーが構成されていない証明書利用者信頼 (アプリケーションやサービス) に適用される代替の認証ポリシーです。

グローバル認証ポリシーは、AD FS によって保護されているすべての利用者に適用されます。 グローバル認証ポリシーの一部として次の設定を構成できます。

-   プライマリ認証に使用する認証方法。

-   MFA に使用する設定と方法。

-   デバイス認証を有効にするかどうか。 詳細については、「 [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

証明書利用者信頼ごとの認証ポリシーは、該当する証明書利用者信頼 (アプリケーションやサービス) にアクセスしようとするときにのみ適用されます。 証明書利用者信頼ごとの認証ポリシーの一部として次の設定を構成できます。

-   ユーザーがサインインするたびに資格情報を入力する必要があるかどうか。

-   ユーザー/グループ、デバイスの登録、アクセス要求の位置データに基づく MFA の設定。

### <a name="primary-and-additional-authentication-methods"></a>プライマリと追加の認証方法
プライマリ認証メカニズムに加えて、Windows Server 2012 R2 で AD FS 管理者は追加の認証方法を構成できます。 プライマリ認証方法が組み込まれており、ユーザーの id を検証するものです。 詳細について、ユーザーの id が提供されることを要求する追加の認証要素を構成し、その結果より強力な認証を確認できます。

Windows Server 2012 R2 で AD FS でプライマリ認証では、次のオプションがあります。

-   企業ネットワークの外部からアクセスされる公開リソースに対しては、フォーム認証が既定で選択されます。 さらに、証明書の認証 (スマート カード ベースの認証、または AD DS と連動するユーザー クライアント証明書の認証) を有効にすることもできます。

-   イントラネット リソースに対しては、Windows 認証が既定で選択されます。 さらに、フォーム認証/証明書の認証を有効にすることもできます。

複数の認証方法を選択することで、アプリケーションやサービスのサインイン ページで、ユーザーに認証方法のオプションを提供できます。

また、シームレスな 2 要素認証に対してデバイス認証を有効にすることもできます。 これには、保護されたリソースにアクセスする前にそのためより安全な複合 id の検証を提供するリソースへのアクセスに使用される登録済みデバイスに、ユーザーの id が結び付いています。

> [!NOTE]
> シームレスな第 2 要素認証および SSO としてのデバイス オブジェクト、デバイス登録サービス、ワークプ レース ジョイン、およびデバイスの詳細については、次を参照してください[SSO およびシームレスな第 2 要素認証の任意のデバイスから社内への参加。会社のアプリケーション間で](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

イントラネット リソースに対して Windows 認証方法 (既定のオプション) を指定した場合、Windows 認証をサポートするブラウザーで認証を要求したユーザーはシームレスにこの方法で認証を受けます。

> [!NOTE]
> Windows 認証は一部のブラウザーではサポートされていません。 Windows Server 2012 R2 で AD FS での認証メカニズムは、ユーザーのブラウザー ユーザー エージェントを検出し、そのユーザー エージェントが Windows 認証をサポートしているかどうかを判断する構成可能な設定を使用します。 管理者は、Windows 認証をサポートするブラウザーの代替ユーザー エージェントの文字列をユーザー エージェントのリストに追加して指定できます (Windows PowerShell の `Set-AdfsProperties -WIASupportedUserAgents` コマンドを使用)。 クライアントのユーザー エージェントが Windows 認証をサポートしていない場合は、フォーム認証が、既定のフォールバック方法。

### <a name="configuring-mfa"></a>MFA の構成
Windows Server 2012 R2 で AD FS で MFA を構成する 2 つの部分: MFA を必須にする条件を指定して、追加の認証方法を選択します。 追加の認証方法の詳細については、次を参照してください。 [AD FS の追加の認証方法の構成](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)します。

**MFA の設定**

次のオプションは MFA の設定 (MFA を必須とする条件) で使用できます。

-   フェデレーション サーバーが参加している AD ドメイン内の特定のユーザーとグループに対して MFA を必須とする。

-   登録済み (職場参加済み) または未登録 (職場未参加) のデバイスに対して MFA を必須とする。

    Windows Server 2012 R2 を最新のデバイスをデバイス オブジェクトが間にリレーションシップを表すユーザー中心のアプローチを採用するuser@deviceと会社とします。 デバイス オブジェクトは、新しいクラスをアプリケーションとサービスへのアクセスを提供するときに、複合 id を提供するために使用する Windows Server 2012 R2 で ad です。 AD FS の新しいコンポーネントであるデバイス登録サービス (DRS) は、Active Directory 内のデバイス ID をプロビジョニングし、一般ユーザー向けデバイスのデバイス ID を表すために使用される証明書を設定します。 このデバイス ID を使用してデバイスを職場に参加させることができます。つまり、個人のデバイスを職場の Active Directory に接続できます。 個人用のデバイスを職場に参加させると、それらのデバイスは既知のデバイスになり、保護済みのリソースやアプリケーションでは、シームレスな 2 要素認証を使用できるようになります。 つまり、デバイスが職場に参加した後、ユーザーの id はこのデバイスに関連付けられているし、保護されたリソースにアクセスする前に、シームレスな複合 id の検証に使用できます。

    ワークプ レース参加と参加解除の詳細については、次を参照してください。 [SSO およびシームレスな第 2 要素認証用アプリケーション間の任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

-   保護済みリソースに対するアクセス要求をエクストラネットまたはイントラネットのいずれかから行うときは、MFA を必須とすることができます。

## <a name="BKMK_2"></a>シナリオの概要
このシナリオでは、特定のアプリケーションのユーザーのグループ メンバーシップ データに基づく MFA を有効にします。 つまり、特定のグループに属するユーザーが、Web サーバーでホストされている特定のアプリケーションへのアクセスを要求するときに、MFA を必須とするように、フェデレーション サーバーで認証ポリシーを設定します。

具体的には、このシナリオでは、**claimapp** という要求ベースのテスト アプリケーションの認証ポリシーを有効にします。それにより、AD ユーザー **Robert Hatley** は、AD グループ **Finance** に属しているため、MFA を受けることが必須となります。

設定して、このシナリオを確認するステップ バイ ステップ手順[チュートリアル ガイド。機密性の高いアプリケーションの追加の多要素認証によるリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。 このチュートリアルの手順を完了するのには必要がありますラボ環境を設定して、次の手順では、 [Windows Server 2012 R2 で AD FS のラボ環境をセットアップ](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

AD FS で MFA を有効にするには、その他のシナリオを以下に示します。

-   アクセス要求がエクストラネットから送られた場合に MFA を有効にする。 "MFA ポリシーを設定 セクションで紹介したコードを変更する[チュートリアル ガイド。追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次。

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   アクセス要求が職場未参加のデバイスから送られた場合に MFA を有効にする。  "MFA ポリシーを設定 セクションで紹介したコードを変更する[チュートリアル ガイド。追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次。

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   ユーザーのデバイスが職場に参加しているがこのユーザーに登録されていない場合、そのユーザーからのアクセスがあるときは、MFA を有効にします。 "MFA ポリシーを設定 セクションで紹介したコードを変更する[チュートリアル ガイド。追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次。

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>関連項目
[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Windows Server 2012 R2 で AD FS のラボ環境のセットアップ](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



