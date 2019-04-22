---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: 代替ログイン ID を構成する
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 615faf4153949aa4ad989f017068d1809fca26b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820873"
---
# <a name="configuring-alternate-login-id"></a>代替ログイン ID を構成する

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2

## <a name="what-is-alternate-login-id"></a>代替ログイン ID とは何ですか。
ほとんどのシナリオでは、ユーザーは自分のアカウントにログインするため、UPN (ユーザー プリンシパル名) を使用します。 ただし、企業のポリシーや、オンプレミスの基幹業務アプリケーションの依存関係が原因の一部の環境では、ユーザーがサインイン用の他の何らかの形式を使用して可能性があります。 

>[!NOTE]
>Microsoft のでは、ベスト プラクティスは、UPN をプライマリ SMTP アドレスに一致するようにお勧めします。 この記事では、UPN を修復できないお客様のごく一部の一致するアドレス。

たとえば、サインイン用の電子メール id を使用することができ、UPN と異なること。 これは、UPN がルーティング不可能なシナリオで特に頻繁に発生します。 ユーザーの UPN を持つ Jane Doe を検討してください。jdoe@contoso.local電子メール アドレスとjdoe@contoso.comします。 Jane がありますも時に知っての UPN のサインインを常に自分の電子メール id を使用しています。 メソッドを使用して、その他のサインインが UPN ではなく構成別の id。 UPN は、方法の詳細については、「作成の[Azure AD の UserPrincipalName 母集団](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)します。

Active Directory フェデレーション サービス (AD FS) フェデレーション アプリケーションにサインインの代替を使用して AD FS を使用して id。 これにより、管理者の代わりに既定のサインインに使用する UPN を指定することができます。 AD FS では、その Active Directory Domain Services (AD DS) によって承認されたユーザー識別子の形式を使用して既にサポートしています。 代替 ID で構成された場合、AD FS、構成済みの別の ID 値を使用してサインイン、電子メール id とユーザーを使用できます。代替 ID を使用して、オンプレミスの Upn を変更することがなく Office 365 などの SaaS プロバイダーを採用できます。 また、コンシューマーがプロビジョニングした id を持つ基幹業務サービス アプリケーションをサポートすることもできます。

## <a name="alternate-id-in-azure-ad"></a>Azure AD での代替 id
組織は、次のシナリオで代替 ID を使用する必要があります。
1.  オンプレミスのドメイン名は、ルーティング不可能な ex です。 Contoso.local し、その結果、既定のユーザー プリンシパル名は、ルーティング不可能 (jdoe@contoso.local)。 ローカル アプリケーションの依存関係または会社のポリシーにより、既存の UPN を変更できません。 Azure AD と Office 365 は完全にインターネット ルーティング可能な Azure AD ディレクトリに関連付けられているすべてのドメイン サフィックスを必要とします。 
2.  オンプレミスの UPN がユーザーの電子メール アドレスと同じユーザーが電子メール アドレスを使用してサインインするには、Office 365 と組織の制約のために UPN を使用できません。
上記のシナリオでは、AD FS を使用して代替 ID をユーザーが、オンプレミスの Upn を変更することがなく Azure AD へのサインインを使用できます。 

## <a name="end-user-experience-with-alternate-login-id"></a>代替ログイン ID のエンドユーザー エクスペリエンス
エンド ユーザー エクスペリエンスは、代替ログイン id を使用する認証方法によって異なります。現在この代替ログイン id を使用して実現する 3 つの方法があります。  それらは以下のとおりです。

- **標準の認証 (レガシ)**-基本認証プロトコルを使用します。
- **先進認証**-アプリケーションには、Active Directory 認証ライブラリ (ADAL) ベース サインインが表示されます。 これにより、サインイン機能で多要素認証 (MFA) など、サード パーティ Id プロバイダーの SAML に基づいた Office クライアント アプリケーションは、スマート カードと証明書ベースの認証とします。
- **ハイブリッド先進認証**- 最新の認証のメリットをすべて提供し、クラウドから取得した承認トークンを使用して、オンプレミス アプリケーションにアクセスする機能を提供します。

>[!NOTE]
> 可能なエクスペリエンスを最善マイクロソフトでは、ハイブリッド先進認証が強くお勧めします。



## <a name="configure-alternate-logon-id"></a>代替ログイン ID を構成します。
Azure AD の使用をお勧めしますが環境内の別のログオン ID を構成する接続を使用して Azure AD に接続します。

- Azure AD Connect の新しい構成は、代替 ID と AD FS ファームを構成する方法の詳細な手順の Azure AD への接続を参照してください。
- 既存の Azure AD Connect のインストール、AD FS をサインイン方法を変更する方法についてのユーザーのサインイン方法の変更を参照してください。

Azure AD Connect で AD FS 環境の詳細を指定した場合、AD FS の適切なサポート技術情報の存在を確認します自動的と Azure AD のフェデレーション信頼のためのすべての必要な適切な要求規則を含む代替 ID の AD FS を構成します。 必要な外部ウィザードを代替 id。 を構成する追加の手順はありません。

>[!NOTE]
> Azure AD Connect を使用して、代替ログオン ID を構成するをお勧めします。

### <a name="manually-configure-alternate-id"></a>代替 ID を手動で構成します。
代替ログイン ID を構成するには、次のタスクを実行する必要があります。代替ログイン ID を有効にするには、AD FS 要求プロバイダー信頼を構成します。

1.  Server 2012R2 がある場合は場合、は、KB2919355 がすべての AD FS サーバーにインストールされている必要があることを確認します。 Windows Update Services 経由で入手したり、直接ダウンロードできます。 

2.  ファーム内のフェデレーション サーバーのいずれかで、次の PowerShell コマンドレットを実行して、AD FS の構成を更新 (WID ファームがあれば、する必要がありますコマンドを実行するこのファームのプライマリ AD FS サーバー上)。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>
```

**AlternateLoginID**ログインを使用する属性の LDAP 名前を指定します。

**LookupForests**フォレストにユーザーが属している DNS の一覧を示します。

代替ログイン ID の機能を有効にするには、null 以外の場合は有効な値を持つ AlternateLoginID - と - LookupForests の両方のパラメーターを構成する必要があります。

次の例で、"mail"属性を持つ AD FS が有効なアプリケーションを contoso.com と fabrikam.com のフォレスト内のアカウントにユーザーがログインできるように、代替ログイン ID の機能を有効にします。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
```

3.  この機能を無効にするには、null にすることの両方のパラメーターの値を設定します。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>代替 ID を持つハイブリッド先進認証

>[!IMPORTANT]
>次はのみに対してテスト済み AD FS といないサード パーティ id プロバイダー。

### <a name="exchange-and-skype-for-business"></a>Exchange と Skype for Business
ビジネス向けに Exchange と Skype 代替ログイン id を使用する場合、ユーザー エクスペリエンスはときなどを使用しているかどうかによって異なります。

>[!NOTE]
>最高のエンド ユーザー エクスペリエンスのハイブリッド先進認証を使用をお勧めします。

詳細については、「または[ハイブリッド先進認証の概要](https://support.office.com/en-us/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d)

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Exchange と Skype for Business の前提条件
代替 ID での SSO を実現するための前提条件を次に示します

- Exchange Online の先進認証を有効化されている必要があります。
- ビジネス (デバイス) online、Skype に先進認証を有効化されている必要があります。
- Exchange は、on-premises にする必要がありますが最新の認証点灯します。  Exchange 2013 CU19 または Exchange 2016 CU18 とすべての Exchange サーバーにアップが必要です。 環境で Exchange 2010 がありません。
- Skype for Business オンプレミスにする必要がありますが最新の認証点灯します。
- 先進認証を有効にしているクライアントが Exchange と Skype を使用する必要があります。 すべてのサーバーには、デバイス Server 2015 CU5 を実行する必要があります。
- 先進認証が可能であるビジネス クライアントの Skype
   - iOS、Android、Windows Phone
   - デバイス 2016年 (既定では、MA は ON です。 が無効になっていないことを確認します)。
   - デバイス 2013年 (MA は、既定で OFF、ようにして MA がオンにされました)。
   - デバイスの Mac デスクトップ
- 先進認証ができるは、AltID レジストリをサポートする Exchange クライアント
    - Office Pro Plus 2016 のみ





#### <a name="supported-office-version"></a>サポートされている Office のバージョン

SSO の代替 id を使用する代替の id を持つ、ディレクトリを設定すると、これらの追加構成が完了していない場合に認証の追加のプロンプトが発生することができます。 代替 id のユーザー エクスペリエンスに影響を及ぼすの記事を参照してください。

次の追加の構成では、ユーザー エクスペリエンスが大幅に向上し、組織の代替 id のユーザーの認証の 0 個のプロンプトの近くに実現できます。

##### <a name="step-1-update-to-required-office-version"></a>手順 1. 必要な office のバージョンに更新するには
Office バージョン 1712 (8827.2148 ビルドなし) され、上記の代替 id のシナリオを処理するために認証ロジックが更新されました。 新しいロジックを利用するために、クライアント コンピューターは、(8827.2148 ビルドなし) の office バージョン 1712 以降に更新する必要があります。

##### <a name="step-2-configure-registry-for-impacted-users-using-group-policy"></a>手順 2.  グループ ポリシーを使用して、影響を受けるユーザーのレジストリを構成します。
Office アプリケーションは、代替 id の環境を識別するために、ディレクトリ管理者によってプッシュされる情報に依存します。 次のレジストリ キーは、office アプリケーションを追加のプロンプトを表示することがなく代替 id を持つユーザーを認証するように構成する必要があります。

|レジストリ キーを追加するには|レジストリ キーのデータの名前、種類、および値|Windows 7/8|Windows 10|説明|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER\Software\Microsoft\AuthN|DomainHint</br>REG_SZ</br>contoso.com|必須|必須|このレジストリ キーの値は、組織のテナントで検証済みカスタム ドメイン名です。 たとえば、Contoso corp は、Contoso.com が Contoso.onmicrosoft.com のテナントで検証済みのカスタム ドメイン名のいずれかである場合、このレジストリ キーには、Contoso.com の値を指定できます。|
HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\Identity|EnableAlternateIdSupport</br>REG_DWORD</br>1|Outlook 2016 ProPlus に必要な|Outlook 2016 ProPlus に必要な|このレジストリ キーの値は 1 を指定できます/0 を Outlook のアプリケーションに強化された代替 id の認証ロジックを連携する必要があるかどうかを示します。|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableADALatopWAMOverride</br>REG_DWORD</br>1|該当なし|必須。|これにより、その Office で使用されない WAM WAM で alt キー id がサポートされていません。|
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Office\16.0\Common\Identity|DisableAADWAM</br>REG_DWORD</br>1|該当なし|必須。|これにより、その Office で使用されない WAM WAM で alt キー id がサポートされていません。|
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\contoso.com\sts|&#42;</br>REG_DWORD</br>1|必須|必須|STS をインターネットの設定で信頼済みゾーンとして設定するのには、このレジストリ キーを使用できます。 ADFS の標準の展開は、Internet Explorer のローカル イントラネット ゾーンの ADFS 名前空間を追加することをお勧めします|

## <a name="new-authentication-flow-after-additional-configuration"></a>追加の構成後に新しい認証フロー

![認証フロー](media/Configure-Alternate-Login-ID/alt1a.png)

1. A:代替 id を使用して Azure AD でユーザーがプロビジョニングされます。
   </br>B:ディレクトリの管理者の影響を受けるクライアント コンピューターに必要なレジストリ キー設定をプッシュします。
2. ユーザーがローカル コンピューターを認証し、office アプリケーションを開きます
3. Office アプリケーションがローカルのセッションの資格情報を受け取る
4. Office アプリケーションが管理者とローカルの資格情報によってプッシュされるドメイン ヒントを使用して Azure AD に認証します。
5. Azure AD がリダイレクト フェデレーション領域を修正し、トークンを発行してユーザーを正常に認証します。

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>アプリケーションとユーザー エクスペリエンスの追加の構成後

### <a name="non-exchange-and-skype-for-business-clients"></a>非 Exchange と Skype for Business クライアント
|クライアント|サポートに関する声明|注釈|
| ----- | -----|-----|
|Microsoft Teams|サポートされている|<li>Microsoft Teams は、AD FS をサポートしています (SAML-P、Ws-fed、Ws-trust、および OAuth) と最新の認証。</li><li> 代替ログイン ID を持つコア Microsoft Teams のチャネル、チャット、およびファイルの機能などの機能します。</li><li>1 番目と 3 番目のパーティのアプリは、顧客が個別に調べる必要があります。 これは、ため、各アプリケーションには、独自のサポートの認証プロトコルです。</li>|     
|OneDrive for Business|サポートされています - クライアント側のレジストリ キーをお勧めします |構成されている代替 id は、検証フィールドに、オンプレミスの UPN があらかじめ設定されているを参照してください。 これは、使用されている代替 Id に変更する必要があります。 この記事に記載されているクライアント側のレジストリ キーの使用をお勧めします。Office 2013 および Lync 2013 は、SharePoint Online、OneDrive、および Lync Online に資格情報を定期的に要求します。|
|OneDrive for Business モバイル クライアント|サポートされている|| 
|Office 365 Pro Plus のアクティブ化 ページ|サポートされています - クライアント側のレジストリ キーをお勧めします|構成されている代替 id は、検証フィールドに、オンプレミスの UPN があらかじめ設定されているを参照してください。 これは、使用されている代替 Id に変更する必要があります。 この記事に記載されているクライアント側のレジストリ キーを使用してをお勧めします。Office 2013 および Lync 2013 は、SharePoint Online、OneDrive、および Lync Online に資格情報を定期的に要求します。|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange と Skype for Business クライアント

|クライアント|サポートに関する声明 - ときなどに|サポートに関する声明 - ときなどなし|
| ----- |----- | ----- |
|Outlook|サポートされている、全くのプロンプト|サポートされている</br></br>**先進認証**の Exchange Online:サポートされている</br></br>**正規認証**Exchange online:次の注意事項でサポートされています。</br><li>企業ネットワークに接続してドメイン参加済みコンピューターである必要があります。 </li><li>代替 ID は、メールボックスのユーザーの外部アクセスを許可しない環境でのみ使用できます。 これは、ユーザー認証できることがのみのメールボックスにサポートされている方法で接続されていると、vpn、企業ネットワークに参加しているまたはマシンに直接アクセス、を介して接続されているが、Outlook プロファイルを構成するときに、いくつかの余分なプロンプトを取得するときにことを意味します。| 
|ハイブリッドのパブリック フォルダー|サポートされている、いいえ余分なプロンプト。|**先進認証**の Exchange Online:サポートされている</br></br>**正規認証**Exchange online:サポートされない</br></br><li>ハイブリッドのパブリック フォルダーは、代替 ID を使用しする必要がありますいないため、現在標準の認証方法と場合を拡張することはできません。|
|オンプレミスの委任をクロスします。|参照してください[ハイブリッド展開でメールボックスの委任されたアクセス許可をサポートするために Exchange を構成します。](https://technet.microsoft.com/library/mt784505.aspx)|参照してください[ハイブリッド展開でメールボックスの委任されたアクセス許可をサポートするために Exchange を構成します。](https://technet.microsoft.com/library/mt784505.aspx)|
|アーカイブのメールボックスへのアクセス (メールボックス、オンプレミス、クラウドでのアーカイブ)|サポートされている、全くのプロンプト|サポートされています - ユーザーが、アーカイブにアクセスするときに、資格情報の追加のプロンプトを表示には、入力を求められたら、代替 ID を指定する必要あります。| 
|Outlook Web Access|サポートされている|サポートされている|
|Android、IOS、および Windows Phone 用の outlook モバイル アプリ|サポートされている|サポートされている|
|Skype for Business/Lync|余分なプロンプトなしでサポートします。|サポートされています (前述のようを除く) がユーザーの混乱が発生する可能性があります。</br></br>モバイル クライアントは、別の Id がサポートされている場合にのみの SIP アドレスの電子メール アドレスを = = 代替 id。</br></br> ユーザーがオンプレミスの UPN を使用する方法と、代替の ID を使用して、ビジネスのデスクトップ クライアントを Skype に 2 回のサインインする必要があります。 (「サインイン アドレス」が実際に「ユーザー名」と同じである可能性がありますいないは多くの場合は、SIP アドレスに注意してください。) 最初にユーザー名の入力を求め、ときに、ユーザーは、場合でも、それは正しくであらかじめ設定されていない代替 ID または SIP アドレス、UPN を入力する必要があります。 サインインして、UPN、ユーザー名のプロンプトが再表示されます、UPN を使用してあらかじめ入力されています。 この時間をクリックした後、ユーザーにします。 今度は、ユーザーがこれを代替 ID で置き換えます、をクリックする必要がありますが、サインイン プロセスを完了にサインインするとします。 モバイル クライアントでユーザーする必要があります、オンプレミス ユーザー ID を入力 [詳細設定] ページで、SAM スタイルの形式 (domain \username)、UPN 形式ではなくを使用します。</br></br>成功したサインイン後に「Exchange には、資格情報が必要がある、」が Skype for Business または Lync の場合必要があります、メールボックスが有効な資格情報を提供します。 メールボックスがクラウド内にある場合は、代替の ID を提供する必要があります。 メールボックスが、オンプレミスの場合は、オンプレミスの UPN を提供する必要があります。| 
 
## <a name="additional-details--considerations"></a>追加の詳細と考慮事項

-   代替ログイン ID 機能は、デプロイされる AD FS でフェデレーション環境で使用できます。  次のシナリオではサポートされません。
    -   非ルーティング可能なドメイン (例: Contoso.local) を Azure AD によって検証されることはできません。
    -   AD FS のデプロイがない環境を管理します。


-   あらゆる、ユーザー名/パスワード認証プロトコルで AD FS でサポートされている代替ログイン ID の機能はユーザー名/パスワード認証に使用できるでのみ有効にすると (SAML-P、Ws-fed、Ws-trust、および OAuth)。


-   Windows 統合認証 (WIA) を実行ときに (たとえばとユーザーが、イントラネットからドメインに参加しているコンピューター上の企業アプリケーションにアクセスしようとしています AD FS 管理者には、イントラネットに WIA を使用する認証ポリシーが構成されている)、、UPN 使われます。認証します。 代替ログイン ID の機能の証明書利用者のすべての要求規則を構成している場合はそれらのルールが WIA ケースではまだ有効であることを確認する必要があります。

-   有効な場合、代替ログイン ID の機能には AD FS がサポートする各ユーザー アカウント フォレストの AD FS サーバーから到達可能にするには少なくとも 1 つのグローバル カタログ サーバーが必要です。 フォールバック UPN を使用する AD FS によりユーザーのアカウント フォレスト内のグローバル カタログ サーバーに到達できません。 既定では、すべてのドメイン コント ローラーは、グローバル カタログ サーバーが。

-   有効になっている場合は、AD FS サーバーで構成したユーザー アカウントのすべてのフォレスト間で指定された同じ代替ログイン ID の値を持つ 1 つ以上のユーザー オブジェクトを検索するときに、ログインが失敗します。

-   AD FS が最初に代替ログイン ID を持つエンドユーザーを認証し、代替ログイン ID で識別できるアカウントを見つけられない場合は、UPN を使用するフォールバックを試みます代替ログイン ID の機能を有効にすると、 まだ UPN ログインをサポートする場合、代替ログイン ID と UPN 間の競合がないことを確認する必要があります。 UPN はたとえば、1 つの mail 属性とその他の設定の他のユーザーが自分の UPN でサインインをブロックします。

-   場合は、管理者が構成されているフォレストの 1 つは、AD FS が構成されている他のフォレスト内の代替ログイン ID を持つユーザー アカウントを検索する続行されます。 AD FS サーバーでは、検索が、フォレスト間で一意のユーザー オブジェクトを検索する場合、ユーザーが正常にログインします。

-   代替ログイン ID に関するいくつかのヒントをエンドユーザーに提供する AD FS サインイン ページをカスタマイズすることもさらに カスタマイズされたサインイン ページの説明を追加して行うことができます (詳細については、次を参照してください[AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)または (複数のユーザー名 フィールド上に"組織アカウントでサインイン"の文字列をカスタマイズする。についてを参照してください[Advanced Customization of AD FS サインイン ページ](https://technet.microsoft.com/library/dn636121.aspx)します。

-   代替ログイン ID の値を含む新しい要求の種類は**http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>イベントとパフォーマンス カウンター
代替ログイン ID が有効にすると、AD FS サーバーのパフォーマンスを測定には、次のパフォーマンス カウンターが追加されています。

-   代替ログイン ID を使用して実行する認証の代替ログイン Id の認証: 数

-   1 秒あたりの代替ログイン ID を使用して実行する認証の数を代替ログイン Id の認証/秒の:

-   代替ログイン ID の検索の待機時間の平均: 代替ログイン ID の管理者が構成されるフォレスト間の平均検索待機時間

以下は、さまざまなエラー ケースと対応する AD FS によって記録されたイベントでは、ユーザーのサインイン エクスペリエンスへの影響です。



**エラー ケース**|**サインイン エクスペリエンスへの影響**|**イベント**|
---------|---------|---------
ユーザー オブジェクトの SAMAccountName の値を取得できません。|ログインに失敗しました|例外メッセージ MSIS8012 にイベント ID 364:ユーザーの samAccountName が見つかりません: '{0}'。|
用の属性にアクセスできません。|ログインに失敗しました|例外メッセージ MSIS8013 にイベント ID 364:用: '{0}' のユーザー:'{1}' が不適切な形式でします。|
1 つのフォレスト内に複数のユーザー オブジェクトがあります。|ログインに失敗しました|例外メッセージ MSIS8015 にイベント ID 364:Id を持つ複数のユーザー アカウントが見つかりません '{0}'in 'フォレスト{1}' id: {2}|
複数のユーザー オブジェクトが複数のフォレストが見つかりません|ログインに失敗しました|例外メッセージ MSIS8014 にイベント ID 364:Id を持つ複数のユーザー アカウントが見つかりません '{0}' フォレストで。 {1}|

## <a name="see-also"></a>関連項目
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)


