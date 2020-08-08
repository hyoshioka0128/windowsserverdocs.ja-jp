---
title: AD FS のトラブルシューティング-Azure AD
description: このドキュメントでは、AD FS と Azure AD のさまざまな側面をトラブルシューティングする方法について説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.openlocfilehash: d7941733ff2191e94c6c1e380d4349585a5c98d3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956179"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS のトラブルシューティング-Azure AD
クラウドの成長に伴って、多くの企業がさまざまなアプリやサービスのために Azure AD を使用するように移行してきました。  Azure AD とのフェデレーションは、多くの組織にとって標準的な手法になりました。  このドキュメントでは、このフェデレーションで発生する問題のトラブルシューティングに関するいくつかの側面について説明します。  一般的なトラブルシューティングドキュメントに記載されているいくつかのトピックは、引き続き Azure とのフェデレーションに関連しているため、このドキュメントでは Azure AD と AD FS の対話に関する詳細のみに焦点を当てています。

## <a name="redirection-to-ad-fs"></a>AD FS へのリダイレクト

リダイレクトは、Office 365 などのアプリケーションにサインインし、組織 AD FS サーバーに "リダイレクト" してサインインすると発生します。

![AD FS へのリダイレクト画面](media/ad-fs-tshoot-azure/azure1.png)

### <a name="first-things-to-check"></a>最初にチェックする項目

リダイレクトが発生していない場合は、いくつかのことを確認する必要があります。

1. Azure portal にサインインし、[Azure AD Connect] をオンにして、Azure AD テナントがフェデレーションに対して有効になっていることを確認します。

   ![Azure AD Connect のユーザーサインイン画面](media/ad-fs-tshoot-azure/azure2.png)

2. Azure portal の [フェデレーション] の横にあるドメインをクリックして、カスタムドメインが検証されていることを確認します。

   ![ポータルでフェデレーションの横に表示されるドメイン](media/ad-fs-tshoot-azure/azure3.png)

3. 最後に、 [DNS](ad-fs-tshoot-dns.md)を確認し、AD FS サーバーまたは WAP サーバーがインターネットから解決していることを確認します。  これが解決されていることを確認し、それに移動できることを確認します。

4. PowerShell コマンドレットを使用して `Get-AzureADDomain` この情報を取得することもできます。

   ![PowerShell コマンドレット画面](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>不明な認証方法のエラーを受信しています
Azure からリダイレクトされた場合、AD FS または STS レベルで AuthnContext がサポートされていないことを示す "不明な認証方法" エラーが発生することがあります。

これは、認証方法を適用するパラメーターを使用して Azure AD が AD FS または STS にリダイレクトされる場合に最も一般的です。

認証方法を適用するには、次のいずれかの方法を使用します。
- WS-FEDERATION の場合は、WAUTH クエリ文字列を使用して、優先認証方法を強制します。

- SAML 2.0 の場合は、次のようにします。
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  強制認証方法が正しくない値で送信された場合、または AD FS または STS で認証方法がサポートされていない場合は、認証される前にエラーメッセージが表示されます。

|必要な認証方法|wauth URI|
|-----|-----|
|ユーザー名とパスワードの認証|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL クライアント認証|urn: ietf: rfc: 2246|
|Windows 統合認証|urn: フェデレーション: 認証: windows|

サポートされている SAML 認証コンテキストクラス

|認証方法|認証コンテキストクラスの URI|
|-----|-----|
|ユーザー名とパスワード|urn:oasis:names:tc:SAML:2.0:ac:classes:Password|
|パスワードで保護されたトランスポート|urn: oasis: names: tc: SAML: 2.0: ac: classes: PasswordProtectedTransport|
|TLS (Transport Layer Security) クライアント|urn: oasis: names: tc: SAML: 2.0: ac: classes: TLSClient
|X.509 証明書|urn: oasis: names: tc: SAML: 2.0: ac: classes: X509
|統合 Windows 認証|urn: フェデレーション: 認証: windows|
|Kerberos|urn: oasis: names: tc: SAML: 2.0: ac: classes: Kerberos|

認証方法が AD FS レベルでサポートされていることを確認するには、次のことを確認してください。

#### <a name="ad-fs-20"></a>AD FS 2.0

[ **/Adfs/ls/web.config**で、認証の種類のエントリが存在することを確認します。

```
<microsoft.identityServer.web>
<localAuthenticationTypes>
<add name="Forms" page="FormsSignIn.aspx" />
<add name="Integrated" page="auth/integrated/" />
<add name="TlsClient" page="auth/sslclient/" />
<add name="Basic" page="auth/basic/" />
</localAuthenticationTypes>
```

#### <a name="ad-fs-2012-r2"></a>AD FS 2012 R2

[ **AD FS の管理**] で、AD FS スナップインの [**認証ポリシー** ] をクリックします。

[**プライマリ認証**] セクションで、[グローバル設定] の横にある [編集] をクリックします。 [認証ポリシー] を右クリックし、[グローバルプライマリ認証の編集] を選択することもできます。 または、[操作] ウィンドウで [グローバルプライマリ認証の編集] を選択します。

[グローバル認証ポリシーの編集] ウィンドウの [プライマリ] タブで、グローバル認証ポリシーの一部として設定を構成できます。 たとえば、プライマリ認証の場合は、[エクストラネットとイントラネット] で利用可能な認証方法を選択できます。

* * [必要な認証方法] チェックボックスがオンになっていることを確認します。

#### <a name="ad-fs-2016"></a>AD FS 2016

[ **AD FS 管理**] で、AD FS スナップインの [**サービス**と**認証方法**] をクリックします。

[**プライマリ認証**] セクションで、[編集] をクリックします。

[**認証方法の編集**] ウィンドウの [プライマリ] タブで、認証ポリシーの一部として設定を構成できます。

![[認証方法の編集] ウィンドウ](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>AD FS によって発行されたトークン

### <a name="azure-ad-throws-error-after-token-issuance"></a>トークンの発行後に Azure AD がエラーをスローする
AD FS によってトークンが発行されると、Azure AD によってエラーがスローされることがあります。 このような状況では、次の問題がないかどうかを確認します。
- トークン内の AD FS によって発行される要求は、Azure AD 内のユーザーの各属性と一致する必要があります。
- Azure AD のトークンには、次の必要な要求が含まれている必要があります。
    - WSFED
        - UPN: この要求の値は Azure AD のユーザーの UPN と一致している必要があります。
        - ImmutableID: この要求の値は、Azure AD のユーザーの sourceAnchor または ImmutableID と一致している必要があります。

Azure AD でユーザー属性値を取得するには、次のコマンドラインを実行します。`Get-AzureADUser –UserPrincipalName <UPN>`

![PowerShell コマンドレット画面](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2.0:
       - IDPEmail: この要求の値は Azure AD のユーザーのユーザープリンシパル名と一致している必要があります。
       - NAMEID: この要求の値は、Azure AD のユーザーの sourceAnchor または ImmutableID と一致している必要があります。

詳細については、「 [SAML 2.0 id プロバイダーを使用したシングルサインオンの実装](/previous-versions/azure/azure-services/dn641269(v=azure.100))」を参照してください。

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>AD FS と Azure AD のトークン署名証明書が一致していません。

AD FS は、トークン署名証明書を使用して、ユーザーまたはアプリケーションに送信されるトークンに署名します。 AD FS と Azure AD 間の信頼は、このトークン署名証明書に基づくフェデレーション信頼です。

ただし、証明書の自動ロールオーバーまたは何らかの介入によって AD FS 側のトークン署名証明書が変更された場合は、フェデレーションドメインの Azure AD 側で新しい証明書の詳細を更新する必要があります。 AD FS のプライマリトークン署名証明書が Azure Ad と異なる場合、AD FS によって発行されたトークンは Azure AD によって信頼されていません。 そのため、フェデレーションユーザーはログオンを許可されていません。

この問題を解決するには、「 [Office 365 用フェデレーション証明書の更新](/azure/active-directory/connect/active-directory-aadconnect-o365-certs)」の手順のアウトラインを使用して Azure Active Directory します。

## <a name="other-common-things-to-check"></a>その他の一般的なチェック事項
AD FS と Azure AD の相互作用に関する問題があるかどうかを確認するための簡単な一覧を次に示します。
- Windows Credential Manager での古いまたはキャッシュされた資格情報
- Office 365 の証明書利用者信頼で構成されているセキュリティで保護されたハッシュアルゴリズムが SHA1 に設定されている

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
