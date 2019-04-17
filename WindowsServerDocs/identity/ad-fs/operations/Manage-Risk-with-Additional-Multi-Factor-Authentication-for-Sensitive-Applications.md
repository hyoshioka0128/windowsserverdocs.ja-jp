---
ms.assetid: 934ac796-e2ee-490d-8265-6a818be5ee79
title: "追加の多要素認証による個人情報アプリケーションのリスクを管理します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e9ee275e6fe38005394cd071e9cfe9a7999350e8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-additional-multi-factor-authentication-for-sensitive-applications"></a>追加の多要素認証による個人情報アプリケーションのリスクを管理します。

>Windows Server 2012 R2 の適用対象:


-   [Windows Server 2012 R2 の AD FS のラボ環境を設定します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)

-   [チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理します。](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

-   [AD FS の追加の認証方法を構成します。](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

## <a name="in-this-guide"></a>このガイドで
このガイドでは、次の情報を提供します。

-   [AD FS での認証メカニズム](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_1)-Windows Server 2012 R2 で Active の Directory フェデレーション サービス (AD FS) で使用できる認証メカニズムの説明

-   [シナリオの概要](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md#BKMK_2)-ユーザーのグループ メンバーシップに基づいて多要素認証 (MFA) を有効にする Active Directory フェデレーション サービス (AD FS) を使用するシナリオの説明。

    > [!NOTE]
    > Windows Server 2012 R2 で AD FS では、ネットワークの場所、デバイス id、およびユーザー ID またはグループ メンバーシップに基づく MFA を有効にできます。

    構成して、このシナリオを確認する手順については詳細な手順について、次を参照してください。[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。

## <a name="BKMK_1"></a>主要な概念 - AD FS での認証メカニズム

### <a name="benefits-of-authentication-mechanisms-in-ad---fs"></a>AD FS での認証メカニズムの利点
Active Directory フェデレーション サービス (AD FS) Windows Server 2012 R2 では、企業リソースにアクセスするユーザーを認証の IT 管理者に柔軟性の高い、高度な一連のツールを提供します。 柔軟に制御はプライマリと追加の認証方法を持つ管理者の支援、認証を構成するための豊富な管理エクスペリエンス ポリシーをユーザー インターフェイスと Windows PowerShell)、およびアプリケーションと AD FS によって保護されたサービスにアクセスするエンド ユーザーのエクスペリエンスの向上を提供します。 一部のアプリケーションと Windows Server 2012 R2 の AD FS サービスのセキュリティ保護の利点を次に示します。

-   グローバル認証ポリシーの一元管理の機能、IT 管理者は、選択可能などのような認証方法は、保護されたリソースにアクセスするネットワークの場所に基づくユーザーの認証に使用されます。 これにより、管理者は、次の操作をします。

    -   エクストラネットからアクセス要求に対してより安全な認証方法の使用を強制します。

    -   シームレスな第 2 要素認証に対してデバイス認証を有効にします。 これにより、保護されたリソースにアクセスする前により安全な複合 ID 検証をられ、リソースにアクセスするために使用している登録済みデバイスにユーザーの id。

        > [!NOTE]
        > シームレスな第 2 要素認証および SSO としてデバイス オブジェクト、デバイス登録サービス、ワークプ レース ジョイン、およびデバイスに関する詳細については、次を参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

    -   すべてのエクストラネット アクセス用の MFA 要件を設定またはユーザーの id、ネットワークの場所または保護されたリソースにアクセスするために使用するデバイスに基づく条件付きでします。

-   柔軟な認証ポリシーの構成: ビジネス価値をさまざまな AD FS で保護されたリソースのカスタム認証ポリシーを構成することができます。 たとえば、ビジネスに大きな影響を与えるアプリケーションに対して MFA を要求できます。

-   使いやすさ: GUI ベースの AD FS 管理] MMC スナップインや Windows PowerShell コマンドレットなどのシンプルで直感的な管理ツールを IT 管理者に比較的簡単に認証ポリシーを構成を有効にします。 Windows powershell では、スクリプトの日常的な管理タスクを自動化してスケールで使用するため、ソリューションを実行できます。

-   企業の資産をより細かく制御: 管理者は AD FS を使用して、特定のリソースに適用される認証ポリシーを構成することができますがある大きいため方法企業リソースの保護を制御します。 アプリケーションは、IT 管理者によって指定された認証ポリシーを上書きできません。 個人情報アプリケーションとサービスは、ことができますリソースにアクセスするたびに MFA 要件、デバイス認証、および必要に応じて新しい認証有効にします。

-   カスタム MFA プロバイダーのサポート: サード パーティの MFA 方法を活用する組織では、AD FS に組み込むし、これらの認証方法をシームレスに使用する機能を提供します。

### <a name="authentication-scope"></a>認証スコープ
Windows Server 2012 R2 で AD FS では、すべてのアプリケーションや AD FS によって保護されたサービスに適用されるグローバル スコープで認証ポリシーを指定できます。  特定のアプリケーションや AD FS によって保護された、(信頼証明書利用者) サービスの認証ポリシーを設定することもできます。 特定のアプリケーションの認証ポリシーを指定する (証明書利用者ごとの信頼) は、グローバル認証ポリシーは上書きされません。 グローバルまたは証明書利用者ごと信頼認証ポリシーには、MFA、MFA が必要ですが、ユーザーがこの証明書利用者信頼に対して認証するときにトリガーされます。  グローバル認証ポリシーは、代替の証明書利用者信頼 (アプリケーションやサービス) に構成された特定の認証ポリシーがないです。

グローバル認証ポリシーは、AD FS によって保護されたすべての利用者に適用されます。 グローバル認証ポリシーの一部として、次の設定を構成できます。

-   プライマリ認証に使用する認証方法

-   設定との MFA 方法

-   デバイスの認証が有効になっているかどうか。 詳細については、次を参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

具体的にその証明書利用者信頼 (アプリケーションやサービス) にアクセスしようとするごとに証明書利用者のパーティ信頼の認証ポリシーが適用されます。 ごとに証明書利用者信頼の認証ポリシーの一部として、次の設定を構成できます。

-   ユーザーはサインイン時に、毎回自分の資格情報を提供するために必要かどうか

-   MFA の設定に基づいて、ユーザー/グループ、デバイスの登録、およびアクセス要求の位置情報データ

### <a name="primary-and-additional-authentication-methods"></a>プライマリと追加の認証方法
管理者は、プライマリ認証メカニズムに加えて、Windows Server 2012 R2 で AD FS による追加の認証方法を構成できます。 プライマリ認証方法は組み込まれており、ユーザーの身元を確認するものです。 詳細については、ユーザーの ID が用意されていることを要求する追加の認証要素を構成し、結果としてより強力な認証を確認できます。

Windows Server 2012 R2 で AD FS でプライマリ認証とには、次のオプションがあります。

-   企業ネットワークの外部からアクセスされる公開リソースに対しては、フォーム認証は既定で選択します。 さらに、証明書の認証 (つまり、スマート カード ベースの認証または AD DS と連動するユーザー クライアント証明書の認証) をも有効にすることができます。

-   イントラネット リソースに対しては、Windows 認証は既定で選択します。 さらにフォーム認証/証明書の認証を有効にできますも。

1 つ以上の認証方法を選択すると、ユーザーに、アプリケーションまたはサービスのサインイン ページを使用して認証方法の選択に有効にします。

シームレスな第 2 要素認証に対してデバイス認証を有効にすることもできます。 これにより、保護されたリソースにアクセスする前により安全な複合 ID 検証をられ、リソースにアクセスするために使用している登録済みデバイスにユーザーの id。

> [!NOTE]
> シームレスな第 2 要素認証および SSO としてデバイス オブジェクト、デバイス登録サービス、ワークプ レース ジョイン、およびデバイスに関する詳細については、次を参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

イントラネット リソースに対して Windows 認証方法 (既定のオプション) を指定する場合、認証要求には、Windows 認証をサポートするブラウザーでシームレスにこのメソッドが行われます。

> [!NOTE]
> すべてのブラウザーでは、Windows 認証はサポートされていません。 Windows Server 2012 R2 の AD FS の認証メカニズムでは、ユーザーのブラウザーのユーザー エージェントを検出し、構成可能な設定を使用して、そのユーザー エージェントが Windows 認証をサポートしているかどうかを決定します。 管理者ユーザー エージェントのリストに追加できます (Windows PowerShell を使用して`Set-AdfsProperties -WIASupportedUserAgents`Windows 認証をサポートするブラウザーの代替ユーザー エージェント文字列を指定するために、コマンドです。 クライアントのユーザー エージェントが Windows 認証をサポートしていない場合は、フォーム認証は既定フォールバック方式です。

### <a name="configuring-mfa"></a>MFA を構成します。
Windows Server 2012 R2 の AD FS で MFA を構成する 2 つの部分があります。MFA を必須条件を指定すると、追加の認証方法を選択するとします。 追加の認証方法の詳細については、次を参照してください。[AD FS の追加認証方法を構成する](../../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)します。

**MFA の設定**

次のオプションは MFA の設定 (条件を MFA を必須とする)。

-   AD ドメインに参加しているフェデレーション サーバーの特定のユーザーとグループに対して MFA を必須とします。

-   登録済み (職場に参加している) または未登録 (職場未参加) のいずれかのときに MFA を必須とデバイス。

    Windows Server 2012 R2 は、デバイス オブジェクトが間の関係を表します最新のデバイスにユーザー中心のアプローチを要するuser@deviceと会社とします。 デバイス オブジェクトは、アプリケーションとサービスへのアクセスを提供するときに、複合 ID を提供するために使用できる Windows Server 2012 R2 で AD で新しいクラスです。 AD FS でデバイス登録サービス (DRS) の新しいコンポーネントでは、Active Directory 内のデバイス ID をプロビジョニングし、デバイス ID を表すために使用するコンシューマー デバイスに証明書を設定します。 このデバイスを使用する、職場への ID が、個人用のデバイスを職場の Active Directory に接続する、つまり、デバイスを参加させます。 個人用のデバイスを職場に参加するときに、既知のデバイスになりは保護されたリソースとアプリケーションにシームレスな第 2 要素認証を提供します。 つまり、デバイスが職場に参加するいると、ユーザーの ID はこのデバイスに関連付けられてし、保護されたリソースにアクセスする前に、シームレスな複合 ID の検証に使用できます。

    ワークプ レース ジョインおよびリーブについて詳しくは、次を参照してください。[用の SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

-   保護されたリソースに対するアクセス要求をエクストラネットまたはイントラネットのいずれかかられたとき、MFA を必須とします。

## <a name="BKMK_2"></a>シナリオの概要
このシナリオでは、特定のアプリケーションのユーザーのグループ メンバーシップ データに基づく MFA を有効にします。 つまりを設定する認証ポリシーをフェデレーション サーバーで、特定のグループに属しているユーザーが Web サーバーでホストされている特定のアプリケーションへのアクセスを要求すると、MFA を必要とします。

具体的には、このシナリオで有効にするという要求ベースのテスト アプリケーションの認証ポリシー **claimapp**それにより、AD ユーザー **Robert Hatley**を AD グループに属しているために、MFA を受ける必要があります**Finance**します。

セットアップし、このシナリオを確認する手順で手順については、「[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。 このチュートリアルの手順を完了するためには必要があります、ラボ環境を設定し、手順に従います[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

その他のシナリオの AD FS で MFA を有効にすると、次のとおりです。

-   エクストラネットからアクセス要求が送られた場合に、MFA を有効にします。 「MFA ポリシーの設定」セクションで示しているコードを変更する[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次の。

    ```
    'c:[type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", value == "false"] => issue(type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn" );'
    ```

-   非職場に参加しているデバイスからアクセス要求が送られた場合に、MFA を有効にします。  「MFA ポリシーの設定」セクションで示しているコードを変更する[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次の。

    ```
    'NOT EXISTS([type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/registrationid"]) => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

-   アクセスが職場に参加しているが、このユーザーに登録されていないのデバイスとユーザーから送られている場合に、MFA を有効にします。 「MFA ポリシーの設定」セクションで示しているコードを変更する[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)次の。

    ```
    'c:[type=="https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", value == "false"] => issue (type="https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod", value = "https://schemas.microsoft.com/claims/multipleauthn");'

    ```

## <a name="see-also"></a>参照してください。
[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスクを管理する](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)<ph x="2">
</ph>[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



