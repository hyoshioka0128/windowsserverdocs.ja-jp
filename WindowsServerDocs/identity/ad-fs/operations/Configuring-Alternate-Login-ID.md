---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: "代替ログイン ID を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/04/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb4c98ff1090a9d3c35654614a43e12db99d691d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-alternate-login-id"></a>代替ログイン ID を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

ユーザーは、Active Directory ドメイン サービス (AD DS) によって承認されたユーザーの識別子を使用した Active Directory フェデレーション サービス (AD FS) 有効になっているアプリケーションにサインインできます。 ユーザー プリンシパル名 (Upn) が含まれます (johndoe@contoso.com) またはドメイン (contoso\johndoe または contoso.com\johndoe) の sam アカウント名を修飾します。

企業のポリシーまたは社内基幹業務アプリケーションの依存関係のため、一部の環境でエンドユーザーの電子メール アドレス、UPN またはではなく sam アカウント名の対応のみ場合があります。 場合によっては、UPN がルーティング不可能なも (jdoe@contoso.local) と、企業ネットワーク上のアプリケーションへの認証にのみ使用します。

ルーティング不可能なドメインの (例: 以降 Contoso.local) の所有権を検証することはできません、Office 365 が Id にルーティング可能なインターネットを完全にすべてのユーザー ログインが必要です。 内部設置型の UPN はルーティング不可能なドメイン (例: を使用している場合 Contoso.local)、またはローカルのアプリケーションの依存関係のため、既存の UPN を変更することはできません、代替ログイン ID の設定をお勧め 代替ログイン ID を構成できます、サインイン エクスペリエンスでメールなど、UPN 以外属性を使用してサインインできるユーザー。

この機能の利点の 1 つは、内部設置型の Upn を変更することがなく、Office 365 などの SaaS プロバイダーの導入できること。 コンシューマー向けプロビジョニングされた id を持つサービスの基幹業務アプリケーションをサポートすることもできます。

> [!IMPORTANT]
> ビジネス向けの Exchange や Skype ハイブリッド環境で別の ID を使用してはサポートしますが、推奨されません。 オンプレミスおよびオンライン (例: UPN) の資格情報の同じ設定を使用するハイブリッド環境での最適なユーザー エクスペリエンスを提供します。  お客様は、代替 ID の必要がなくなります可能であれば、Upn を変更をお勧めします。 Lync または Skype for business の別の ID を使って、Lync Server 2013 以降が必要です。 別の ID を使用しているお客様が有効化を検討する必要があります[最新の認証](https://support.office.com/article/using-office-365-modern-authentication-with-office-clients-776c0036-66fd-41cb-8928-5495c0f9168a)、ユーザー エクスペリエンスの向上の Office 365 に Exchange 用です。 さらに、ビジネス向けモバイル クライアントで Skype を使用しているお客様は、SIP アドレスがユーザーのメール アドレス (と代替の ID) と同じであることを確認する必要があります。 

標準の認証、最新の認証と証明書ベースの認証 (最新の認証を有効にする必要があります) にさまざまな Office 365 のクライアントを使用して代替の ID を持つユーザー エクスペリエンスは、次の表を参照してください。

|**クライアントの種類**|**追加情報**|**サポートに関する声明 - 通常と最新の認証**|**説明**|
|--------------------|------------------------------|------------------------------|------------------------------|
|Outlook|標準の認証: ドメインに参加しているコンピューターである必要がありますして企業ネットワークに接続されています。<br /><br />最新の認証: サポートされています。|別の ID は、ユーザーのメールボックスの外部からのアクセスを許可しない環境でのみ使用できます。 これは、ユーザー認証がメールボックスにサポートされている方法で接続されていると、VPN 上、企業ネットワークに参加しているまたはへの直接アクセス経由で接続されたときに意味します。 最新の認証 (ADAL と呼ばれます) を構成することを選択する場合は、非ドメインに参加している接続し、マシンから Outlook を使用することができますの Outlook プロファイルを構成するときに、いくつかの余分なプロンプトが表示されます。<br /><br />ユーザー エクスペリエンスのデモについては、表の下の最初のイメージを参照してください。|[Office 2013 で最新の認証](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|ハイブリッドのパブリック フォルダ|定期的な認証: サポートされていません<br /><br />最新の認証: サポートされています。|ハイブリッドのパブリック フォルダでは、代替の ID を使用し、したがって使用しないで今日標準の認証方法の場合を展開できません。 ハイブリッドのパブリック フォルダーを使用する場合は、最新の認証 (ADAL と呼ばれます) を構成する必要があります。<br /><br />ユーザー エクスペリエンスのデモについては、表の下の最初のイメージを参照してください。|[Office 2013 で最新の認証](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|クロス内部設置型の委任|サポートされていません|現在間の内部設置型のアクセス許可は、ハイブリッド構成でサポートされていませんが、または動作しません AltID を使用する場合。||
|アーカイブのメールボックスへのアクセス (メールボックス、オンプレミス、クラウドでアーカイブ)|サポートされています。|ユーザー、アーカイブにアクセスするときに資格情報の追加のプロンプトが表示されます、提供する必要がある別の ID が表示されたらします。<br /><br />ユーザー エクスペリエンスのデモについては、表の下の最初のイメージを参照してください。||
|Office 365 Pro Plus のライセンス認証] ページ|クライアント側のレジストリ キーの推奨 - サポートされています。|代替 ID の構成と検証] フィールドに、社内の UPN があらかじめ設定されているが表示されます。 これは、使用されている別の Id に変更する必要があります。 [リンク] 列に記載されているクライアント側のレジストリ キーを使用することをお勧めします。<br /><br />ユーザー エクスペリエンスのデモについては、表の下 2 番目のイメージを参照してください。|[Office 2013 と SharePoint Online、OneDrive、および Lync Online 資格情報の入力を求める定期的に Lync 2013](https://support.microsoft.com/en-us/kb/2913639)|
|Microsoft Teams|サポートされています。|Microsoft Teams supports AD FS (SAML-P, WS-Fed, WS-Trust, and OAuth) and Modern Authentication.<br/><br/> Core Microsoft Teams such as Channels, chats and files functionalities does work with Altnernate Login ID. </br></br>1st and 3rd party apps have to be separately investigated  by the customer. This is because each application has their own supportability authentication protocols.| 
|Skype for Business または Lync|サポートされている (一部の例外を除き) が、ユーザーが混乱が発生する可能性があります。  モバイル クライアントは、別の Id がサポートされている場合にのみ SIP アドレスの電子メール アドレスを = = 代替 id。|ユーザーがサインインするには 2 回クリック、Skype for Business デスクトップ クライアント、まず、社内の UPN を使用し、代替の id。 を使用する必要があります。 (「サインイン アドレス」が実際には、SIP アドレスできない可能性があります「ユーザー名」と同じ、多くの場合は注意してください。)  最初のユーザー名の入力を求め、ユーザーが正しくあらかじめ入力されていない別の ID または SIP のアドレスを持つ場合でも、UPN を入力する必要があります。 ユーザーから、UPN、名前プロンプトが再び表示ユーザー、UPN を持つあらかじめ設定されているこの時点でのサインインをクリックします。 この時間をユーザーが代替 ID に置き換えますこれと] をクリックする必要がありますが、サインイン プロセスを完了するサインインします。 モバイル クライアントでユーザー必要があります、内部設置型ユーザー ID を入力、[詳細設定] ページで、SAM スタイルの形式 (ドメイン \ ユーザー名)、UPN 形式ではなくを使用します。<br /><br />正常では、サインイン後に Skype for Business または Lync では、「Exchange、必要がある資格情報」と表示場合、メールボックスが置かれている有効な資格情報を提供します。 メールボックスが、クラウド内にある場合は、代替の id。 提供する必要があります。 メールボックスが内部設置型の場合は、内部設置型の UPN を提供する必要があります。|[Office 2013 で最新の認証](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|Outlook Web Access|サポートされています。|||
|Android、IOS、および Windows Phone 用のモバイル アプリの outlook|サポートされています。|||
|OneDrive for Business|クライアント側のレジストリ キーの推奨 - サポートされています。|代替 ID の構成と検証] フィールドに、社内の UPN があらかじめ設定されているが表示されます。 これは、使用されている別の Id に変更する必要があります。 [リンク] 列に記載されているクライアント側のレジストリ キーを使用することをお勧めします。<br /><br />ユーザー エクスペリエンスのデモについては、表の下 2 番目のイメージを参照してください。|[Office 2013 と SharePoint Online、OneDrive、および Lync Online 資格情報の入力を求める定期的に Lync 2013](https://support.microsoft.com/en-us/kb/2913639)|
|OneDrive for Business モバイル クライアント|サポートされています。|||

![代替ログイン](media/Configure-Alternate-Login-ID/ADFS_Alt_ID1.png)

![代替ログイン](media/Configure-Alternate-Login-ID/ADFS_Alt_ID2.png)

![代替ログイン](media/Configure-Alternate-Login-ID/ADFS_Alt_ID3.png)

、次は、次のスクリーン ショットは、その他の使用例を Skype for Business を示します。  例では、次の情報を使用します。


- SIP:userA@contoso.com 
- UPN:userA@contoso.local
- 電子メール：userA@contoso.com
- AltId:userA@contoso.com 

[Sign in] フィールドには、SIP のアドレスを入力します。

![Skype](media/Configure-Alternate-Login-ID/SkypeA.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeB.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeC.png)

## <a name="to-configure-alternate-login-id"></a>代替ログイン ID を構成するには
代替ログイン ID を構成するために、次のタスクを実行する必要があります。

代替ログイン ID を有効にするには、AD FS 要求プロバイダー信頼を構成します。

1.  Install [KB2919355](https://go.microsoft.com/fwlink/?LinkID=396590).  Windows Update サービス経由で取得したり、直接ダウンロードできます。

2.  ファームにフェデレーション サーバーのいずれかで、次の PowerShell コマンドレットを実行して、AD FS 構成を更新 (WID ファームの場合は、必要がありますコマンドを実行するこのファーム内のプライマリ AD FS サーバー)。

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>

    ```

    **AlternateLoginID**ログインに使用する属性の LDAP 名です。

    **LookupForests** DNS には、ユーザーに属しているフォレストの一覧を示します。

    代替ログイン ID の機能を有効にするには、null 以外の有効な値を持つ - AlternateLoginID と - LookupForests の両方のパラメーターを構成する必要があります。

    次の例では、contoso.com と fabrikam.com のフォレスト内のアカウントに、ユーザーが"mail"属性を持つ AD FS 対応アプリケーションにログインできるように、代替ログイン ID の機能を有効にします。

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
    ```

3.  この機能を無効にするには、両方のパラメーターに null 値を設定します。

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
    ```

4.  Azure AD と代替ログイン ID を有効にするには、追加の構成手順は必要ありません Azure AD Connect を使用する場合。   代替の ID は、ウィザードから直接構成することができます。  セクションの下で、ユーザーを一意に識別するを参照してください。[を Azure AD Connect](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-get-started-custom/#connect-to-azure-ad)します。

## <a name="additional-details--considerations"></a>追加の詳細と考慮事項

-   展開されている AD FS では、代替ログイン ID の機能をフェデレーション環境で使用できるのみです。  次のシナリオではサポートされません。
    -   非ルーティング可能なドメイン (例: Contoso.local) を Azure AD で検証することはできません。
    -   AD FS の展開がない環境を管理します。


-   有効な場合、代替ログイン ID 機能のみで使用可能なユーザー名とパスワードの認証のすべてのユーザー名/パスワードの認証プロトコル AD FS でサポートされている (SAML P、WS-が取り込まれる、Ws-trust、や OAuth)。


-   Windows 統合認証 (WIA) が実行されると (たとえば、ときにユーザーがイントラネットからドメインに参加しているコンピューター上の企業アプリケーションにアクセスしようし、AD FS 管理者には、イントラネットに WIA を使用する認証ポリシーが構成されている)、UPN が認証に使用されます。 代替ログイン ID の機能の証明書利用者の要求規則を構成した場合はそれらの規則が WIA 場合は、まだ有効であることを確認する必要があります。

-   有効な場合、代替ログイン ID 機能には、AD FS をサポートする各ユーザー アカウントのフォレストの AD FS サーバーから到達可能にするには、少なくとも 1 つのグローバル カタログ サーバーが必要です。 AD FS UPN を使用するようにフォールバック ユーザー アカウントのフォレストにグローバル カタログ サーバーに到達する障害が発生します。 既定では、すべてのドメイン コント ローラーはグローバル カタログ サーバーをされます。

-   有効な場合、AD FS サーバーと同じ代替ログイン ID 値に設定されたユーザー アカウントのすべてのフォレスト間で指定されている 1 つ以上のユーザー オブジェクトが検出された場合は、ログインは失敗します。

-   AD FS を最初に代替ログイン ID を持つエンドユーザーを認証し、代替ログイン ID によって識別できるアカウントが見つからない場合は、UPN を使用するフォールバックを試みます代替ログイン ID の機能を有効にすると、 まだ UPN ログインをサポートする場合、代替ログイン ID と UPN の間の競合がないことを確認する必要があります。 たとえば、1 つのメールの属性を設定、その他の UPN を持つ、UPN サインインから他のユーザーがブロックされます。

-   管理者が構成されているフォレストのいずれかが停止して、AD FS は引き続き構成されている他のフォレスト内の代替ログイン ID を持つユーザー アカウントを検索します。 AD FS サーバーが検出された場合、一意のユーザー オブジェクトの検索が、フォレスト間で、ユーザーは正常ログオンします。

-   代替ログイン ID に関するいくつかのヒントをエンド ユーザーに提供する AD FS サインイン ページをカスタマイズすることもまた カスタマイズされたサインイン ページの説明を追加して行うことができます (詳細については、次を参照してください。 [AD FS サインイン ページのカスタマイズ](https://technet.microsoft.com/library/dn280950.aspx)またはユーザー名] フィールドの上に"組織のアカウントでサインイン"文字列をカスタマイズする (詳細については、次を参照してください。 [Advanced Customization of AD FS Sign-in Pages](https://technet.microsoft.com/library/dn636121.aspx)します。

-   代替ログイン ID の値を含む新しい要求の種類が**http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>イベントとパフォーマンス カウンター
代替ログイン ID が有効にすると、AD FS サーバーのパフォーマンスを測定する次のパフォーマンス カウンターが追加されました。

-   代替ログイン ID を使用して実行する認証の代替ログイン Id の認証: 数

-   1 秒あたりの代替ログイン ID を使用して実行する認証の数を代替ログイン Id 認証/秒の:

-   代替ログイン ID の検索の待機時間の平均: 管理者が代替ログイン ID の構成のフォレスト間での検索の待機時間の平均

さまざまなエラーの場合と対応する AD FS によって記録されたイベントとユーザーのサインイン エクスペリエンスへの影響を次に示します。



**エラーの場合**|**サインイン エクスペリエンスへの影響**|**イベント**|
---------|---------|---------
ユーザー オブジェクトの SAMAccountName の値を取得できません。|ログインに失敗しました|例外メッセージ MSIS8012 にイベント ID 364: ユーザーの sam アカウント名が見つかりません: '{0}' です。|
用の属性にアクセスできません。|ログインに失敗しました|例外メッセージ MSIS8013 にイベント ID 364: 用: ユーザーの '{0} ':' {1}' は無効な形式でします。|
1 つのフォレストに複数のユーザー オブジェクトがあります。|ログインに失敗しました|例外メッセージ MSIS8015 にイベント ID 364: '{0}' id を持つ複数のユーザー アカウントに記載の id を持つ '{1}' フォレスト: {2}|
複数のユーザー オブジェクトが複数のフォレストが見つかりません|ログインに失敗しました|例外メッセージ MSIS8014 にイベント ID 364: '{0}' id を持つ複数のユーザー アカウントをフォレストで見つかった: {1}|

## <a name="see-also"></a>参照してください。
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)


