---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: "条件付きアクセス制御によるリスクを管理します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e2ad7d1467abd6d69077b515b8c69a65f7e70f19
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="manage-risk-with-conditional-access-control"></a>条件付きアクセス制御によるリスクを管理します。

>Windows Server 2012 R2 の適用対象:


-   [AD FS でのキーの概念条件付きアクセス制御](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [条件付きアクセス制御によるリスクを管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="BKMK_1"></a>主要な概念 - AD FS での条件付きアクセス制御
AD FS の全体的な関数では、信頼性情報のセットを含むアクセス トークンを発行します。 AD FS が許可して発行は、どのようなクレームに関する決定は、要求規則によって左右されます。

AD FS でのアクセス制御は発行承認要求規則の許可または拒否要求をユーザーかどうかを決定するに使用すると実装またはユーザーのグループができるかどうか AD FS で保護されたリソースにアクセスします。 承認規則は、証明書利用者信頼にのみ設定できます。

|規則のオプション|規則のロジック|
|---------------|--------------|
|すべてのユーザーを許可します。|入力方向の要求の種類と等しい場合*いずれかの要求の種類*等しく、値*任意の値*、要求値が発行されます*許可*|
|この入力方向の要求を持つユーザーにアクセスを許可します。|入力方向の要求の種類と等しい場合*要求の種類を指定した*等しく、値*指定した要求値*、要求値が発行されます*許可*|
|この入力方向の要求を持つユーザーにアクセス権を拒否します。|入力方向の要求の種類と等しい場合*要求の種類を指定した*等しく、値*指定した要求値*、要求値が発行されます*拒否*|

これらの規則オプションおよびロジックの詳細については、次を参照してください。[When to Use an Authorization Claim Rule](https://technet.microsoft.com/library/ee913560.aspx)します。

Windows Server 2012 R2 での AD FS では、アクセス制御は複数の要因によって、ユーザー、デバイス、位置情報、認証データなど強化されました。 これが可能になりますより多様な要求の種類によって承認要求規則を使用します。  つまり、Windows Server 2012 R2 での AD FS で強制することもユーザー ID またはグループのメンバーシップ、ネットワークの場所、デバイスに基づく条件付きアクセス制御 (ワークプ レースに参加している、詳細についてであるかどうかを参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md))、認証状態 (かどうか多要素認証 (MFA) が実行されます)。

Windows Server 2012 R2 では、AD FS での条件付きアクセス制御には次の利点があります。

-   柔軟で表現力の高いアプリケーションごとの承認ポリシー、それにより、許可またはユーザー、デバイス、ネットワークの場所、および認証状態に基づいてアクセスを拒否することができます。

-   発行の証明書利用者のパーティ製アプリケーションの承認規則を作成します。

-   一般的な条件付きアクセス制御シナリオの充実した UI エクスペリエンス

-   豊富な要求の言語と Windows PowerShell の高度な条件付きアクセス制御シナリオのサポートします。

-   カスタム (証明書利用者ごとパーティ製のアプリケーション)「アクセスが拒否されました」メッセージ。 詳細については、次を参照してください。[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)します。 これらのメッセージをカスタマイズすることでは、理由、ユーザーはアクセスが拒否されることを説明し、セルフ サービスで修復が可能であれば、たとえば、職場へのプロンプトのユーザーが自分のデバイスを参加を容易にもできます。 詳細については、次を参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。

次の表には、条件付きアクセス制御を実装するために使用する Windows Server 2012 R2 で AD FS で使用できるすべての要求種類が含まれています。

|要求の種類|説明|
|--------------|---------------|
|電子メール アドレス|ユーザーの電子メール アドレスです。|
|指定された名前|ユーザーの姓名の名です。|
|名|ユーザーの一意の名前|
|UPN|ユーザー プリンシパル名 (UPN) のユーザー。|
|共通名|ユーザーの共通名。|
|AD FS 1 x 電子メール アドレス|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの電子メール アドレス。|
|グループ|メンバーであるユーザーのグループ。|
|AD FS 1 x UPN|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの UPN です。|
|ロール|ユーザーが役割。|
|姓|ユーザーの姓します。|
|PPID|ユーザーの個人識別子。|
|名前 ID|ユーザーの SAML 名前識別子です。|
|認証のタイムスタンプ|ユーザーが認証された日付と時刻を表示するために使用します。|
|認証方法|ユーザーの認証に使用する方法。|
|拒否専用グループ SID|拒否専用グループ SID のユーザー。|
|拒否専用プライマリ SID|拒否専用プライマリ SID のユーザー。|
|拒否専用プライマリ グループ SID|拒否専用プライマリ グループのユーザーの SID。|
|グループ SID|ユーザーのグループ SID。|
|プライマリ グループ SID|ユーザーのプライマリ グループ SID。|
|プライマリ SID|ユーザーのプライマリ SID です。|
|Windows アカウント名|ドメイン \ ユーザーの形式でユーザーのドメイン アカウント名。|
|ユーザーの登録|このデバイスを使用して、ユーザーが登録されます。|
|デバイス識別子|デバイスの識別子です。|
|デバイス登録識別子|デバイスの登録の識別子。|
|デバイス登録表示名|デバイスの登録の名前を表示します。|
|デバイス OS の種類|デバイスのオペレーティング システムの種類。|
|デバイスの OS バージョン|デバイスのオペレーティング システムのバージョン。|
|デバイスの管理|デバイスは管理サービスによって管理されます。|
|転送済みクライアント IP|ユーザーの IP アドレスです。|
|クライアント アプリケーション|クライアント アプリケーションの種類。|
|クライアント ユーザー エージェント|デバイスの種類、クライアントは、アプリケーションにアクセスするを使用します。|
|クライアント IP|クライアントの IP アドレスです。|
|エンドポイント パス|エンドポイントの絶対パスがアクティブかパッシブ クライアントを特定するために使用することができます。|
|プロキシ|要求が渡されるフェデレーション サーバー プロキシの DNS 名。|
|アプリケーション識別子|証明書利用者の識別子。|
|アプリケーション ポリシー|証明書のアプリケーション ポリシー。|
|機関キー識別子|発行された証明書に署名した証明書の機関キー識別子拡張子です。|
|基本制限|証明書の基本的な制約の 1 つです。|
|拡張キー使用法|証明書の拡張キー使用法のいずれかを説明します。|
|発行者|X.509 証明書を発行した証明機関の名前。|
|発行者名|証明書の発行者の識別名。|
|キー使用法|証明書のキー使用法の 1 つです。|
|いない後|その後、証明書が有効な不要になったローカル時刻で日付です。|
|前にしません。|証明書が有効になるローカル時刻の日です。|
|証明書ポリシー|証明書が発行されたポリシー。|
|公開キー|証明書の公開キーです。|
|証明書の未処理データ|証明書の未処理データ。|
|サブジェクト代替名|証明書の代替名の 1 つです。|
|シリアル番号|証明書のシリアル番号。|
|署名アルゴリズム|証明書の署名の作成に使用されるアルゴリズム。|
|件名|証明書のサブジェクト。|
|サブジェクト キー識別子|証明書のサブジェクト キー識別子。|
|サブジェクト名|証明書のサブジェクトの識別名。|
|V2 テンプレート名|バージョン 2 証明書テンプレートの名前は、発行または証明書の更新時に使用されます。 これは、Microsoft 固有の値です。|
|V1 テンプレート名|発行または証明書を更新するときに使用するバージョン 1 の証明書テンプレートの名前。 これは、Microsoft 固有の値です。|
|拇印|証明書の拇印です。|
|X 509 バージョン|証明書の X.509 形式のバージョン。|
|企業ネットワーク内|要求が企業ネットワーク内から送られたかどうかを示すために使用されます。|
|パスワードの有効期限|パスワードの有効期限が切れる時刻を表示するために使用します。|
|パスワードの有効期限日|パスワードの有効期限を日数を表示するために使用します。|
|パスワード更新 URL|パスワード更新サービスの Web アドレスを表示するために使用します。|
|認証方法の参照|ユーザーの認証に使用される認証方法を示すために使用されます。|

## <a name="BKMK_2"></a>条件付きアクセス制御によるリスクを管理
利用可能な設定を使用して、方法は多数あります条件付きアクセス制御を実装することによってリスクを管理できます。

### <a name="common-scenarios"></a>一般的なシナリオ
たとえば、特定のアプリケーション (証明書利用者信頼) に、ユーザーのグループ メンバーシップ データに基づく条件付きアクセス制御を実装する単純なシナリオを考えてみます。 つまり、設定できます発行承認規則をフェデレーション サーバーで、AD で、特定のグループに属するユーザーを許可するドメイン AD FS によって保護されている特定のアプリケーションへのアクセスします。  ステップ バイ ステップの手順 (UI と Windows PowerShell を使用して) このシナリオを実装するのには、「[チュートリアル ガイド: 条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)します。 このチュートリアルの手順を完了するためには必要があります、ラボ環境を設定し、手順に従います[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)します。

### <a name="advanced-scenarios"></a>高度なシナリオ
Windows Server 2012 R2 で AD FS での条件付きアクセス制御を実装するには、その他の例を以下に示します。

-   このユーザーの ID が MFA で検証された場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可します。

    次のコードを使用することができます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   ユーザーに登録されている職場に参加しているデバイスからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可します。

    次のコードを使用することができます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Id が MFA で検証済みのユーザーに登録されている職場に参加しているデバイスからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可します。

    次のコードを使用することができます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Id が MFA で検証済みのユーザーからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのエクストラネット アクセスを許可します。

    次のコードを使用することができます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>参照してください。
[チュートリアル ガイド: 条件付きアクセス制御によるリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)<ph x="2">
</ph>[Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)



