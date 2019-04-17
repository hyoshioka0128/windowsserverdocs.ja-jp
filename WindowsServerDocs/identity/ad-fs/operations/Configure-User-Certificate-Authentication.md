---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: "ユーザー証明書認証のサポートを AD FS を構成します。"
description: 
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.service: active-directory
ms.technology: identity-adfs
ms.openlocfilehash: 9941d4dd997e857874aceddc920ec7f9d8944a81
ms.sourcegitcommit: d351cdbb0bf2533d6db35626ebbc4924b3834309
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2018
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>AD FS ユーザー証明書認証の構成

>適用対象: Windows Server 2016、Windows Server 2012 R2

X509 ユーザー証明書の認証を使用して、モードのいずれかに記載の AD FS を構成することができます[この記事](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)します。 この機能を使用する[と Azure Active Directory](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)独自に、クライアントとデバイスを有効にするがプロビジョニングされて AD FS のアクセスをユーザーの証明書、イントラネットまたはエクストラネットからリソースです。

## <a name="prerequisites"></a>前提条件
- ユーザー証明書がすべての AD FS と WAP サーバーによって信頼されていることを確認します。
- Active Directory 内の NTAuth ストアでのユーザー証明書信頼チェーンのルート証明書があることを確認します。
- AD FS と WAP サーバーは、たとえば"certauth.fs.contoso.com"と、"certauth"で始まる AD FS ホスト名が含まれている SSL 証明書であることを確認し、ファイアウォールをこのホスト名にそのトラフィックが許可されている場合、代替の証明書の認証モードでは、AD FS を使用して、
- エクストラネットから証明書認証を使用する場合は、少なくとも 1 つの AIA と証明書で指定されている一覧から 1 つ以上の CDP または OCSP の場所が、インターネットからアクセス可能であることを確認します。
- Azure AD の証明書認証用の AD FS を構成している場合は、構成していることを確認、 [Azure AD の設定](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)と[AD FS 要求のために必要なルール](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements)証明書の発行者とシリアル番号
- Exchange ActiveSync クライアントの場合、Azure AD の証明書認証用クライアント証明書が必要、ユーザーにルーティング可能なメール アドレス Exchange オンライン プリンシパル名またはサブジェクトの別名] フィールドの rfc 822 名前値のいずれかでです。 (Azure Active Directory にマップする rfc 822 値ディレクトリにプロキシ アドレスの属性です。)

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>ユーザー証明書認証用の AD FS を構成します。  
- イントラネットまたは AD FS 管理コンソールまたはセット AdfsGlobalAuthenticationPolicy PowerShell コマンドレットを使用して、AD FS のエクストラネット認証方法としてユーザー証明書認証を有効にします。
- すべての AD FS と WAP サーバーで、中間証明書を含む、信頼チェーン全体がインストールされていることを確認します。 中間証明書は、すべての AD FS と WAP サーバー上でローカル コンピューターの中間証明機関ストアにインストールする必要があります。
- If you wish to use claims based on certificate fields and extensions in addition to EKU (claim type https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku), configure additional claim pass through rules on the Active Directory claims provider trust.  利用可能な証明書の信頼性情報の完全な一覧については、以下をご覧ください。  
- [オプション]"クライアント認証用の信頼された発行者の管理] の下のガイダンスを使用してクライアント証明書の発行元証明機関を許可されている構成[この記事](https://technet.microsoft.com/en-us/library/dn786429(v=ws.11).aspx)します。

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Chrome ブラウザー Windows デスクトップでのシームレスな証明書の認証を構成します。
(証明書の Wi ‑ Fi) などの複数のユーザー証明書がクライアント認証の目的を満たしているコンピューターに存在する場合、Windows デスクトップで Chrome ブラウザーは、ユーザーを適切な証明書の選択を求められます。 これは、エンド ユーザーが混乱可能性があります。 このエクスペリエンスを最適化するには、Chrome より良いユーザー エクスペリエンスのための適切な証明書を自動選択するためのポリシーを設定することができます。 このポリシーは、レジストリの変更を加えるを手動で設定または GPO (レジストリ キーを設定) を使用して自動的に構成できます。 これには、個別の発行者他のユース ケースからに AD FS に対して認証のため、ユーザー クライアント証明書が必要です。 

Chrome に対するこの構成に関する詳細については、これを参照してください[リンク](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)します。  


## <a name="troubleshooting"></a>トラブルシューティング
- 証明書の認証要求は HTTP 204「https://certauth.fs.contoso.com から不要コンテンツ」応答に失敗した場合、ルートおよび中間 CA 証明書がインストールされている、それぞれを確認する、すべてのフェデレーション サーバー上のストアの証明書には、信頼されたルート CA と中間 CA です。
- 不明な理由により証明書の認証要求が失敗する場合、.cer ファイルに、クライアント証明書をエクスポートし、コマンドを実行 

`certutil -f -urlfetch -verify certificatefilename.cer`

すべての CRL および delta CRL の場所の解決を確認します。  Base CRL の内容に基づく delta CRL の場所を検出することに注意してください。

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>参照: ユーザー証明書の完全なリストの要求の種類と値の例

|要求の種類|値の例
|-----|-----
|https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version | 3
|https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm | sha256RSA
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer | CN = entca、DC = domain, DC = contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername | CN = entca、DC = domain, DC = contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore | 12/05/2016 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter | 12/05/2017 20:50:18
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subject | E =user@contoso.com、CN = ユーザー、CN = Users, DC = domain, DC = contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname | E =user@contoso.com、CN = ユーザー、CN = Users, DC = domain, DC = contoso, DC = com
|https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata | {Base64 でエンコードされたデータのデジタル証明書}
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | Digitalsignature ビット
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage | KeyEncipherment
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier | 9D11941EC06FACCCCB1B116B56AA97F3987D620A
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier | キー Id = d6 13 e3 6b bc e5 d8 15 52 0a fd 36 6a d5 0b 51 f3 0b 25 7f
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename | ユーザー
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/san | その他の名前: プリンシパル名 =user@contoso.com、rfc 822 名 =user@contoso.com
|https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku | 1.3.6.1.4.1.311.10.3.4


