---
ms.assetid: 
title: "Active Directory フェデレーション サービス 2.0 内のクライアント アクセス制御ポリシー"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 00b9cd17c7a5c206e06bea12fd90762adb336715
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>AD FS 2.0 でのクライアント アクセス制御ポリシー
Active Directory フェデレーション サービス 2.0 内のクライアント アクセス ポリシーを使用すると、ユーザー リソースへのアクセスを許可または制限できます。  このドキュメントでは、AD FS 2.0 でのクライアント アクセス ポリシーを有効にする方法と、最も一般的なシナリオを構成する方法について説明します。

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>AD FS 2.0 でクライアントのアクセス ポリシーを有効にします。

クライアントのアクセス ポリシーを有効にするには、次の手順に従います。

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>手順 1: AD FS サーバーのインストール AD FS 2.0 の更新プログラムのロールアップ 2 パッケージします。

ダウンロード、 [Active Directory フェデレーション サービス (AD FS) の更新プログラムのロールアップ 2 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0)パッケージ化し、すべてのフェデレーション サーバーとフェデレーション サーバー プロキシにインストールします。

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>手順 2: 5 つの要求規則を Active Directory 要求プロバイダー信頼を追加します。

AD FS サーバーとプロキシのすべての更新プログラム ロールアップ 2 をインストールすると、新しい要求の種類をポリシー エンジンを使用できるようにする要求規則のセットを追加するのに、次の手順を使用します。

これを行うには、追加する 5 つの受付変換規則の新しい要求コンテキスト要求の種類、次の手順を使用して各します。

Active Directory の要求プロバイダー信頼では、新しい要求コンテキスト要求の種類の各を通過する新しい受け付け変換規則を作成します。

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Active Directory に要求規則を追加するには、5 つのコンテキストの各要求プロバイダー信頼要求の種類。


1. [スタート] ボタン、プログラム] をポイントし、管理ツール] をポイントし、AD FS 2.0 管理します。
2. コンソール ツリーで、[AD FS 2.0\Trust 関係、要求プロバイダー信頼] をクリックして、Active Directory を右クリックし、[要求規則の編集] をクリックします。
3. 要求規則の編集] ダイアログ ボックスで、受け付け変換規則] タブを選択し、[規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、要求規則テンプレートでは、[パススルー] を選択またはリストから、入力方向の要求をフィルター処理し、[次へ] をクリックします。
5. 規則の構成] ページで、要求規則名、[この規則の表示名を入力します入力方向要求の種類、および次の要求の種類の URL を入力し、すべての要求値をパスを選択します。</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. ルールを確認するため、一覧から選択規則の編集] をクリックし、[規則言語の表示] をクリックします。 要求規則言語は次のように表示されます。 `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. [完了] をクリックします。
8. 要求規則の編集] ダイアログ ボックスで、規則を保存するには、[ok] をクリックします。
9. 手順 2 の 5 つすべての規則が作成されるまで、以下に示す残りの 4 つの要求の種類ごとに、その他の要求規則を作成する.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>手順 3: 証明書利用者の信頼 Microsoft Office 365 の Id プラットフォームの更新します。

証明書利用者の信頼、組織のニーズに最も合致 Microsoft Office 365 の Id プラットフォームで要求規則を構成するのには、次のシナリオ例のいずれかを選択します。

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>AD FS 2.0 のクライアント アクセス ポリシーのシナリオ
次のセクションでは、AD FS 2.0 に存在しているシナリオを示します

### <a name="scenario-1-block-all-external-access-to-office-365"></a>シナリオ 1: Office 365 へのすべての外部アクセスをブロックします。

このクライアントのアクセス ポリシーのシナリオでは、外部クライアントの IP アドレスに基づくすべての外部のクライアントすべての内部クライアントおよびブロックからのアクセスを許可します。 規則セットは、既定の発行承認規則のすべてのユーザーにアクセス許可に基づいています。 証明書利用者の信頼、Office 365 に発行承認規則を追加するのに、次の手順を使用することができます。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックする規則を作成するには



1. [スタート] ボタン、プログラム] をポイントし、管理ツール] をポイントし、AD FS 2.0 管理します。
2. コンソール ツリーで、[AD FS 2.0\Trust 関係、証明書利用者信頼をクリックして、Microsoft Office 365 の Id プラットフォームの信頼を右クリックし、[要求規則の編集] をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、要求規則テンプレートでは、[カスタム規則を信頼性情報を使用して送信を選択し、[次へ] をクリックします。
5. [規則の構成] ページで、要求規則名、[この規則の表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文を貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. [完了] をクリックします。 新しい規則が表示されているすぐ下発行承認規則のリスト内のすべてのユーザーのルールにアクセス許可を確認します。
7. 要求規則の編集] ダイアログ ボックスで、規則を保存するには、[ok] をクリックします。

>[!NOTE]
>有効な IP の式で上「のパブリック ip アドレスの正規表現」の値を置き換えるには詳細については IP アドレス範囲の式の作成を参照してください。


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>シナリオ 2: Exchange ActiveSync を除く、Office 365 へのすべての外部アクセスをブロックします。

次の例では、Outlook などの内部クライアントから、Exchange Online を含め、すべての Office 365 アプリケーションにアクセスできるようにします。 スマート フォンなどの Exchange ActiveSync クライアントを除き、クライアントの IP アドレスによって示されている、企業のネットワークの外部に存在するクライアントからのアクセスをブロックします。 規則セットは、タイトルのすべてのユーザーへのアクセスを許可する既定の発行承認規則に基づいています。 証明書利用者の信頼、要求規則のウィザードを使用して、Office 365 に発行承認規則を追加するのにには、次の手順を使用します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックする規則を作成するには



1. [スタート] ボタン、プログラム] をポイントし、管理ツール] をポイントし、AD FS 2.0 管理します。
2. コンソール ツリーで、[AD FS 2.0\Trust 関係、証明書利用者信頼をクリックして、Microsoft Office 365 の Id プラットフォームの信頼を右クリックし、[要求規則の編集] をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、要求規則テンプレートでは、[カスタム規則を信頼性情報を使用して送信を選択し、[次へ] をクリックします。
5. [規則の構成] ページで、要求規則名、[この規則の表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文を貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 新しい規則が表示されているすぐ下発行承認規則のリスト内のすべてのユーザーのルールにアクセス許可を確認します。
7. 要求規則の編集] ダイアログ ボックスで、規則を保存するには、[ok] をクリックします。

>[!NOTE]
>有効な IP の式で上「のパブリック ip アドレスの正規表現」の値を置き換えるには詳細については IP アドレス範囲の式の作成を参照してください。

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>シナリオ 3: Office 365 にブラウザー ベースのアプリケーションを除くのすべての外部アクセス権をブロックします。

規則セットは、タイトルのすべてのユーザーへのアクセスを許可する既定の発行承認規則に基づいています。 証明書利用者の信頼、要求規則のウィザードを使用して Microsoft Office 365 の Id プラットフォームに発行承認規則を追加するのにには、次の手順を使用します。

>[!NOTE]
>クライアント アクセス ポリシー ヘッダーとパッシブ (Web ベースの) 要求の制限のため、サード パーティ製プロキシと、このシナリオがサポートされていません。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>Office 365 にブラウザー ベースのアプリケーションを除くのすべての外部アクセス権をブロックする規則を作成するには



1. [スタート] ボタン、プログラム] をポイントし、管理ツール] をポイントし、AD FS 2.0 管理します。
2. コンソール ツリーで、[AD FS 2.0\Trust 関係、証明書利用者信頼をクリックして、Microsoft Office 365 の Id プラットフォームの信頼を右クリックし、[要求規則の編集] をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、要求規則テンプレートでは、[カスタム規則を信頼性情報を使用して送信を選択し、[次へ] をクリックします。
5. [規則の構成] ページで、要求規則名、[この規則の表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文を貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 新しい規則が表示されているすぐ下発行承認規則のリスト内のすべてのユーザーのルールにアクセス許可を確認します。
7. 要求規則の編集] ダイアログ ボックスで、規則を保存するには、[ok] をクリックします。

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>シナリオ 4: 指定された Active Directory グループの Office 365 にすべての外部アクセスをブロックします。

次の例では、IP アドレスに基づく内部クライアントからアクセスできるようにします。 外部のクライアント IP アドレスを持っている、企業ネットワークの外部に存在するクライアントからのアクセスがブロック、指定した Active Directory グループ規則でユーザーを除くセットに基づいて、既定の発行承認規則をタイトルのすべてのユーザーへのアクセスを許可します。 証明書利用者の信頼、要求規則のウィザードを使用して Microsoft Office 365 の Id プラットフォームに発行承認規則を追加するのにには、次の手順を使用します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>指定した Active Directory グループの Office 365 にすべての外部アクセスをブロックする規則を作成するには



1. [スタート] ボタン、プログラム] をポイントし、管理ツール] をポイントし、AD FS 2.0 管理します。
2. コンソール ツリーで、[AD FS 2.0\Trust 関係、証明書利用者信頼をクリックして、Microsoft Office 365 の Id プラットフォームの信頼を右クリックし、[要求規則の編集] をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、要求規則テンプレートでは、[カスタム規則を信頼性情報を使用して送信を選択し、[次へ] をクリックします。
5. [規則の構成] ページで、要求規則名、[この規則の表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文を貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 新しい規則が表示されているすぐ下発行承認規則のリスト内のすべてのユーザーのルールにアクセス許可を確認します。
7. 要求規則の編集] ダイアログ ボックスで、規則を保存するには、[ok] をクリックします。


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>上記のシナリオで使用する要求規則言語構文の説明

|説明|要求規則言語の構文|
|-----|-----| 
|すべてのユーザーへのアクセスを許可する既定の AD FS ルールです。 このルールは、Microsoft Office 365 の Id プラットフォーム証明書利用者の信頼発行承認規則の一覧に既に存在する必要があります。|= > 問題 (種類"https://schemas.microsoft.com/authorization/claims/permit"、値を = ="true")。| 
|新しいカスタム ルールにこの句を追加するには、要求がフェデレーション サーバー プロキシから来ているを指定します (x-ms-プロキシ ヘッダーを持つなど)
すべてのルールがこれを含めることをお勧めします。|存在する ([種類"https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"= =])| 
|定義済みの許容範囲で IP を使用するクライアントから要求されるを確立するために使用されます。|存在しない] ([種類"https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"、値を = = = ~「顧客によって提供されたのパブリック ip アドレスの正規表現」])| 
|この句を使用して、アクセスしているアプリケーションが Microsoft.Exchange.ActiveSync でない場合、要求拒否することを指定します。|存在しない] ([種類"https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"= =、Value=="Microsoft.Exchange.ActiveSync"])| 
|このルールでは、呼び出しは、Web ブラウザーを利用した、拒否されていないかどうかを決定することができます。|存在しない] ([種類"https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path"、値を = = = ="/adfs/ls/"])| 
|このルールは、ユーザー (SID の値に基づく) 特定の Active Directory グループだけが拒否されることを示しています。 この声明にしない追加の場所に関係なく、ユーザーのグループが許可されますを意味します。|存在する ([種類"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid"、値を = = = ~"{グループ許可されている AD グループの SID 値}"])| 
|これは、上記のすべての条件が満たされたときに、拒否を発行するため、必要な句を使用します。|= > 問題 (種類"https://schemas.microsoft.com/authorization/claims/deny"、値を = ="true")。|

### <a name="building-the-ip-address-range-expression"></a>IP アドレスの範囲の式の作成

X-ms-転送-クライアントの ip アドレスの要求は、HTTP ヘッダー、認証要求を AD FS を渡す際に、ヘッダーを設定する Exchange Online、によってのみ現在設定されているから入力されます。 要求の値は、次のいずれかにあります。

>[!Note] 
>Exchange Online の場合、現在、IPV4 と IPV6 ではないアドレスのみをサポートします。

単一の IP アドレス: Exchange Online に直接接続されているクライアントの IP アドレス

>[!Note] 
>企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。

VPN または Microsoft DirectAccess (DA) によって、企業ネットワークに接続されているクライアントが企業内部のクライアント、または VPN または DA の構成によっては外部のクライアントとして表示可能性があります。

1 つまたは複数の IP アドレス: ときに Exchange Online は接続中のクライアントの IP アドレスを調べることはできません、x-転送-のヘッダーの HTTP ベースの要求に含めることがあり、多くのクライアント、ロード バランサー、および市場でのプロキシでサポートされている標準的でないヘッダーの値に基づいた値が設定されます。

>[!Note]
>クライアントの IP アドレスと、要求が渡される各プロキシのアドレスを示す、複数の IP アドレスが、コンマで区切られます。

Exchange Online のインフラストラクチャに関連する IP アドレスは、一覧には表示されません。


#### <a name="regular-expressions"></a>正規表現

範囲の IP アドレスに一致するときに、正規表現の比較を実行するに必要になります。 次の一連の手順では、アドレスの範囲 (パブリック IP の範囲を一致するようにこれらの例を変更する必要があるに注意してください) と一致するような式を作成する方法の例は、指定します。


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

最初に、単一の IP アドレスが一致する基本的なパターンは、次のように: \b###\.###\.###\.###\b

これを拡張するには、マッチさせる 2 つの異なる IP アドレスまたは式を次のように: \b###\.###\.###\.###\b|\b###\.###\.###\.###\b

そのため、2 つのアドレス (192.168.1.1 10.0.0.1 など) に一致する例があります: \b192\.168\.1\.1\b|\b10\.0\.0\.1\b

これにより、手法を任意の数のアドレスを入力することができます。 アドレスの範囲をたとえば 192.168.1.1 – 192.168.1.25 を許可する必要がありますが、一致する行う必要があります文字で文字: \b192\.168\.1\ します。([1-9] | [0-9] 1 | 2 0 ~ 5) \b

>[!Note] 
>IP アドレスは、文字列と番号ではないと見なされます。


このルールは次のように分けられます。 \b192\.168\.1\ します。

これには、任意の値から始まる 192.168.1 と一致します。

次に、最終的な小数点後アドレスの部分に必要な範囲と一致します。


- ([1-9] と一致するアドレス 1-9 で終わる
- | 1 [0-9] 10 ~ 19 で終わるアドレスと一致します。
- 20 ~ 25 で終わる |2[0-5]) と一致するアドレス

>[!Note]
>かっこ必要がありますが正しい位置、IP アドレスの他の部分を照合を開始しないようにします。

マッチング 192 ブロックは、10 個のブロックのような式を記述できます: \b10\.0\.0\ します。([1-9] | [1 0 ~ 4) \b

一緒に配置するには、次の式が一致している「192.168.1.1~25」および「10.0.0.1~14」のすべてのアドレスと: \b192\.168\.1\ します。([1-9]|1[0-9]|2[0-5])\b|\b10\.0\.0\ します。([1-9] | [1 0 ~ 4) \b

#### <a name="testing-the-expression"></a>式のテスト

正規表現の式を強くお勧め regex 検証ツールを使用するように非常に難しい場合になります。 「オンライン regex 式」でインターネットを検索する場合は、サンプル データに対して、式を試すことができるいくつかの優れたオンライン ユーティリティが表示されます。

式をテストする場合に一致する必要があることを期待できることを理解することが重要です。 Exchange のオンライン システムでは、コンマで区切って、多くの IP アドレスを送信できます。 上記の式は、この動作します。 ただし、これが、正規表現をテストするときに、これについて考えること重要です。 たとえば、上記の例を確認する入力次の例を使用していずれかの可能性があります。 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>展開の検証

### <a name="security-audit-logs"></a>セキュリティ監査ログ

信頼性情報が送信していると、AD FS に使用できる新しい要求コンテキスト要求処理パイプラインのことを確認するには、AD FS サーバーでの監査ログを有効にします。 標準的なセキュリティ監査ログ エントリで一部の認証要求と要求値の確認を送信します。 

AD FS サーバーでログのイベントにセキュリティ監査のログを有効にするには、AD FS 2.0 の監査の構成の手順に従います。

### <a name="event-logging"></a>イベント ログ

既定では、失敗した要求はアプリケーションとサービス ログの下にある、アプリケーション イベント ログに記録 \ AD FS 2.0 \ Admin.For の詳細については、AD FS のイベント ログを参照してください[AD セットアップ FS 2.0 のイベント ログ](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)します。

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>詳細な AD FS トレース ログを構成します。

AD FS トレース イベントは、AD FS 2.0 のデバッグ ログに記録されます。 トレースを有効にするのを参照してください。 [AD FS 2.0 のデバッグ トレースを構成する](https://technet.microsoft.com/en-us/library/adfs2-troubleshooting-configuring-computers.aspx)します。

トレースを有効にした後は、次のコマンドライン構文を使用して、詳細ログ記録レベルを有効にする: wevtutil.exe sl"AD FS 2.0 トレース/デバッグ"/l:5  

## <a name="related"></a>関連します。
新しい要求の種類の詳細については、次を参照してください。 [AD FS のクレーム タイプ](AD-FS-Claims-Types.md)します。
 
