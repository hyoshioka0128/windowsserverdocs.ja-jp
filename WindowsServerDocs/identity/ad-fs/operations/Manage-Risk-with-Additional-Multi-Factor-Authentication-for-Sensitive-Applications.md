---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: 追加の多要素認証による個人情報アプリケーションのリスク管理
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: dc6608713ddd60d20b0b717d4133d93d23fc7b25
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816255"
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>追加の多要素認証による個人情報アプリケーションのリスク管理




-   [Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [AD FS の追加の認証方法を構成する](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>このガイドの内容
このガイドでは、次の情報を提供します。

-   [AD FS の認証メカニズム](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1)-Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) で使用できる認証メカニズムについて説明します。

-   [シナリオの概要](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)-Active Directory フェデレーションサービス (AD FS) (AD FS) を使用して、ユーザーのグループメンバーシップに基づいて多要素認証 (MFA) を有効にするシナリオの説明。

    > [!NOTE]
    > Windows Server 2012 R2 の AD FS では、ネットワークの場所、デバイス id、ユーザー id またはグループメンバーシップに基づいて MFA を有効にすることができます。

    このシナリオの構成と確認の詳細な手順については、「[チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)」を参照してください。

## <a name="key-concepts---authentication-mechanisms-in-ad-fs"></a><a name="BKMK_1"></a>主要な概念-AD FS の認証メカニズム

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>AD FS での認証メカニズムの利点
Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS) (AD FS) を使用すると、IT 管理者は、会社のリソースにアクセスするユーザーを認証するための、より豊富で柔軟なツールセットを提供できます。 これにより、管理者はプライマリと追加の認証方法を柔軟に制御できるようになり、認証ポリシー (ユーザーインターフェイスと Windows PowerShell の両方) を構成するための豊富な管理エクスペリエンスが提供され、AD FS によって保護されたアプリケーションやサービスにアクセスするエンドユーザーのエクスペリエンスが向上します。 Windows Server 2012 R2 で AD FS を使用してアプリケーションとサービスをセキュリティで保護する利点の一部を次に示します。

-   グローバル認証ポリシー-一元的な管理機能。 IT 管理者は、保護されたリソースへのアクセス元のネットワークの場所に基づいてユーザーを認証するために使用する認証方法を選択できます。 これにより、管理者は次のことを実行できます。

    -   エクストラネットへのアクセス要求に対してより安全な認証方法の使用を必須とする。

    -   シームレスな 2 要素認証に対してデバイス認証を有効にする。 これにより、リソースへのアクセスに使用される登録済みデバイスにユーザー id が関連付けられるため、保護されたリソースにアクセスする前に、より安全な複合 id の検証を行うことができます。

        > [!NOTE]
        > デバイスオブジェクト、デバイス登録サービス、Workplace Join、およびシームレスな2要素認証と SSO としてのデバイスの詳細については、「[任意のデバイスからの職場への参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

    -   保護されたリソースにアクセスするために使用されるユーザーの id、ネットワークの場所、またはデバイスに基づいて、すべてのエクストラネットアクセスまたは条件付きで MFA 要件を設定します。

-   認証ポリシーの構成の柔軟性の向上: さまざまなビジネス価値を持つ AD FS 保護されたリソースに対してカスタム認証ポリシーを構成できます。 たとえば、ビジネスに大きな影響を与えるアプリケーションに対して MFA を必須とすることができます。

-   使いやすさ: GUI ベースの AD FS 管理 MMC スナップインや Windows PowerShell コマンドレットなどのシンプルで直感的な管理ツールにより、IT 管理者は、比較的簡単に認証ポリシーを構成できます。 Windows PowerShell でスクリプトを作成して、使用中のソリューションの代わりに使用したり、日常的な管理タスクを自動化したりできます。

-   企業資産のより詳細な制御: 管理者は AD FS を使用して、特定のリソースに適用される認証ポリシーを構成できるため、企業リソースの保護方法をより詳細に制御できます。 アプリケーションでは、IT 管理者によって指定された認証ポリシーを上書きすることはできません。 個人情報アプリケーションおよびサービスでは、リソースがアクセスされるたびに、MFA の要件、デバイス認証、さらに必要に応じて新しい認証を有効にすることができます。

-   カスタム MFA プロバイダーのサポート: サードパーティの MFA 方法を利用している組織の場合、AD FS は、これらの認証方法をシームレスに組み込んで使用する機能を提供します。

### <a name="authentication-scope"></a>認証スコープ
Windows Server 2012 R2 の AD FS では、AD FS によって保護されているすべてのアプリケーションとサービスに適用されるグローバルスコープで認証ポリシーを指定できます。  また、AD FS によって保護されている特定のアプリケーションとサービス (証明書利用者信頼) に対して認証ポリシーを設定することもできます。 特定のアプリケーションの認証ポリシー (証明書利用者信頼ごと) を指定しても、グローバル認証ポリシーは上書きされません。 認証ポリシーがグローバルであっても、証明書利用者信ごとであっても、MFA が必要である場合、ユーザーがこの証明書利用者信頼に対して認証しようとすると、MFA がトリガーされます。  グローバル認証ポリシーは、特定の認証ポリシーが構成されていない証明書利用者信頼 (アプリケーションやサービス) に適用される代替の認証ポリシーです。

グローバル認証ポリシーは、AD FS によって保護されているすべての証明書利用者に適用されます。 グローバル認証ポリシーの一部として次の設定を構成できます。

-   プライマリ認証に使用する認証方法。

-   MFA に使用する設定と方法。

-   デバイス認証を有効にするかどうか。 詳細については、「 [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

証明書利用者信頼ごとの認証ポリシーは、該当する証明書利用者信頼 (アプリケーションやサービス) にアクセスしようとするときにのみ適用されます。 証明書利用者信頼ごとの認証ポリシーの一部として次の設定を構成できます。

-   ユーザーがサインインするたびに資格情報を入力する必要があるかどうか。

-   ユーザー/グループ、デバイスの登録、アクセス要求の位置データに基づく MFA の設定。

### <a name="primary-and-additional-authentication-methods"></a>プライマリと追加の認証方法
Windows Server 2012 R2 の AD FS では、プライマリ認証メカニズムに加えて、管理者は追加の認証方法を構成できます。 プライマリ認証方法は組み込みであり、ユーザーの id を検証することを目的としています。 追加の認証要素を構成して、ユーザーの id に関する詳細情報を要求することができます。その結果、より強力な認証が保証されます。

Windows Server 2012 R2 の AD FS でプライマリ認証を使用する場合、次のオプションがあります。

-   企業ネットワークの外部からアクセスされる公開リソースに対しては、フォーム認証が既定で選択されます。 さらに、証明書の認証 (スマート カード ベースの認証、または AD DS と連動するユーザー クライアント証明書の認証) を有効にすることもできます。

-   イントラネット リソースに対しては、Windows 認証が既定で選択されます。 さらに、フォーム認証/証明書の認証を有効にすることもできます。

複数の認証方法を選択することで、アプリケーションやサービスのサインイン ページで、ユーザーに認証方法のオプションを提供できます。

また、シームレスな 2 要素認証に対してデバイス認証を有効にすることもできます。 これにより、リソースへのアクセスに使用される登録済みデバイスにユーザー id が関連付けられるため、保護されたリソースにアクセスする前に、より安全な複合 id の検証を行うことができます。

> [!NOTE]
> デバイスオブジェクト、デバイス登録サービス、Workplace Join、およびシームレスな2要素認証と SSO としてのデバイスの詳細については、「[任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

イントラネット リソースに対して Windows 認証方法 (既定のオプション) を指定した場合、Windows 認証をサポートするブラウザーで認証を要求したユーザーはシームレスにこの方法で認証を受けます。

> [!NOTE]
> Windows 認証は一部のブラウザーではサポートされていません。 Windows Server 2012 R2 の AD FS の認証メカニズムにより、ユーザーのブラウザーユーザーエージェントが検出され、構成可能な設定を使用して、そのユーザーエージェントが Windows 認証をサポートしているかどうかが判断されます。 管理者は、Windows 認証をサポートするブラウザーの代替ユーザー エージェントの文字列をユーザー エージェントのリストに追加して指定できます (Windows PowerShell の `Set-AdfsProperties -WIASupportedUserAgents` コマンドを使用)。 クライアントのユーザーエージェントが Windows 認証をサポートしていない場合、既定のフォールバック方法はフォーム認証です。

### <a name="configuring-mfa"></a>MFA の構成
Windows Server 2012 R2 の AD FS で MFA を構成するには、次の2つの部分があります。 MFA を必要とする条件を指定し、追加の認証方法を選択します。 追加の認証方法の詳細については、「 [AD FS の追加の認証方法を構成する](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)」を参照してください。

**MFA の設定**

次のオプションは MFA の設定 (MFA を必須とする条件) で使用できます。

-   フェデレーション サーバーが参加している AD ドメイン内の特定のユーザーとグループに対して MFA を必須とする。

-   登録済み (職場参加済み) または未登録 (職場未参加) のデバイスに対して MFA を必須とする。

    Windows Server 2012 R2 は、最新のデバイスへのユーザー中心のアプローチを採用しています。デバイスオブジェクトは、user@device と会社の間の関係を表します。 デバイスオブジェクトは、Windows Server 2012 R2 の AD の新しいクラスであり、アプリケーションやサービスへのアクセスを提供するときに、複合 id を提供するために使用できます。 AD FS の新しいコンポーネントであるデバイス登録サービス (DRS) は、Active Directory 内のデバイス ID をプロビジョニングし、一般ユーザー向けデバイスのデバイス ID を表すために使用される証明書を設定します。 このデバイス ID を使用してデバイスを職場に参加させることができます。つまり、個人のデバイスを職場の Active Directory に接続できます。 個人用のデバイスを職場に参加させると、それらのデバイスは既知のデバイスになり、保護済みのリソースやアプリケーションでは、シームレスな 2 要素認証を使用できるようになります。 つまり、デバイスが職場に参加した後、ユーザーの id はこのデバイスに関連付けられ、保護されたリソースにアクセスする前に、シームレスな複合 id の検証に使用できます。

    Workplace join と leave の詳細については、「[任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

-   保護済みリソースに対するアクセス要求をエクストラネットまたはイントラネットのいずれかから行うときは、MFA を必須とすることができます。

## <a name="scenario-overview"></a><a name="BKMK_2"></a>シナリオの概要
このシナリオでは、特定のアプリケーションのユーザーのグループメンバーシップデータに基づいて MFA を有効にします。 つまり、特定のグループに属するユーザーが、Web サーバーでホストされている特定のアプリケーションへのアクセスを要求するときに、MFA を必須とするように、フェデレーション サーバーで認証ポリシーを設定します。

具体的には、このシナリオでは、**claimapp** という要求ベースのテスト アプリケーションの認証ポリシーを有効にします。それにより、AD ユーザー **Robert Hatley** は、AD グループ **Finance** に属しているため、MFA を受けることが必須となります。

このシナリオをセットアップして確認する手順については、 [「チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)」を参照してください。 このチュートリアルの手順を完了するには、ラボ環境を設定し、「 [Windows Server 2012 R2 の AD FS 用のラボ環境](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)をセットアップする」の手順に従ってください。

AD FS で MFA を有効にするその他のシナリオを次に示します。

-   アクセス要求がエクストラネットから送られた場合に MFA を有効にする。 「[チュートリアルガイド: 追加 Multi-Factor Authentication を使用したリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)」の「MFA ポリシーの設定」セクションに示されているコードを変更して、次の情報を確認できます。

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   アクセス要求が職場未参加のデバイスから送られた場合に MFA を有効にする。  「[チュートリアルガイド: 追加 Multi-Factor Authentication を使用したリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)」の「MFA ポリシーの設定」セクションに示されているコードを変更して、次の情報を確認できます。

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   ユーザーのデバイスが職場に参加しているがこのユーザーに登録されていない場合、そのユーザーからのアクセスがあるときは、MFA を有効にします。 「[チュートリアルガイド: 追加 Multi-Factor Authentication を使用したリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)」の「MFA ポリシーの設定」セクションに示されているコードを変更して、次の情報を確認できます。

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>参照
[チュートリアルガイド: 追加の Multi-Factor Authentication による機密アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
[Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップ](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)する



