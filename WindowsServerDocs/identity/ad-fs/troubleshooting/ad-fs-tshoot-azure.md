---
title: AD FS のトラブルシューティング - Azure AD
description: このドキュメントは、AD FS と Azure AD のさまざまな側面をトラブルシューティングする方法を説明します
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 228ef34ab25276c1cf98f9b2b64e997390023c87
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444012"
---
# <a name="ad-fs-troubleshooting---azure-ad"></a>AD FS のトラブルシューティング - Azure AD
クラウドの増加、多くの企業が Azure AD のさまざまなアプリやサービスを使用する外してきました。  Azure AD とのフェデレーションと、多くの組織の標準的な手法になっています。  このドキュメントは、このフェデレーションで発生する問題のトラブルシューティングの側面のいくつかについて説明します。  このドキュメントは単なる仕様と Azure AD にフォーカスすることが Azure とのフェデレーションに関するいくつかの一般的なトラブルシューティング ドキュメントのトピックと AD FS の相互作用します。

## <a name="redirection-to-ad-fs"></a>AD FS へのリダイレクト
リダイレクトと発生しますサインインで Office 365 などのアプリケーションに「リダイレクトされます」に、組織のサインインに AD FS サーバー。

![](media/ad-fs-tshoot-azure/azure1.png)


### <a name="first-things-to-check"></a>最初に行うことを確認するには
リダイレクトが行われていないいくつかの点がある場合は、確認します。

   1. Azure portal にサインインし、Azure AD Connect の下のチェックで、フェデレーション用に、Azure AD テナントが有効になっていることを確認します。

![](media/ad-fs-tshoot-azure/azure2.png)

1. Azure portal でのフェデレーションの横にあるドメインをクリックして、カスタム ドメインを確認することを確認します。
   ![](media/ad-fs-tshoot-azure/azure3.png)

2. 最後に、確認したい[DNS](ad-fs-tshoot-dns.md)し、AD FS サーバーまたは WAP サーバーがインターネットから解決することを確認します。  これが解決されると、それに移動できることを確認します。
3. PowerShell コマンドレットを使用することもできます。`Get-AzureADDomain`もこの情報を取得します。

![](media/ad-fs-tshoot-azure/azure6.png)

### <a name="you-are-receiving-an-unknown-auth-method-error"></a>不明な認証メソッドのエラーを受信しています。
Azure からリダイレクトされる、AuthnContext が AD FS または STS のレベルでサポートされないことを示す「不明な認証方法」エラーが発生する可能性があります。 

これは、Azure AD が認証方法を強制するパラメーターを使用して、AD FS または STS にリダイレクトするときに最も一般的です。 

認証方法を適用するには、次のメソッドのいずれかを使用します。
- 、Ws-federation の WAUTH クエリ文字列を使用して、強制的に推奨される認証方法。

- SAML2.0 の次の手順に従います。
  ```
  <saml:AuthnContext>
  <saml:AuthnContextClassRef>
  urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
  </saml:AuthnContextClassRef>
  </saml:AuthnContext>
  ```
  適用される認証方法が正しくない値では、送信されたときに、または AD FS または STS でその認証方法がサポートされていない場合は、認証を行う前にエラー メッセージが表示されます。

|必要な認証方法|wauth URI|
|-----|-----|
|ユーザー名とパスワードの認証|urn:oasis:names:tc:SAML:1.0:am:password|
|SSL クライアント認証|urn:ietf:rfc:2246|
|Windows 統合認証|urn:federation:authentication:windows|

サポートされている SAML 認証コンテキスト クラス

|認証方法|認証コンテキスト クラスの URI|
|-----|-----| 
|ユーザー名とパスワード|urn: oasis: 名前: tc: SAML:2.0:ac:classes:Password|
|パスワードで保護されたトランスポート|urn: oasis: 名前: tc: SAML:2.0:ac:classes:PasswordProtectedTransport|
|トランスポート層セキュリティ (TLS) クライアント|urn:oasis:names:tc:SAML:2.0:ac:classes:TLSClient
|X.509 証明書|urn: oasis: 名前: tc: SAML:2.0:ac:classes:X 509
|統合 Windows 認証|urn:federation:authentication:windows|
|Kerberos|urn:oasis:names:tc:SAML:2.0:ac:classes:Kerberos|

認証方法が AD FS レベルでサポートされていることを確認するには、次の手順を確認します。

#### <a name="ad-fs-20"></a>AD FS 2.0 

**/Adfs/ls/web.config**認証の種類のエントリが存在するかどうかを確認します。

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

[ **AD FS 管理**、] をクリックして**認証ポリシー**スナップインで、AD FS します。

**プライマリ認証**セクションで、グローバル設定 の横の編集 をクリックします。 認証ポリシーを右クリックし、グローバル プライマリ認証の編集を選択できます。 または、[操作] ウィンドウで、グローバル プライマリ認証の編集を選択します。

プライマリ タブで、グローバル認証ポリシーの編集 ウィンドウで、グローバル認証ポリシーの一部として設定を構成できます。 たとえば、プライマリ認証の場合、エクストラネットおよびイントラネットで使用できる認証方法を選択できます。

* * こと、必要な認証方式 チェック ボックスが選択されていることを確認します。 

#### <a name="ad-fs-2016"></a>AD FS 2016

[ **AD FS 管理**、] をクリックして**サービス**と**認証方法**スナップインで、AD FS します。

**プライマリ認証**セクションで、[編集] をクリックします。

**認証方法の編集**ウィンドウで、[プライマリ] タブで、認証ポリシーの一部として設定を構成することができます。

![](media/ad-fs-tshoot-azure/azure4.png)

## <a name="tokens-issued-by-ad-fs"></a>AD FS によって発行されたトークン

### <a name="azure-ad-throws-error-after-token-issuance"></a>Azure AD トークン発行後にエラーがスローされます。
AD FS トークンを発行した後は、Azure AD がエラーをスローします。 このような状況では、次の問題を確認します。
- トークン内の AD FS によって発行される要求は、Azure AD でユーザーのそれぞれの属性を一致させてください。
- Azure AD のトークンには、次の必要なクレームが含まれます。
    - : WSFED 
        - UPN:この要求の値は、Azure AD でのユーザーの UPN を一致する必要があります。
        - ImmutableID:この要求の値は、Azure AD で sourceAnchor またはユーザーの ImmutableID を一致する必要があります。

Azure AD でユーザー属性の値を取得するには、次のコマンドラインを実行します。 `Get-AzureADUser –UserPrincipalName <UPN>`

![](media/ad-fs-tshoot-azure/azure5.png)

   - SAML 2.0:
       - IDPEmail:この要求の値は、Azure AD でのユーザーのユーザー プリンシパル名を一致する必要があります。
       - NAMEID:この要求の値は、Azure AD で sourceAnchor またはユーザーの ImmutableID を一致する必要があります。

詳細については、次を参照してください。 [、SAML 2.0 id プロバイダーを使用して、シングル サインオンを実装する](https://technet.microsoft.com/library/dn641269.aspx)します。

### <a name="token-signing-certificate-mismatch-between-ad-fs-and-azure-ad"></a>トークン署名証明書の不一致 AD FS と Azure AD の間。

AD FS では、トークン署名証明書を使用して、ユーザーまたはアプリケーションに送信されるトークンに署名します。 AD FS と Azure AD の間の信頼では、このトークン署名証明書に基づくフェデレーションによる信頼です。

ただし、自動証明書のロール オーバーのため、または何らかの介入によって AD FS にある トークン署名証明書を変更する場合、新しい証明書の詳細は、フェデレーション ドメインの Azure AD 側で更新する必要があります。 AD FS のプライマリ トークン署名証明書が Azure Ad と異なる場合は、AD FS によって発行されるトークンは Azure AD によって信頼されていません。 そのため、フェデレーション ユーザーは、ログオンは許可されません。

使用することがこれを解決する手順の説明で[Office 365 と Azure Active Directory のフェデレーション証明書を書き換える](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)します。

## <a name="other-common-things-to-check"></a>その他の一般的なチェック事項
次は AD FS と Azure AD との対話によって問題が発生したかどうかを確認する項目の簡単な一覧です。
- 古いまたはキャッシュされた資格情報では、Windows 資格情報マネージャー
- Office 365 の Relying Party Trust で構成されているセキュリティで保護されたハッシュ アルゴリズムが SHA1 に設定されています。

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)