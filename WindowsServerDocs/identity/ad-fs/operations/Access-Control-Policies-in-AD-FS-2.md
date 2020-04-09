---
title: Active Directory フェデレーションサービス (AD FS) 2.0 のクライアント Access Control ポリシー
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6ae1f34343e8574ce776fcc5761c078b12bc9977
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814825"
---
# <a name="client-access-control-policies-in-ad-fs-20"></a>AD FS 2.0 のクライアント Access Control ポリシー
Active Directory フェデレーションサービス (AD FS) 2.0 のクライアントアクセスポリシーでは、リソースへのアクセスを制限または許可することができます。  このドキュメントでは、AD FS 2.0 でクライアントアクセスポリシーを有効にする方法と、最も一般的なシナリオを構成する方法について説明します。

## <a name="enabling-client-access-policy-in-ad-fs-20"></a>AD FS 2.0 でクライアントアクセスポリシーを有効にする

クライアントアクセスポリシーを有効にするには、次の手順に従います。

### <a name="step-1-install-the-update-rollup-2-for-ad-fs-20-package-on-your-ad-fs-servers"></a>手順 1: AD FS サーバーに AD FS 2.0 パッケージの更新プログラムのロールアップ2をインストールする

[Active Directory フェデレーションサービス (AD FS) (AD FS) 2.0 パッケージの更新プログラムのロールアップ 2](https://support.microsoft.com/help/2681584/description-of-update-rollup-2-for-active-directory-federation-services-ad-fs-2.0)をダウンロードし、すべてのフェデレーションサーバーとフェデレーションサーバープロキシにインストールします。

### <a name="step-2-add-five-claim-rules-to-the-active-directory-claims-provider-trust"></a>手順 2: Active Directory 要求プロバイダー信頼に5つの要求規則を追加する

すべての AD FS サーバーとプロキシに更新プログラムのロールアップ2がインストールされたら、次の手順を実行して、新しい要求の種類をポリシーエンジンで使用できるようにする一連の要求規則を追加します。

これを行うには、次の手順に従って、新しい要求コンテキスト要求の種類ごとに5つの受け入れ変換規則を追加します。

Active Directory 要求プロバイダー信頼で、新しい要求コンテキスト要求の種類をパススルーする新しい受け入れ変換規則を作成します。

#### <a name="to-add-a-claim-rule-to-the-active-directory-claims-provider-trust-for-each-of-the-five-context-claim-types"></a>要求規則を、5つのコンテキスト要求の種類それぞれについて、Active Directory 要求プロバイダー信頼に追加するには、次のようにします。


1. [スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントし、[AD FS 2.0 管理] をクリックします。
2. コンソールツリーの [AD FS 2.0 \ 信頼関係] で、[要求プロバイダー信頼] をクリックし、[Active Directory] を右クリックして、[要求規則の編集] をクリックします。
3. [要求規則の編集] ダイアログボックスで、[受け入れ変換規則] タブを選択し、[規則の追加] をクリックして規則ウィザードを起動します。
4. [規則テンプレートの選択] ページの [要求規則テンプレート] で、[入力方向の要求をパススルーまたはフィルター処理する] を選択し、[次へ] をクリックします。
5. [規則の構成] ページの [要求規則名] に、この規則の表示名を入力します。[入力方向の要求の種類] で、次の要求の種類の URL を入力し、[すべての要求値をパススルー] を選択します。</br>
        `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`</br>
6. 規則を確認するには、一覧で規則を選択し、[規則の編集] をクリックして、[規則言語の表示] をクリックします。 要求規則言語は次のようになります。 `c:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip"] => issue(claim = c);`
7. [完了] をクリックします。
8. [要求規則の編集] ダイアログボックスで、[OK] をクリックして規則を保存します。
9. 手順 2. ~ 6. を繰り返して、5つのすべてのルールが作成されるまで、下に示す4つの要求の種類ごとに追加の要求規則を作成します。

    `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`


~~~
`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

`https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`
~~~

### <a name="step-3-update-the-microsoft-office-365-identity-platform-relying-party-trust"></a>手順 3: Microsoft Office 365 Id プラットフォーム証明書利用者信頼を更新する

次のシナリオ例のいずれかを選択して、組織のニーズに最も合った Microsoft Office 365 Id プラットフォーム証明書利用者信頼の要求規則を構成します。

## <a name="client-access-policy-scenarios-for-ad-fs-20"></a>AD FS 2.0 のクライアントアクセスポリシーのシナリオ
次のセクションでは、AD FS 2.0 に存在するシナリオについて説明します。

### <a name="scenario-1-block-all-external-access-to-office-365"></a>シナリオ 1: Office 365 への外部アクセスをすべてブロックする

このクライアントアクセスポリシーのシナリオでは、すべての内部クライアントからのアクセスを許可し、外部クライアントの IP アドレスに基づいてすべての外部クライアントをブロックします。 既定の発行承認規則に基づいた規則セットは、すべてのユーザーにアクセスを許可します。 発行承認規則を Office 365 証明書利用者信頼に追加するには、次の手順を実行します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 への外部アクセスをすべてブロックするルールを作成するには



1. [スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントし、[AD FS 2.0 管理] をクリックします。
2. コンソールツリーの [AD FS 2.0 \ 信頼関係] で、[証明書利用者信頼] をクリックし、Microsoft Office 365 Id プラットフォーム信頼を右クリックして、[要求規則の編集] をクリックします。 
3. [要求規則の編集] ダイアログボックスで、[発行承認規則] タブを選択し、[規則の追加] をクリックして、要求規則ウィザードを開始します。
4. [規則テンプレートの選択] ページの [要求規則テンプレート] で、[カスタム規則を使用して要求を送信する] を選択し、[次へ] をクリックします。
5. [規則の構成] ページの [要求規則名] に、この規則の表示名を入力します。 [カスタム規則] で、次の要求規則言語構文を入力するか貼り付けます: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");` 
6. [完了] をクリックします。 [発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則のすぐ下に新しい規則が表示されていることを確認します。
7. 規則を保存するには、[要求規則の編集] ダイアログボックスで [OK] をクリックします。

>[!NOTE]
>"パブリック ip アドレス regex" の上の値を有効な IP 式に置き換える必要があります。詳細については、「IP アドレス範囲を構築する」を参照してください。


### <a name="scenario-2-block-all-external-access-to-office-365-except-exchange-activesync"></a>シナリオ 2: Exchange ActiveSync 以外の Office 365 への外部アクセスをすべてブロックする

次の例では、Outlook を含む社内クライアントから、Exchange Online を含むすべての Office 365 アプリケーションにアクセスできるようにします。 クライアントの IP アドレスで示されているように、企業ネットワークの外部に存在するクライアントからのアクセスをブロックします。ただし、スマートフォンなどの Exchange ActiveSync クライアントは除きます。 規則セットは、すべてのユーザーにアクセスを許可する "という名前の既定の発行承認規則に基づいて作成されます。 要求規則ウィザードを使用して、Office 365 証明書利用者信頼に発行承認規則を追加するには、次の手順を実行します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365"></a>Office 365 への外部アクセスをすべてブロックするルールを作成するには



1. [スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントし、[AD FS 2.0 管理] をクリックします。
2. コンソールツリーの [AD FS 2.0 \ 信頼関係] で、[証明書利用者信頼] をクリックし、Microsoft Office 365 Id プラットフォーム信頼を右クリックして、[要求規則の編集] をクリックします。 
3. [要求規則の編集] ダイアログボックスで、[発行承認規則] タブを選択し、[規則の追加] をクリックして、要求規則ウィザードを開始します。
4. [規則テンプレートの選択] ページの [要求規則テンプレート] で、[カスタム規則を使用して要求を送信する] を選択し、[次へ] をクリックします。
5. [規則の構成] ページの [要求規則名] に、この規則の表示名を入力します。 [カスタム規則] で、次の要求規則言語構文を入力するか貼り付けます: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.Autodiscover"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application",
    Value=="Microsoft.Exchange.ActiveSync"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 [発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則のすぐ下に新しい規則が表示されていることを確認します。
7. 規則を保存するには、[要求規則の編集] ダイアログボックスで [OK] をクリックします。

>[!NOTE]
>"パブリック ip アドレス regex" の上の値を有効な IP 式に置き換える必要があります。詳細については、「IP アドレス範囲を構築する」を参照してください。

### <a name="scenario-3-block-all-external-access-to-office-365-except-browser-based-applications"></a>シナリオ 3: ブラウザーベースのアプリケーションを除く Office 365 への外部アクセスをすべてブロックする

規則セットは、すべてのユーザーにアクセスを許可する "という名前の既定の発行承認規則に基づいて作成されます。 要求規則ウィザードを使用して、Microsoft Office 365 Id プラットフォーム証明書利用者信頼に発行承認規則を追加するには、次の手順を実行します。

>[!NOTE]
>このシナリオは、サードパーティのプロキシではサポートされていません。これは、クライアントアクセスポリシーヘッダーに対するパッシブな (Web ベースの) 要求に制限があるためです。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>ブラウザーベースのアプリケーションを除く Office 365 への外部アクセスをすべてブロックするルールを作成するには



1. [スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントし、[AD FS 2.0 管理] をクリックします。
2. コンソールツリーの [AD FS 2.0 \ 信頼関係] で、[証明書利用者信頼] をクリックし、Microsoft Office 365 Id プラットフォーム信頼を右クリックして、[要求規則の編集] をクリックします。 
3. [要求規則の編集] ダイアログボックスで、[発行承認規則] タブを選択し、[規則の追加] をクリックして、要求規則ウィザードを開始します。
4. [規則テンプレートの選択] ページの [要求規則テンプレート] で、[カスタム規則を使用して要求を送信する] を選択し、[次へ] をクリックします。
5. [規則の構成] ページの [要求規則名] に、この規則の表示名を入力します。 [カスタム規則] で、次の要求規則言語構文を入力するか貼り付けます: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value == "/adfs/ls/"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 [発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則のすぐ下に新しい規則が表示されていることを確認します。
7. 規則を保存するには、[要求規則の編集] ダイアログボックスで [OK] をクリックします。

### <a name="scenario-4-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>シナリオ 4: 指定された Active Directory グループの Office 365 への外部アクセスをすべてブロックする

次の例では、IP アドレスに基づいて内部クライアントからのアクセスを有効にします。 これは、指定された Active Directory グループ内の個人を除き、外部クライアント IP アドレスを持つ企業ネットワークの外部に存在するクライアントからのアクセスをブロックします。この規則セットは、[すべてのユーザーにアクセスを許可する] という名前の既定の発行承認規則に基づいています。 要求規則ウィザードを使用して、Microsoft Office 365 Id プラットフォーム証明書利用者信頼に発行承認規則を追加するには、次の手順を実行します。

#### <a name="to-create-a-rule-to-block-all-external-access-to-office-365-for-designated-active-directory-groups"></a>指定された Active Directory グループの Office 365 への外部アクセスをすべてブロックするルールを作成するには



1. [スタート] をクリックし、[プログラム]、[管理ツール] の順にポイントし、[AD FS 2.0 管理] をクリックします。
2. コンソールツリーの [AD FS 2.0 \ 信頼関係] で、[証明書利用者信頼] をクリックし、Microsoft Office 365 Id プラットフォーム信頼を右クリックして、[要求規則の編集] をクリックします。 
3. [要求規則の編集] ダイアログボックスで、[発行承認規則] タブを選択し、[規則の追加] をクリックして、要求規則ウィザードを開始します。
4. [規則テンプレートの選択] ページの [要求規則テンプレート] で、[カスタム規則を使用して要求を送信する] を選択し、[次へ] をクリックします。
5. [規則の構成] ページの [要求規則名] に、この規則の表示名を入力します。 [カスタム規則] で、次の要求規則言語構文を入力するか貼り付けます: `exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy"]) &&
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "Group SID value of allowed AD group"]) &&
    NOT exists([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip",
    Value=~"customer-provided public ip address regex"])
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "true");`
6. [完了] をクリックします。 [発行承認規則] の一覧の [すべてのユーザーにアクセスを許可する] 規則のすぐ下に新しい規則が表示されていることを確認します。
7. 規則を保存するには、[要求規則の編集] ダイアログボックスで [OK] をクリックします。


### <a name="descriptions-of-the-claim-rule-language-syntax-used-in-the-above-scenarios"></a>上記のシナリオで使用される要求規則言語の構文について説明します。

|                                                                                                   説明                                                                                                   |                                                                     要求規則言語の構文                                                                     |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              すべてのユーザーへのアクセスを許可する既定の AD FS 規則。 このルールは、Microsoft Office 365 Id プラットフォーム証明書利用者信頼の発行承認規則の一覧に既に存在している必要があります。              |                                  = > の問題 (Type = "<https://schemas.microsoft.com/authorization/claims/permit>", Value = "true");                                   |
|                               この句を新しいカスタムルールに追加すると、要求がフェデレーションサーバープロキシから取得された (つまり、x.509 プロキシヘッダーがある) ことが指定されます。                                |                                                                                                                                                                    |
|                                                                                 すべてのルールにこれを含めることをお勧めします。                                                                                  |                                    exists ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy>"])                                    |
|                                                         定義された許容範囲内の IP を持つクライアントからの要求であることを確立するために使用されます。                                                         | 存在しません ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip>", Value = ~ "顧客が指定したパブリック ip アドレス regex"]) |
|                                    この句を使用して、アクセスするアプリケーションが Microsoft. Exchange. ActiveSync でない場合に、要求を拒否する必要があることを指定します。                                     |       存在しません ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application>", Value = = "Microsoft. Exchange. ActiveSync"])        |
|                                                      この規則を使用すると、呼び出しが Web ブラウザーを介して行われたかどうかを判断でき、拒否されません。                                                      |              存在しません ([Type = = "<https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path>", Value = = "/adfs/ls/"])               |
| このルールは、(SID 値に基づいて) 特定の Active Directory グループ内のユーザーのみを拒否することを示します。 このステートメントを追加しないと、場所に関係なく、ユーザーのグループが許可されます。 |             exists ([Type = = "<https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid>", Value = ~ "{Group SID Value of allowed AD group}"])              |
|                                                                これは、上記の条件がすべて満たされたときに拒否を発行するために必要な句です。                                                                 |                                   = > の問題 (Type = "<https://schemas.microsoft.com/authorization/claims/deny>", Value = "true");                                    |

### <a name="building-the-ip-address-range-expression"></a>IP アドレス範囲の作成

HTTP ヘッダーは、現在 Exchange Online によってのみ設定されています。これにより、認証要求を AD FS に渡すときにヘッダーが設定されます。 要求の値には、次のいずれかを指定できます。

>[!Note] 
>現在、Exchange Online では IPV6 以外の IPV4 アドレスのみがサポートされています。

単一の IP アドレス: Exchange Online に直接接続されているクライアントの IP アドレス

>[!Note] 
>企業ネットワーク上のクライアントの IP アドレスは、組織の送信プロキシまたはゲートウェイの外部インターフェイス IP アドレスとして表示されます。

VPN または Microsoft DirectAccess (DA) によって企業ネットワークに接続されているクライアントは、VPN または DA の構成に応じて、内部の企業クライアントとして、または外部クライアントとして表示されることがあります。

1つまたは複数の IP アドレス: Exchange Online が接続しているクライアントの IP アドレスを特定できない場合、HTTP ベースの要求に含めることができ、多くのクライアント、ロードバランサー、および市場のプロキシでサポートされる、非標準のヘッダーの値に基づいて値が設定されます。

>[!Note]
>クライアント IP アドレスと、要求を受けた各プロキシのアドレスを示す複数の IP アドレスは、コンマで区切られます。

Exchange Online インフラストラクチャに関連する IP アドレスは、一覧に表示されません。


#### <a name="regular-expressions"></a>正規表現

IP アドレスの範囲を一致させる必要がある場合は、比較を実行するために正規表現を作成する必要があります。 次の一連の手順では、次のアドレス範囲に一致するような式を作成する方法の例を示します (パブリック IP の範囲に合わせてこれらの例を変更する必要があります)。


- 192.168.1.1 –192.168.1.25
- 10.0.0.1 –10.0.0.14

まず、1つの IP アドレスに一致する基本的なパターンは次のようになります。 \b # # #\.###\.###\.# # # \b

これを拡張すると、2つの異なる IP アドレスを OR 式と一致させることができます。 \b # # #\.###\.###\.# # # \b | \b # # #\.###\.###\.# # # \b

そのため、2つのアドレス (192.168.1.1、10.0.0.1 など) のみを照合する例は次のようになります: \b192\.168\.1\.1 \ b | \b10\.0\.0\.1 \ b

これにより、任意の数のアドレスを入力できるようになります。 アドレスの範囲を許可する必要がある場合 (例: 192.168.1.1 – 192.168.1.25)、\b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b という文字で一致する必要があります。

>[!Note] 
>IP アドレスは、数値ではなく文字列として扱われます。


ルールは次のように分類されます: \b192\.168\.1\.

これは、192.168.1 から始まる任意の値と一致します。

次の例では、最後の小数点の後のアドレス部分に必要な範囲に一致します。


- ([1-9] は、1-9 で終了するアドレスと一致します
- | 1 [0-9] は、10-19 で終わるアドレスと一致します
- | 2 [0-5]) は、20-25 で終わるアドレスと一致します

>[!Note]
>かっこは、IP アドレスの他の部分との照合を開始しないように、正しく配置されている必要があります。

192ブロックが一致すると、10個のブロックに対して同様の式を記述できます。 \b10\.0\.0\.([1-9] | 1 [0-4]) \b

次の式は、"192.168.1.1 ~ 25" および "10.0.0.1 ~ 14" のすべてのアドレスと一致します。 \b192\.168\.1\.([1-9] | 1 [0-9] | 2 [0-5]) \b | \b10\.0\.0\.([1-9] | 1 [0-4]) \b

#### <a name="testing-the-expression"></a>式のテスト

Regex 式は非常に複雑になる可能性があるため、regex 検証ツールを使用することを強くお勧めします。 "オンライン正規表現ビルダー" のインターネット検索を実行すると、サンプルデータに対して式を試すことができる便利なオンラインユーティリティがいくつか用意されています。

式をテストするときは、どのようなものを一致させる必要があるかを理解することが重要です。 Exchange online システムは、コンマで区切られた多数の IP アドレスを送信する場合があります。 上記の式は、このに対して機能します。 ただし、regex 式をテストするときは、この点を考慮することが重要です。 たとえば、次のサンプル入力を使用して上記の例を確認できます。 

192.168.1.1、192.168.1.2、192.169.1.1。 192.168.12.1、192.168.1.10、192.168.1.25、192.168.1.26、192.168.1.30、1192.168.1.20 

10.0.0.1、10.0.0.5、10.0.0.10、10.0.1.0、10.0.1.1、110.0.0.1、10.0.0.14、10.0.0.15、10.0.0.10、10、0.0.1 











## <a name="validating-the-deployment"></a>デプロイの検証

### <a name="security-audit-logs"></a>セキュリティ監査ログ

新しい要求コンテキスト要求が送信されていて、AD FS 要求処理パイプラインで使用できることを確認するには、AD FS サーバーで監査ログを有効にします。 次に、認証要求を送信し、標準のセキュリティ監査ログエントリに要求値があるかどうかを確認します。 

AD FS サーバー上のセキュリティログへの監査イベントのログ記録を有効にするには AD FS 2.0 の監査の構成」の手順に従います。

### <a name="event-logging"></a>イベント ログ

既定では、失敗した要求は、[アプリケーションとサービスログ] \ AD FS 2.0 \ Admin にあるアプリケーションイベントログに記録されます。 AD FS のイベントログの詳細については、「 [AD FS 2.0 イベントログの設定](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)」を参照してください。

### <a name="configuring-verbose-ad-fs-tracing-logs"></a>詳細 AD FS トレースログの構成

AD FS トレースイベントは、AD FS 2.0 デバッグログに記録されます。 トレースを有効にするには、「 [Configure debug tracing for AD FS 2.0](https://technet.microsoft.com/library/adfs2-troubleshooting-configuring-computers.aspx)」を参照してください。

トレースを有効にした後、次のコマンドライン構文を使用して詳細ログ記録レベルを有効にします。 wevtutil sl "AD FS 2.0 Tracing/Debug"/l: 5  

## <a name="related"></a>の関係
新しい要求の種類の詳細については、「 [AD FS 要求の種類](AD-FS-Claims-Types.md)」を参照してください。

