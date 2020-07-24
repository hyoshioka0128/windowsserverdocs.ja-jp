---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: 代替ログイン ID を構成する
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 11/14/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0872131de7ba2a201b0a0e70fb6157b0e2706def
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86958634"
---
# <a name="configuring-alternate-login-id"></a>代替ログイン ID を構成する


## <a name="what-is-alternate-login-id"></a>代替ログイン ID とは
ほとんどのシナリオでは、ユーザーは自分の UPN (ユーザープリンシパル名) を使用してアカウントにログインします。 ただし、企業のポリシーやオンプレミスの基幹業務アプリケーションの依存関係が原因で、環境によっては、他の形式のサインインが使用されている場合があります。 

>[!NOTE]
>Microsoft の推奨されるベストプラクティスは、UPN をプライマリ SMTP アドレスに一致させることです。 この記事では、UPN を修復できないお客様の小さな割合について説明します。

たとえば、サインインには電子メール id を使用し、UPN とは異なる場合があります。 これは特に、UPN がルーティング不可能なシナリオで一般的に発生します。 UPN jdoe@contoso.local と電子メールアドレスを持つユーザー Jane Doe を考えてみましょう jdoe@contoso.com 。 サインインにメール id を常に使用しているため、Jane は UPN を認識していない可能性があります。 UPN ではなく他のサインイン方法を使用すると、代替 ID が構成されます。 UPN の作成方法の詳細については、「UserPrincipalName の作成[Azure AD](/azure/active-directory/connect/active-directory-aadconnect-userprincipalname)」を参照してください。

Active Directory フェデレーションサービス (AD FS) (AD FS) を使用すると、AD FS を使用するフェデレーションアプリケーションで代替 ID を使用してサインインできます。 これにより、管理者は、サインインに使用する既定の UPN の代わりにを指定できます。 AD FS は、Active Directory Domain Services (AD DS) で受け入れられる任意の形式のユーザー識別子の使用を既にサポートしています。 代替 ID として構成されている場合、AD FS では、ユーザーは構成された代替 ID 値 (たとえば、電子メール ID) を使用してサインインできます。代替 ID を使用すると、オンプレミスの Upn を変更することなく、Office 365 などの SaaS プロバイダーを採用できます。 また、コンシューマーがプロビジョニングした id で基幹業務サービスアプリケーションをサポートすることもできます。

## <a name="alternate-id-in-azure-ad"></a>Azure AD の代替 id
組織は、次のシナリオで代替 ID を使用する必要がある場合があります。
1. オンプレミスのドメイン名は、ルーティング不可能な例です。 その結果、既定のユーザープリンシパル名はルーティング不可能 () になり jdoe@contoso.local ます。 ローカルアプリケーションの依存関係または会社のポリシーにより、既存の UPN を変更することはできません。 Azure AD と Office 365 では、Azure AD ディレクトリに関連付けられているすべてのドメインサフィックスが完全にインターネットにルーティング可能である必要があります。 
2. オンプレミスの UPN は、ユーザーの電子メールアドレスと同じではなく、Office 365 にサインインするために、組織の制約により、ユーザーが電子メールアドレスと UPN を使用することはできません。
   前述のシナリオでは、AD FS による代替 ID を使用すると、ユーザーはオンプレミスの Upn を変更することなく Azure AD にサインインできます。 

## <a name="end-user-experience-with-alternate-login-id"></a>代替ログイン ID を使用したエンドユーザーエクスペリエンス
エンドユーザーエクスペリエンスは、代替ログイン id で使用される認証方法によって異なります。 現在、代替ログイン id を使用する方法は3種類あります。  これらは次のとおりです。

- **標準認証 (レガシ)**-基本認証プロトコルを使用します。
- **先進認証**-ACTIVE DIRECTORY 認証ライブラリ (ADAL) ベースのサインインをアプリケーションに提供します。 これにより、Multi-Factor Authentication (MFA)、SAML ベースのサードパーティ Id プロバイダー (Office クライアントアプリケーションを含む)、スマートカード、証明書ベースの認証などのサインイン機能が有効になります。
- **ハイブリッド先進認証**-先進認証のすべての利点を提供し、クラウドから取得した承認トークンを使用して、オンプレミスのアプリケーションにアクセスする機能をユーザーに提供します。

>[!NOTE]
> 最適なエクスペリエンスを実現するために、Microsoft はハイブリッド先進認証を強く推奨しています。



## <a name="configure-alternate-logon-id"></a>代替ログオン ID の構成
Azure AD Connect 使用する場合は、Azure AD 接続を使用して、環境の代替ログオン ID を構成することをお勧めします。

- Azure AD Connect の新しい構成については、代替 ID と AD FS ファームを構成する方法の詳細な手順については、「Azure AD への接続」を参照してください。
- 既存の Azure AD Connect インストールについては、「サインイン方法の変更」の手順について「ユーザーのサインイン方法の変更」を参照してください AD FS

AD FS 環境の詳細を指定 Azure AD Connect と、AD FS に適切な KB があるかどうかが自動的にチェックされ、Azure AD フェデレーションの信頼に必要なすべての要求規則を含む代替 ID の AD FS が構成されます。 ウィザードの外部で代替 ID を構成するために必要な追加の手順はありません。

>[!NOTE]
> 代替ログオン ID を構成するには Azure AD Connect を使用することをお勧めします。

### <a name="manually-configure-alternate-id"></a>代替 ID の手動構成
代替ログイン ID を構成するには、次のタスクを実行する必要があります。代替ログイン ID を有効にするための AD FS 要求プロバイダー信頼の構成

1.  サーバー2012R2 を使用している場合は、すべての AD FS サーバーに KB2919355 がインストールされていることを確認してください。 Windows Update Services を使用して取得することも、直接ダウンロードすることもできます。 

2.  ファーム内のいずれかのフェデレーションサーバーで次の PowerShell コマンドレットを実行して、AD FS 構成を更新します (WID ファームがある場合は、ファーム内のプライマリ AD FS サーバーでこのコマンドを実行する必要があります)。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>
```

**Alternateloginid**は、ログインに使用する属性の LDAP 名です。

**Lookupforests**は、ユーザーが属するフォレスト DNS の一覧です。

代替ログイン ID 機能を有効にするには、-AlternateLoginID と-LookupForests の両方のパラメーターを null 以外の有効な値で構成する必要があります。

次の例では、contoso.com および fabrikam.com フォレスト内のアカウントを持つユーザーが "mail" 属性を使用して AD FS 対応アプリケーションにログインできるように、代替ログイン ID 機能を有効にしています。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
```

3. この機能を無効にするには、両方のパラメーターの値を null に設定します。

``` powershell
Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
```

## <a name="hybrid-modern-authentication-with-alternate-id"></a>代替 ID を使用したハイブリッド先進認証

>[!IMPORTANT]
>次のは、サードパーティの id プロバイダーではなく AD FS に対してのみテストされています。

### <a name="exchange-and-skype-for-business"></a>Exchange と Skype for Business
Exchange と Skype for Business で代替ログイン id を使用している場合、ユーザーエクスペリエンスは、HMA を使用しているかどうかによって異なります。

>[!NOTE]
>エンドユーザーエクスペリエンスを最大限に高めるために、ハイブリッド先進認証を使用することをお勧めします。

詳細については、「[ハイブリッド先進認証の概要](https://support.office.com/article/Hybrid-Modern-Authentication-overview-and-prerequisites-for-using-it-with-on-premises-Skype-for-Business-and-Exchange-servers-ef753b32-7251-4c9e-b442-1a5aec14e58d)」を参照してください。

### <a name="pre-requisites-for-exchange-and-skype-for-business"></a>Exchange と Skype for Business の前提条件
代替 ID で SSO を実現するための前提条件は次のとおりです。

- Exchange Online では、先進認証が有効になっている必要があります。
- Skype for Business (SFB) オンラインでは、先進認証が有効になっている必要があります。
- オンプレミスの Exchange では、先進認証が有効になっている必要があります。  Exchange 2013 CU19 または Exchange 2016 CU18 および up は、すべての Exchange サーバーで必要です。 環境に Exchange 2010 がありません。
- Skype for Business オンプレミスでは、先進認証が有効になっている必要があります。
- 最新の認証が有効になっている Exchange および Skype クライアントを使用する必要があります。 すべてのサーバーで SFB Server 2015 CU5 が実行されている必要があります。
- 先進認証に対応している Skype for Business クライアント
   - iOS、Android、Windows Phone
   - SFB 2016 (MA は既定でオンになっていますが、無効になっていないことを確認してください)。
   - SFB 2013 (MA は既定でオフになっているため、MA がオンになっていることを確認してください)。
   - SFB Mac デスクトップ
- 最新の認証に対応していて AltID regkeys をサポートしている Exchange クライアント
    - Office Pro Plus 2016 のみ





#### <a name="supported-office-version"></a>サポートされている Office のバージョン

代替 id を使用して代替 id で SSO 用にディレクトリを構成すると、追加の構成が完了していない場合、認証のための追加のプロンプトが発生する可能性があります。 代替 id を使用したユーザーエクスペリエンスへの影響については、「」を参照してください。

次の追加の構成を使用すると、ユーザーエクスペリエンスが大幅に向上し、組織内の代替 id ユーザーの認証について、ほぼゼロのプロンプトが表示されます。

##### <a name="step-1-update-to-required-office-version"></a>手順 1. 必須の Office バージョンに更新する
Office バージョン 1712 (build no 8827.2148) 以降では、代替 id シナリオを処理するために認証ロジックが更新されました。 新しいロジックを利用するには、クライアントコンピューターを Office バージョン 1712 (8827.2148 をビルドしない) 以降に更新する必要があります。

##### <a name="step-2-update-to-required-windows-version"></a>手順 2. 必須の Windows バージョンに更新する
Windows バージョン1709以降では、代替 id シナリオを処理するために認証ロジックが更新されました。 新しいロジックを利用するには、クライアントコンピューターを Windows バージョン1709以降に更新する必要があります。

##### <a name="step-3-configure-registry-for-impacted-users-using-group-policy"></a>手順 3. グループポリシーを使用して影響を受けるユーザーのレジストリを構成する
Office アプリケーションは、代替 id 環境を識別するために、ディレクトリ管理者によってプッシュされた情報に依存しています。 次のレジストリキーは、office アプリケーションが、追加のプロンプトを表示せずに、代替 id を使用してユーザーを認証できるように構成する必要があります。

|追加するレジストリキー|レジストリキーのデータ名、型、および値|Windows 7/8|Windows 10|説明|
|-----|-----|-----|-----|-----|
|HKEY_CURRENT_USER \Software\Microsoft\AuthN|DomainHint</br>REG_SZ</br>contoso.com|必須|必須|このレジストリキーの値は、組織のテナントで検証されたカスタムドメイン名です。 たとえば、Contoso corp では、Contoso.com がテナント Contoso.onmicrosoft.com の検証済みのカスタムドメイン名の1つである場合、このレジストリキーに Contoso.com の値を指定できます。|
HKEY_CURRENT_USER \Software\Microsoft\Office\16.0\Common\Identity|EnableAlternateIdSupport</br>REG_DWORD</br>1|Outlook 2016 ProPlus に必要|Outlook 2016 ProPlus に必要|このレジストリキーの値は、強化された代替 id 認証ロジックを使用する必要があるかどうかを Outlook アプリケーションに示す 1/0 にすることができます。|
HKEY_CURRENT_USER \Software\Microsoft\Windows\CurrentVersion\Internet Settings\ZoneMap\Domains\contoso.com\sts|&#42;</br>REG_DWORD</br>1|必須|必須|このレジストリキーを使用して、インターネットの設定で STS を信頼済みゾーンとして設定できます。 標準の ADFS 展開では、ADFS 名前空間を Internet Explorer のローカルイントラネットゾーンに追加することをお勧めします。|

## <a name="new-authentication-flow-after-additional-configuration"></a>追加の構成後の新しい認証フロー

![Authentication flow](media/Configure-Alternate-Login-ID/alt1a.png)

1. a: ユーザーは、代替 id を使用して Azure AD にプロビジョニングされています
   </br>b: ディレクトリ管理者は、影響を受けるクライアントコンピューターに必要なレジストリ設定をプッシュします。
2. ユーザーがローカルコンピューターで認証を行い、office アプリケーションを開く
3. Office アプリケーションがローカルセッションの資格情報を取得する
4. 管理者およびローカルの資格情報によってプッシュされたドメインヒントを使用して Azure AD に対する Office アプリケーションの認証
5. Azure AD は、フェデレーション領域を修正してトークンを発行することで、ユーザーを正しく認証します。

## <a name="applications-and-user-experience-after-the-additional-configuration"></a>追加の構成後のアプリケーションとユーザーエクスペリエンス

### <a name="non-exchange-and-skype-for-business-clients"></a>Exchange 以外のクライアントと Skype for Business クライアント

|クライアント|サポートに関する声明|注釈|
| ----- | -----|-----|
|Microsoft Teams|サポートされています|<li>Microsoft Teams は、AD FS (SAML P、WS-ATOMICTRANSACTION、WS-TRUST、および OAuth) と先進認証をサポートしています。</li><li> チャンネル、チャット、ファイルなどの主要な Microsoft チームは、代替ログイン ID を使用します。</li><li>1番目とサードパーティのアプリは、顧客が個別に調査する必要があります。 これは、各アプリケーションが独自のサポート認証プロトコルを持っているためです。</li>|     
|OneDrive for Business|サポートされている-クライアント側のレジストリキーを推奨します |代替 ID が構成されている場合は、オンプレミスの UPN が検証フィールドに事前設定されていることがわかります。 これは、使用されている代替 Id に変更する必要があります。 この記事に記載されているクライアント側のレジストリキーを使用することをお勧めします。 Office 2013 および Lync 2013 では、SharePoint Online、OneDrive、および Lync Online への資格情報を定期的に確認するように求められます。|
|OneDrive for Business モバイルクライアント|サポートされています|| 
|Office 365 Pro Plus ライセンス認証ページ|サポートされている-クライアント側のレジストリキーを推奨します|代替 ID が構成されている場合は、オンプレミスの UPN が検証フィールドに事前設定されていることがわかります。 これは、使用されている代替 Id に変更する必要があります。 この記事で説明されているクライアント側のレジストリキーを使用することをお勧めします。 Office 2013 および Lync 2013 は、SharePoint Online、OneDrive、および Lync Online への資格情報を定期的に確認します。|

### <a name="exchange-and-skype-for-business-clients"></a>Exchange と Skype for Business クライアント

|クライアント|サポートステートメント-HMA がある|サポートステートメント-HMA なし|
| ----- |----- | ----- |
|Outlook|サポートされています。追加のプロンプトはありません|サポートされています</br></br>Exchange Online の**先進認証**を使用する: サポートされています。</br></br>Exchange Online の**通常の認証**では、次の点に注意してください。</br><li>ドメインに参加しているコンピューターで、企業ネットワークに接続している必要があります。 </li><li>代替 ID は、メールボックスユーザーの外部アクセスを許可しない環境でのみ使用できます。 これは、ユーザーが会社のネットワーク、VPN、または直接アクセスコンピューターを使用して接続されている場合に、メールボックスに対してのみ認証を行うことができることを意味します。ただし、Outlook プロファイルを構成するときに、いくつかの追加のプロンプトが表示されます。| 
|ハイブリッドパブリックフォルダー|サポートされています。特別なプロンプトはありません。|Exchange Online の**先進認証**を使用する: サポートされています。</br></br>Exchange Online の**通常の認証**を使用する: サポートされていません。</br></br><li>ハイブリッドパブリックフォルダーは、代替 ID が使用されている場合は拡張できないため、現在は通常の認証方法では使用できません。|
|クロスプレミスの委任|[ハイブリッド展開での委任されたメールボックスのアクセス許可をサポートするように Exchange を構成する](/exchange/hybrid-deployment/set-up-delegated-mailbox-permissions)|[ハイブリッド展開での委任されたメールボックスのアクセス許可をサポートするように Exchange を構成する](/exchange/hybrid-deployment/set-up-delegated-mailbox-permissions)|
|メールボックスへのアクセス (オンプレミスのメールボックス-クラウド内のアーカイブ)|サポートされています。追加のプロンプトはありません|サポートされている-ユーザーは、アーカイブにアクセスするときに資格情報の追加のプロンプトを受け取り、プロンプトが表示されたら代替 ID を入力する必要があります。| 
|Outlook Web Access|サポートされています|サポートされています|
|Android、IOS、および Windows Phone 用 Outlook Mobile Apps|サポートされています|サポートされています|
|Skype for Business/Lync|サポートされています。追加のプロンプトはありません|サポートされています (ただし、前述の場合を除く) が、ユーザーの混乱を招く可能性があります。</br></br>モバイルクライアントでは、代替 Id がサポートされるのは、SIP アドレス = 電子メールアドレス = 代替 ID の場合のみです。</br></br> ユーザーは、最初にオンプレミスの UPN を使用し、次に代替 ID を使用して、Skype for Business デスクトップクライアントに2回サインインする必要がある場合があります。 ("サインインアドレス" は、実際には "ユーザー名" と同じではない可能性がある SIP アドレスです。ただし、多くの場合は)。 ユーザー名の入力を求められた場合、代替 ID または SIP アドレスが誤って事前設定されていても、ユーザーは UPN を入力する必要があります。 ユーザーが UPN でサインインすると、ユーザー名のプロンプトが再び表示されます。今回は UPN で事前に登録されています。 今回は、ユーザーがこれを代替 ID で置き換える必要があります。サインインプロセスを完了するには、[サインイン] をクリックします。 モバイルクライアントでは、ユーザーは [詳細設定] ページで、UPN 形式ではなく SAM 形式 (domain\username) を使用して、オンプレミスのユーザー ID を入力する必要があります。</br></br>サインインに成功した後に、Skype for Business または Lync に "Exchange で資格情報が必要です" と表示されている場合は、メールボックスが存在する場所に対して有効な資格情報を入力する必要があります。 メールボックスがクラウド内にある場合は、代替 ID を指定する必要があります。 メールボックスがオンプレミスの場合は、オンプレミスの UPN を指定する必要があります。| 

## <a name="additional-details--considerations"></a>追加の詳細 & 考慮事項

-   代替ログイン ID 機能は、AD FS デプロイされたフェデレーション環境で使用できます。  次のシナリオではサポートされていません。
    -   Azure AD によって検証できないルーティング不可能なドメイン (例: Contoso. ローカル)。
    -   AD FS デプロイされていないマネージ環境。


-   有効にした場合、代替ログイン ID 機能は、AD FS でサポートされているすべてのユーザー名/パスワード認証プロトコル (SAML P、WS-ATOMICTRANSACTION、WS-TRUST、および OAuth) のユーザー名/パスワード認証でのみ使用できます。


-   Windows 統合認証 (WIA) を実行する場合 (たとえば、ユーザーがイントラネットからドメインに参加しているコンピューターの企業アプリケーションにアクセスしようとしたときに、AD FS 管理者によって認証ポリシーがイントラネットに対して WIA を使用するように構成されている場合)、UPN isused が認証に使用されます。 代替ログイン ID 機能のために証明書利用者の要求規則を構成した場合は、これらの規則が引き続き WIA ケースで有効であることを確認してください。

-   代替ログイン ID 機能を有効にすると、AD FS がサポートする各ユーザーアカウントフォレストに対して、AD FS サーバーから少なくとも1つのグローバルカタログサーバーにアクセスできる必要があります。 ユーザーアカウントフォレストのグローバルカタログサーバーに接続できない場合は、UPN を使用するようにフォールバック AD FS ます。 既定では、すべてのドメインコントローラーはグローバルカタログサーバーです。

-   有効にした場合、AD FS サーバーが、構成されているすべてのユーザーアカウントフォレストで同じ代替ログイン ID 値を使用して複数のユーザーオブジェクトを検出すると、ログインに失敗します。

-   代替ログイン ID 機能が有効になっている場合、AD FS は、最初に代替ログイン id を使用してエンドユーザーの認証を試み、次に代替ログイン ID で識別できるアカウントが見つからない場合に UPN を使用するようにフォールバックします。 UPN ログインを引き続きサポートする場合は、代替ログイン ID と UPN が競合していないことを確認してください。 たとえば、あるメール属性をもう一方の UPN で設定すると、他のユーザーは UPN でサインインできません。

-   管理者によって構成されているフォレストの1つがダウンした場合、AD FS は、構成されている他のフォレストの代替ログイン ID を持つユーザーアカウントを検索し続けます。 検索したフォレスト全体で一意のユーザーオブジェクトが検出されると、ユーザーは正常にログインします。 AD FS

-   また、AD FS サインインページをカスタマイズして、代替ログイン ID に関するヒントをエンドユーザーに与えることもできます。 これを行うには、カスタマイズされたサインインページの説明を追加します (詳細については、「ユーザー名フィールドの[AD FS サインインページのカスタマイズ](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280950(v=ws.11))」または「組織アカウントでのサインイン」を参照してください。詳細については、「 [AD FS サインインページの高度なカスタマイズ](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn636121(v=ws.11))」を参照してください。

-   代替ログイン ID の値を含む新しい要求の種類は**http: schema. microsoft .com/ws/2013/11/alternateloginid です。**

## <a name="events-and-performance-counters"></a>イベントおよびパフォーマンス カウンター
代替ログイン ID が有効になっている場合、AD FS サーバーのパフォーマンスを測定するために、次のパフォーマンスカウンターが追加されました。

-   代替ログイン Id 認証: 代替ログイン ID を使用して実行された認証数

-   代替ログイン Id 認証数/秒: 代替ログイン ID を使用して実行された認証の1秒あたりの数

-   代替ログイン ID の平均検索待機時間: 管理者によって代替ログイン ID が構成されているフォレスト全体の検索の平均待機時間

次に、AD FS によってログに記録されたイベントを使用したユーザーのサインインエクスペリエンスに対するさまざまなエラーケースとそれに対する影響を示します。



|                       **エラーケース**                        | **サインインエクスペリエンスへの影響** |                                                              **Event**                                                              |
|--------------------------------------------------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| ユーザーオブジェクトの SAMAccountName の値を取得できません |          ログインエラー           |                  イベント ID 364、例外メッセージ MSIS8012: ユーザーの samAccountName が見つかりません: ' {0} '。                   |
|        CanonicalName 属性にアクセスできません         |          ログインエラー           |               イベント ID 364 (例外メッセージ MSIS8013: CanonicalName: ' {0} '、ユーザー: ' ') の {1} 形式が正しくありません。                |
|        1つのフォレストに複数のユーザーオブジェクトが見つかりました        |          ログインエラー           | イベント ID 364、例外メッセージ MSIS8015: フォレスト ' ' の id ' ' を持つ複数のユーザーアカウントが id で見つかりました {0} {1} :{2} |
|   複数のユーザーオブジェクトが複数のフォレストにわたって検出される    |          ログインエラー           |           イベント ID 364、例外メッセージ MSIS8014: フォレストに id ' ' を持つ複数のユーザーアカウントが見つかりました {0} :{1}            |

## <a name="see-also"></a>参照
[AD FS の運用](../ad-fs-operations.md)
