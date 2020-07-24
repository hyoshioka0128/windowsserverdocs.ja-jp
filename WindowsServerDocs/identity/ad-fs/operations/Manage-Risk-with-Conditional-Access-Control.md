---
ms.assetid: a0f7bb11-47a5-47ff-a70c-9e6353382b39
title: 条件付きアクセス制御によってリスクを管理する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b72f324d7037df30a9a8b1f0b9a966a633d30950
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966494"
---
# <a name="manage-risk-with-conditional-access-control"></a>条件付きアクセス制御によってリスクを管理する




-   [主要な概念-AD FS での条件付きアクセス制御](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_1)

-   [条件付きアクセス制御でのリスクの管理](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md#BKMK_2)

## <a name="key-concepts---conditional-access-control-in-ad-fs"></a><a name="BKMK_1"></a>主要な概念 - AD FS での条件付きアクセス制御
AD FS の全体的な機能は、クレームのセットを含むアクセストークンを発行することです。 AD FS が許可して、発行は、どのようなクレームに関する決定は、要求規則が適用されます。

AD FS のアクセス制御は、発行承認要求規則を使用して実装されます。この規則は、ユーザーまたはユーザーグループが AD FS セキュリティで保護されたリソースにアクセスできるかどうかを決定する許可要求または拒否要求を発行するために使用されます。 承認規則は証明書利用者信頼を基づいてのみ設定できます。

|規則のオプション|規則のロジック|
|---------------|--------------|
|すべてのユーザーを許可|入力方向の要求の種類が *[すべての要求の種類]* に等しく、値が *[すべての値]* に等しい場合、値が *[許可]* に等しい要求が発行されます。|
|この入力方向の要求を行ったユーザーのアクセスを許可|入力方向の要求の種類が *[指定された要求の種類]* に等しく、値が *[指定された要求の値]* に等しい場合は、値が *[許可]* に等しい要求が発行されます。|
|この入力方向の要求を行ったユーザーのアクセスを拒否|入力方向の要求の種類が *[指定された要求の種類]* に等しく、値が *[指定された要求の値]* に等しい場合は、値が *[拒否]* に等しい要求が発行されます。|

これらの規則のオプションとロジックの詳細については、「[承認要求規則を使用する場合](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ee913560(v=ws.11))」を参照してください。

Windows Server 2012 R2 の AD FS では、アクセス制御は、ユーザー、デバイス、場所、認証データを含む複数の要因によって強化されています。 このアクセス制御の拡張は、承認要求規則で利用できるさまざまな種類の要求によって実現されます。  言い換えると、Windows Server 2012 R2 の AD FS では、ユーザー id またはグループメンバーシップ、ネットワークの場所、デバイス (社内参加しているかどうかにかかわらず) に基づいて条件付きアクセス制御を適用することができます。詳細については、「[任意のデバイスからの職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

Windows Server 2012 R2 の AD FS での条件付きアクセス制御には、次のような利点があります。

-   アプリケーションごとにさまざまに設定できる柔軟な認証ポリシー。ユーザー、デバイス、ネットワーク上の位置情報、認証状態に基づいてアクセスを許可または拒否できます。

-   証明書利用者アプリケーションに関する発行承認規則の作成。

-   一般的な条件付きアクセス制御シナリオに対応する充実した UI エクスペリエンス。

-   高度な条件付きアクセス制御シナリオに対応する豊富な要求の定義と Windows PowerShell のサポート。

-   カスタム (証明書利用者アプリケーションごと) の "アクセスが拒否されました" メッセージ。 詳細については、「[AD FS サインイン ページのカスタマイズ](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11))」を参照してください。 これらのメッセージをカスタマイズできることで、ユーザーがアクセスを拒否されている理由を説明し、可能であればセルフサービスで修復するように促すことができます。たとえば、ユーザーに職場へのデバイスの参加を促すことができます。 詳細については、「 [Join to Workplace from Any Device for SSO and Seamless Second Factor Authentication Across Company Applications](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。

次の表には、条件付きアクセス制御を実装するために使用される Windows Server 2012 R2 の AD FS で使用できるすべての要求の種類が含まれています。

|要求の種類|説明|
|--------------|---------------|
|電子メール アドレス|ユーザーのメール アドレス。|
|名|ユーザーの姓名の名。|
|名前|ユーザーの一意の名前。|
|UPN|ユーザーのユーザー プリンシパル名 (UPN)。|
|共通名|ユーザーの一般名。|
|AD FS 1 x 電子メール アドレス|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの電子メール アドレス。|
|グループ|ユーザーが属するグループ。|
|AD FS 1 x UPN|AD FS 1.1 または AD FS 1.0 と相互運用するときのユーザーの UPN。|
|Role|ユーザーの役割。|
|Surname|ユーザーの姓名の姓。|
|PPID|ユーザーの個人識別子。|
|名前 ID|ユーザーの SAML 名前識別子。|
|認証タイム スタンプ|ユーザーが認証された時刻と日付を表示するために使用されます。|
|認証方法|ユーザーの認証に使用される方法。|
|拒否専用グループ SID|ユーザーの拒否専用グループ SID。|
|拒否専用プライマリ SID|ユーザーの拒否専用プライマリ SID。|
|拒否専用プライマリ グループ SID|ユーザーの拒否専用プライマリ グループ SID。|
|グループ SID|ユーザーのグループ SID。|
|プライマリ グループ SID|ユーザーのプライマリ グループ SID。|
|プライマリ SID|ユーザーのプライマリ SID。|
|Windows アカウント名|ユーザーの domain\user 形式のドメイン アカウント名。|
|登録済みユーザー|ユーザーはこのデバイスを使用するように登録されています。|
|デバイス識別子|デバイスの識別子。|
|デバイス登録識別子|デバイス登録の識別子。|
|デバイス登録表示名|デバイス登録の表示名。|
|デバイス OS の種類|デバイスのオペレーティング システムの種類。|
|Device OS Version|デバイスのオペレーティング システムのバージョン。|
|マネージド デバイス|デバイスは管理サービスによって管理されています。|
|転送済みクライアント IP アドレス|ユーザーの IP アドレス。|
|クライアント アプリケーション|クライアント アプリケーションの種類。|
|クライアント ユーザー エージェント|クライアントがアプリケーションへのアクセスに使用しているデバイスの種類。|
|クライアント IP|クライアントの IP アドレス。|
|エンドポイント パス|クライアントがアクティブかパッシブかの決定に使用できるエンドポイントの絶対パス。|
|プロキシ|要求が渡されるフェデレーション サーバー プロキシの DNS 名。|
|アプリケーション識別子|証明書利用者の識別子。|
|アプリケーション ポリシー|証明書のアプリケーション ポリシー。|
|機関キー識別子|発行された証明書への署名に使用した証明書の機関キー識別子 (拡張子)。|
|基本制限|証明書のいずれかの基本制限。|
|拡張キー使用法|証明書のいずれかの拡張キー使用法。|
|発行者|X.509 証明書を発行した証明機関の名前。|
|発行者名|証明書の発行者の識別名。|
|キー使用法|証明書のいずれかのキー使用法。|
|有効期間の終了時刻|証明書が無効になるローカル時間での日付。|
|期間の開始時刻|証明書が有効になるローカル時間での日付。|
|証明書ポリシー|証明書が発行されている場合に従うポリシー。|
|公開キー|証明書の公開キー。|
|証明書の未処理データ|証明書の未処理データ。|
|サブジェクト代替名|証明書のいずれかの代替名。|
|シリアル番号|証明書のシリアル番号。|
|署名アルゴリズム|証明書の署名の作成に使用されるアルゴリズム。|
|サブジェクト|証明書のサブジェクト。|
|サブジェクト キー識別子|証明書のサブジェクト キー識別子。|
|サブジェクト名|証明書のサブジェクトの識別名。|
|V2 テンプレート名|証明書の発行または更新時に使用されるバージョン 2 証明書テンプレートの名前。 これは Microsoft 固有の値です。|
|V1 テンプレート名|証明書の発行または更新時に使用されるバージョン 1 証明書テンプレートの名前。 これは Microsoft 固有の値です。|
|Thumbprint|証明書の拇印。|
|X 509 バージョン|証明書の X.509 形式のバージョン。|
|企業ネットワーク内|要求が企業ネットワーク内から送られたかどうかを示すために使用されます。|
|パスワードの有効期限|パスワードの有効期限が切れる日時を表示するために使用されます。|
|パスワードの有効日数|パスワードの有効期限が切れるまでの日数を表示するために使用されます。|
|パスワード更新 URL|パスワード更新サービスの Web アドレスを表示するために使用されます。|
|認証方法の参照|ユーザーを認証するために使用される認証方法を示すために使用されます。|

## <a name="managing-risk-with-conditional-access-control"></a><a name="BKMK_2"></a>条件付きアクセス制御でのリスクの管理
条件付きアクセス制御を実装し、利用可能な設定を使用することで、多くの方法でリスクを管理できます。

### <a name="common-scenarios"></a>一般的なシナリオ
たとえば、特定のアプリケーション (証明書利用者信頼) のユーザーのグループメンバーシップデータに基づいて、条件付きアクセス制御を実装する簡単なシナリオを考えてみます。 つまり、フェデレーションサーバーで発行承認規則を設定して、AD ドメイン内の特定のグループに属するユーザーに、AD FS によって保護されている特定のアプリケーションへのアクセスを許可することができます。  このシナリオを実装する詳細な手順 (UI と Windows PowerShell を使用) については、「 [Walkthrough Guide: Manage Risk with Conditional Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)」で説明しています。 このチュートリアルの手順を完了するには、ラボ環境を設定し、「 [Windows Server 2012 R2 の AD FS 用のラボ環境](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)をセットアップする」の手順に従ってください。

### <a name="advanced-scenarios"></a>高度なシナリオ
Windows Server 2012 R2 の AD FS での条件付きアクセス制御を実装するその他の例を次に示します。

-   このユーザーの id が MFA で検証された場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可する

    次のコードを使用できます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessWithMFA"
    c:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   ユーザーに登録されている社内参加デバイスからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可する

    次のコードを使用できます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "PermitAccessFromRegisteredWorkplaceJoinedDevice"
    c:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Id が MFA で検証済みのユーザーに登録されている職場参加済みのデバイスからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのアクセスを許可する

    次のコードを使用できます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAOnRegisteredWorkplaceJoinedDevice"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser", Value =~ "^(?i)true$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

-   Id が MFA で検証済みのユーザーからアクセス要求が送られている場合にのみ、AD FS によって保護されたアプリケーションへのエクストラネットアクセスを許可します。

    次のコードを使用できます。

    ```
    @RuleTemplate = "Authorization"
    @RuleName = "RequireMFAForExtranetAccess"
    c1:[Type == "https://schemas.microsoft.com/claims/authnmethodsreferences", Value =~ "^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$"] &&
    c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value =~ "^(?i)false$"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "PermitUsersWithClaim");

    ```

## <a name="see-also"></a>参照
[チュートリアルガイド: 条件付き Access Control](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md) 
 によるリスク管理[Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
