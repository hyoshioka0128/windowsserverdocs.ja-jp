---
ms.assetid: ''
title: Active Directory フェデレーション サービス 2.0 内のクライアント アクセス制御ポリシー
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 216af933aee643ee56feff71c59d9ecc2e62998c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842993"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>AD FS 2.0 でのクライアント アクセス制御ポリシー
Active Directory フェデレーション サービス 2.0 内のクライアント アクセス ポリシーを使用すると、リソースへのアクセスをユーザーに許可または制限できます。  このドキュメントでは、AD FS 2.0 でのクライアント アクセス ポリシーを有効にする方法と、最も一般的なシナリオを構成する方法について説明します。

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>AD FS 2.0 でのクライアント アクセス ポリシーを有効にします。

クライアント アクセス ポリシーを有効にするには、次の手順に従います。

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>手順 1:AD FS 2.0 の更新プログラムのロールアップ 2 は、AD FS サーバーでパッケージのインストール

ダウンロード、 [Active Directory フェデレーション サービス (AD FS) の更新プログラムのロールアップ 2 2.0](https://support.microsoft.com/en-us/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0)パッケージ化し、すべてのフェデレーション サーバーとフェデレーション サーバー プロキシにインストールします。

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>手順 2:5 つの要求規則を Active Directory 要求プロバイダー信頼の追加します。

AD FS サーバーとプロキシのすべての更新プログラム ロールアップ 2 をインストールすると、新しいクレームの種類をポリシー エンジンを使用できるようにする一連の要求規則を追加するのに、次の手順を使用します。

これを行うには、追加する 5 つの受付変換規則の次の手順を使用して新しい要求コンテキストの要求種類ごと。

Active Directory の要求プロバイダー信頼では、新しい要求コンテキスト クレームの種類の各を通過する新しい受け入れ変換規則を作成します。

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>Active Directory に要求規則を追加するには、5 つのコンテキストの各要求プロバイダー信頼要求の種類。


1. 開始 をクリックしてのプログラム、管理ツール をポイントし、および広告をクリックし、FS 2.0 管理します。
2. AD FS 2.0 \trust Relationships、下のコンソール ツリーでは、要求プロバイダー信頼 をクリックして、Active Directory を右クリックし、要求規則の編集 をクリックします。
3. 要求規則の編集 ダイアログ ボックスで、受け入れ変換規則 タブを選択し、し、規則のウィザードを開始するには、規則の追加 をクリックします。
4. 規則テンプレートの選択] ページで、[要求規則テンプレートでは、パススルーを選択または一覧から、入力方向の要求をフィルター処理し、し、[次へ] をクリックします。
5. 規則の構成 ページで、要求規則名の下には、この規則の表示名を入力します。受信要求の種類を選択し、次の要求の種類の URL を入力し、すべての要求値をパスを選択します。</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. ルールを確認するには、一覧から選択しますルールの編集 をクリックし、規則言語をクリックします。 要求規則言語としては、次のように表示されます。 `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. [完了] をクリックします。
8. 要求規則の編集 ダイアログ ボックスで、ルールを保存するには、ok をクリックします。
9. 手順 2 の 5 つすべての規則が作成されるまでに、次に示す残りの 4 つの要求の種類ごとに、追加の要求規則を作成する.

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>手順 3:パーティの信頼証明書利用者 Microsoft Office 365 Id プラットフォームの更新します。

組織のニーズに最も適合する信頼証明書利用者 Microsoft Office 365 Id プラットフォームに要求規則を構成するのには、次のシナリオ例のいずれかを選択します。

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>AD FS 2.0 のクライアント アクセス ポリシーのシナリオ
次のセクションでは、AD FS 2.0 に存在するシナリオをについて説明します

### <a name="scenario-1-block-all-external-access-to-office-365"></a>シナリオ 1:Office 365 へのすべての外部アクセスをブロックします。

このクライアント アクセス ポリシーのシナリオでは、外部のクライアントの IP アドレスに基づくすべての外部クライアントからすべての内部クライアントおよびブロックへのアクセスを許可します。 規則セットは、既定の発行承認規則のすべてのユーザーへのアクセスの許可に基づいています。 次の手順を使用するには、Office 365 の信頼証明書利用者に発行承認規則を追加します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックするルールを作成するには



1. 開始 をクリックしてのプログラム、管理ツール をポイントし、および広告をクリックし、FS 2.0 管理します。
2. AD FS 2.0 \trust Relationships、下のコンソール ツリーで証明書利用者信頼 をクリックして、Microsoft Office 365 Id プラットフォームの信頼を右クリックし、要求規則の編集 をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、[要求規則テンプレートでは、カスタム ルールを送信要求を使用してを選択し、[次へ] をクリックします。
5. 規則の構成 ページで、要求規則名の下には、このルールの表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. [完了] をクリックします。 以下の発行承認規則の一覧のすべてのユーザーの規則へのアクセスを許可する新しい規則がすぐに表示されますを確認します。
7. 要求規則の編集 ダイアログ ボックスで、ルールを保存するには、ok をクリックします。

>[!NOTE]
>「パブリック ip アドレスの正規表現」は、上記の値を有効な IP の式に置き換える必要があります。詳細については、IP アドレスの範囲式の構築に参照してください。


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>例 2:Exchange ActiveSync を除く Office 365 へのすべての外部アクセスをブロックします。

次の例では、Outlook を含む内部のクライアントから Exchange Online を含むすべての Office 365 アプリケーションへのアクセスを許可します。 Exchange ActiveSync クライアントのスマート フォンなどを除き、クライアントの IP アドレスで示されている、企業ネットワークの外部に存在するクライアントからのアクセスをブロックします。 規則セットは、すべてのユーザーにアクセスを許可という既定の発行承認規則に基づいています。 要求規則のウィザードを使用して信頼証明書利用者、Office 365 に発行承認規則を追加するのにには、次の手順を使用します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 へのすべての外部アクセスをブロックするルールを作成するには



1. 開始 をクリックしてのプログラム、管理ツール をポイントし、および広告をクリックし、FS 2.0 管理します。
2. AD FS 2.0 \trust Relationships、下のコンソール ツリーで証明書利用者信頼 をクリックして、Microsoft Office 365 Id プラットフォームの信頼を右クリックし、要求規則の編集 をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、[要求規則テンプレートでは、カスタム ルールを送信要求を使用してを選択し、[次へ] をクリックします。
5. 規則の構成 ページで、要求規則名の下には、このルールの表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 以下の発行承認規則の一覧のすべてのユーザーの規則へのアクセスを許可する新しい規則がすぐに表示されますを確認します。
7. 要求規則の編集 ダイアログ ボックスで、ルールを保存するには、ok をクリックします。

>[!NOTE]
>「パブリック ip アドレスの正規表現」は、上記の値を有効な IP の式に置き換える必要があります。詳細については、IP アドレスの範囲式の構築に参照してください。

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>例 3:ブラウザー ベースのアプリケーションを除く Office 365 に対するすべての外部アクセスをブロックします。

規則セットは、すべてのユーザーにアクセスを許可という既定の発行承認規則に基づいています。 要求規則のウィザードを使用して信頼証明書利用者 Microsoft Office 365 Id プラットフォームに発行承認規則を追加するのにには、次の手順を使用します。

>[!NOTE]
>パッシブ (Web ベースの) 要求でクライアント アクセス ポリシーのヘッダーに関する制限事項のため、サード パーティ製プロキシを使用した、このシナリオがサポートされていません。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>ブラウザー ベースのアプリケーションを除く Office 365 に対するすべての外部アクセスをブロックするルールを作成するには



1. 開始 をクリックしてのプログラム、管理ツール をポイントし、および広告をクリックし、FS 2.0 管理します。
2. AD FS 2.0 \trust Relationships、下のコンソール ツリーで証明書利用者信頼 をクリックして、Microsoft Office 365 Id プラットフォームの信頼を右クリックし、要求規則の編集 をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、[要求規則テンプレートでは、カスタム ルールを送信要求を使用してを選択し、[次へ] をクリックします。
5. 規則の構成 ページで、要求規則名の下には、このルールの表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 以下の発行承認規則の一覧のすべてのユーザーの規則へのアクセスを許可する新しい規則がすぐに表示されますを確認します。
7. 要求規則の編集 ダイアログ ボックスで、ルールを保存するには、ok をクリックします。

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>シナリオ 4:指定された Active Directory グループの Office 365 に対するすべての外部アクセスをブロックします。

次の例では、IP アドレスに基づく内部のクライアントからアクセスできるようにします。 企業ネットワークの外部に存在する外部のクライアント IP アドレスを持つクライアントからのアクセスがブロックにアクセスを許可という既定の発行承認規則のセットを構築、指定した Active Directory グループの規則で人を除くすべてのユーザー。 要求規則のウィザードを使用して信頼証明書利用者 Microsoft Office 365 Id プラットフォームに発行承認規則を追加するのにには、次の手順を使用します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>指定された Active Directory グループの Office 365 に対するすべての外部アクセスをブロックするルールを作成するには



1. 開始 をクリックしてのプログラム、管理ツール をポイントし、および広告をクリックし、FS 2.0 管理します。
2. AD FS 2.0 \trust Relationships、下のコンソール ツリーで証明書利用者信頼 をクリックして、Microsoft Office 365 Id プラットフォームの信頼を右クリックし、要求規則の編集 をクリックします。 
3. 要求規則の編集] ダイアログ ボックスで、[発行承認規則] タブを選択し、し、[要求規則のウィザードを開始するには、[規則の追加] をクリックします。
4. 規則テンプレートの選択] ページで、[要求規則テンプレートでは、カスタム ルールを送信要求を使用してを選択し、[次へ] をクリックします。
5. 規則の構成 ページで、要求規則名の下には、このルールの表示名を入力します。 カスタム規則を入力するか、次の要求規則言語構文貼り付けます。 `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 以下の発行承認規則の一覧のすべてのユーザーの規則へのアクセスを許可する新しい規則がすぐに表示されますを確認します。
7. 要求規則の編集 ダイアログ ボックスで、ルールを保存するには、ok をクリックします。


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>上記のシナリオで使用する要求規則言語構文の説明

|説明|要求規則言語の構文|
|-----|-----| 
|すべてのユーザーにアクセスを許可する既定の AD FS 規則。 このルールは、発行承認規則のリストの信頼証明書利用者 Microsoft Office 365 Id プラットフォームに既に存在する必要があります。|=> issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");| 
|新しいカスタム ルールにこの句を追加するには、要求がフェデレーション サーバー プロキシから取得することを指定します (x-ms-プロキシ ヘッダーを持つなど)
この属性のすべてのルールを含めることをお勧めします。|exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"])| 
|Ip アドレスに定義された許容範囲を使用するクライアントから要求がであるを確立するために使用されます。|NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value=~"customer-provided public ip address regex"])| 
|この句は、アクセスされるアプリケーションは、Microsoft.Exchange.ActiveSync ではない場合、要求拒否することを指定に使用されます。|存在しない ([型 = ="https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"、Value=="Microsoft.Exchange.ActiveSync"])| 
|このルールでは、呼び出しは、Web ブラウザーを使用し、拒否されていないかどうかを判断できます。|NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])| 
|このルールは、唯一のユーザー (SID 値に基づいて) 特定の Active Directory グループを拒否することを示しています。 このステートメントにない追加場所に関係なく、ユーザーのグループが許可されますを意味します。|存在する ([型 = ="https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid"、値 = ~"{グループ許可されている AD グループの SID 値}"])| 
|これは、上記のすべての条件が満たされたときに、拒否を発行するために必要な句です。|=> issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");|

### <a name="building-the-ip-address-range-expression"></a>IP アドレス範囲の式の構築

X-ms-転送-クライアントの ip の要求は、AD FS を認証要求を渡すときに、ヘッダーを設定する Exchange Online でのみ設定されている HTTP ヘッダーから設定されます。 要求の値は、次のいずれかにあります。

>[!Note] 
>Exchange Online の場合、現在、IPV4 と IPV6 はリッスンしませんアドレスのみをサポートします。

1 つの IP アドレス:Exchange Online に直接接続されているクライアントの IP アドレス

>[!Note] 
>企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイスの IP アドレスとして表示されます。

企業内部のクライアント、または VPN または DA の構成によっては外部のクライアントとして Microsoft DirectAccess (DA) によって、または VPN で企業ネットワークに接続されているクライアントが表示されます。

1 つまたは複数の IP アドレス:接続するクライアントの IP アドレスは、Exchange Online の場合に特定することはできません、x のヘッダー、HTTP ベースの要求に含めることがあり、多くのクライアントでは、ロード バランサーでサポートされている非標準ヘッダーの値に基づいて値が設定されます。市場でのプロキシ。

>[!Note]
>クライアントの IP アドレスと、要求が渡される各プロキシのアドレスを示す、複数の IP アドレスはコンマで区切られます。

Exchange Online のインフラストラクチャに関連する IP アドレスは、一覧には表示されません。


#### <a name="regular-expressions"></a>正規表現

範囲の IP アドレスと一致するときに、比較を実行する正規表現を構築するために必要になります。 次の一連の手順では、次のアドレス範囲 (注、パブリック IP の範囲に一致するようにこれらの例を変更する必要があります) に一致するようにこのような式を作成する方法の例は、指定します。


- 192.168.1.1 – 192.168.1.25
- 10.0.0.1 – 10.0.0.14

単一の IP アドレスに一致する基本的なパターンが最初に、次に示します: \b###\.###\.###\.### \b

これを拡張するには、照合できる 2 つの異なる IP アドレス、OR 式を次のように: \b###\.###\.###\.### \b|\b###\. ### \. ### \.### \b

そのため、2 つのアドレス (192.168.1.1 10.0.0.1 など) に一致するように例があります: \b192\.168\.1\.1\b | \b10\.0\.0\.1\b

これにより、手法を任意の数のアドレスを入力することができます。 アドレスの範囲は、たとえば 192.168.1.1 – 192.168.1.25 を許可する必要がありますが、一致する必要があります文字が文字: \b192\.168\.1\.([1-9] | [0-9] 1 | 2 [0-5]) \b

>[!Note] 
>IP アドレスは、文字列と数ではなくとして扱われます。


このルールは次のように分割されます \b192\.168\.1\.

これには、192. 168.1 始まる任意の値と一致します。

範囲の最後の小数点より後に必要なアドレスの一部を次に一致します。


- ([1-9] と一致するアドレス 1-9 で終わる
- | 1 [0-9] 10 ~ 19 のアドレスと一致します。
- 20 ~ 25 で終わる |2[0-5]) と一致するアドレス

>[!Note]
>かっこは、する必要がありますが正しく配置されている、IP アドレスの他の部分を照合を開始しないようにします。

192 のブロックを照合して、10 個のブロックのような式を記述できます \b10\.0\.0\.([1-9] | [0-4] の 1) \b。

まとめて配置するには、次の式は「192.168.1.1~25」と「10.0.0.1~14」のすべてのアドレスを一致する必要があります: \b192\.168\.1\.([1-9] | [0-9] 1 | 2 [0-5]) \b|\b10\.0\.0\.([1-9] | [0-4] の 1) \b

#### <a name="testing-the-expression"></a>式のテスト

正規表現の式はなる正規表現検証ツールの使用を強くお勧めので非常に複雑です。 「オンライン regex 式ビルダー」のインターネット検索を実行する場合は、サンプル データに対して、式を試用するために、いくつかの優れたオンライン ユーティリティが表示されます。

式をテストするときに、一致する必要がありますの注意点を理解する必要が。 Exchange online のシステムでは、コンマで区切られた多くの IP アドレスを送信できます。 上記の式は、この機能します。 ただし、これが、正規表現の式をテストするときに、これについて考える重要です。 たとえば、上記の例を確認する入力次のサンプルを使用していずれかの可能性があります。 

192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20 

10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1 











## <a name="validating-the-deployment"></a>展開の検証

### <a name="security-audit-logs"></a>セキュリティ監査ログ

要求が送信されると、AD FS を使用できるは、新しい要求コンテキスト要求処理パイプラインのことを確認するには、AD FS サーバーでの監査ログを有効にします。 標準的なセキュリティ監査ログ エントリでいくつかの認証要求と要求値の確認を送信します。 

AD FS サーバーのログ、セキュリティにイベントを監査のログ記録を有効にするには、AD FS 2.0 の監査の構成の手順に従います。

### <a name="event-logging"></a>イベントのログ記録

既定では、失敗した要求がアプリケーションとサービス ログの下にあるアプリケーション イベント ログに記録されます \ AD FS 2.0 \ Admin.For の詳細については、AD FS のイベント ログを参照してください[を設定する AD FS 2.0 のイベントのログ記録](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)します。

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>トレース ログの詳細な AD FS を構成

AD FS トレース イベントは、AD FS 2.0 のデバッグ ログに記録されます。 トレースを有効にするのを参照してください。 [AD FS 2.0 のデバッグ トレースの構成](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)します。

トレースを有効にした後は、次のコマンドライン構文を使用して、詳細ログ記録レベルを有効にする: wevtutil.exe sl"AD FS 2.0 のトレース/デバッグ"/l:5  

## <a name="related"></a>関連
新しいクレームの種類の詳細については、次を参照してください。 [AD FS のクレームの種類](AD-FS-Claims-Types.md)します。
 
