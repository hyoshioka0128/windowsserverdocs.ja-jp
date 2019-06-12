---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: ユーザー証明書認証をサポートする AD FS 構成します。
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c69192a4223379b896a57eb04a38e37863c1366e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444308"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>AD FS ユーザー証明書認証の構成


X509 ユーザー証明書の認証モードのいずれかの方法が記載の AD FS を構成することができます[今回](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)します。 この機能を使用できる[と Azure Active Directory](https://blogs.msdn.microsoft.com/samueld/2016/07/19/adfs-certauth-aad-o365/)自体でクライアントとデバイスを有効にするがプロビジョニングに AD FS にアクセスするユーザーの証明書、イントラネットまたはエクストラネットからリソース。

## <a name="prerequisites"></a>前提条件
- すべての AD FS と WAP サーバーによって、ユーザー証明書が信頼できることを確認します。
- Active Directory で NTAuth ストア内のユーザー証明書の信頼チェーンのルート証明書があることを確認します。
- AD FS を使用して、代替の証明書認証モードで場合、AD FS および WAP サーバーが付いています"certauth"、たとえば"certauth.fs.contoso.com"と、AD FS ホスト名が含まれている SSL 証明書があることを確認し、このホスト名には、そのトラフィックを許可します。ファイアウォールを経由
- エクストラネットからの証明書認証を使用する場合は、少なくとも 1 つ AIA と CDP または OCSP の少なくとも 1 つの場所、証明書で指定されたリストからは、インターネットからアクセスできることを確認します。
- Azure AD の証明書認証用の AD FS を構成する場合は、構成したことを確認、 [Azure AD 設定](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)と[AD FS の要求規則のために必要な](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements)証明書の発行者とシリアル番号
- Exchange ActiveSync クライアントの場合、Azure AD の証明書認証のクライアント証明書も必要、ユーザーのルーティング可能な電子メール アドレス Exchange オンライン プリンシパル名または RFC822 名のサブジェクト代替名フィールドの値のいずれかで。 (Azure Active Directory に、ディレクトリにプロキシ アドレス属性にある RFC822 値がマップ) します。

## <a name="configure-ad-fs-for-user-certificate-authentication"></a>ユーザー証明書認証用に AD FS を構成する  
- イントラネットまたは AD FS 管理コンソールまたは PowerShell コマンドレット セット AdfsGlobalAuthenticationPolicy のいずれかを使用して、AD FS でエクストラネットの認証方法として、ユーザー証明書認証を有効にします。
- すべての AD FS と WAP サーバー上の任意の中間証明書の信頼チェーン全体がインストールされていることを確認します。 中間証明書は、すべての AD FS と WAP サーバーのローカル コンピューターの中間証明機関ストアにインストールする必要があります。
- 証明書のフィールドとに加えて、EKU 拡張機能に基づくクレームを使用する場合 (要求の種類 https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku)、Active Directory 要求プロバイダー信頼の追加の要求のパススルー規則を構成します。  使用可能な証明書の要求の完全な一覧については、以下を参照してください。  
- [省略可能]「クライアント認証用の信頼された発行者の管理」の下のガイダンスを使用してクライアント証明書の発行元証明機関を許可されている構成[今回](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx)します。

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Windows デスクトップで Chrome ブラウザーのシームレスな証明書認証を構成します。
(Wi-fi 証明書) などの複数のユーザー証明書がクライアント認証の目的に適合するコンピューターに存在する場合は、Windows デスクトップで、Chrome ブラウザーは、ユーザーに適切な証明書の選択を求められます。 これは、エンドユーザーに混乱を招く可能性があります。 このエクスペリエンスを最適化するには、Chrome のユーザー エクスペリエンスを向上させる適切な証明書の自動選択するためのポリシーを設定できます。 このポリシーは、レジストリの変更が手動で設定または GPO (レジストリ キーを設定する) を使用して自動的に構成できます。 これには、他のユース ケースから個別の発行者を使用して AD FS に対する認証のため、ユーザー クライアント証明書が必要です。 

Chrome 用に構成の詳細については、これを参照してください[リンク](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls)します。  


## <a name="troubleshooting"></a>トラブルシューティング
- HTTP 204 と証明書の認証要求が失敗した場合"https からのコンテンツはありません:\//certauth.fs.contoso.com"応答、ルートおよび中間 CA 証明書がインストールされていること、それぞれ、信頼されたルート CA をことを確認し、中間 CA 証明書は、すべてのフェデレーション サーバーに保存します。
- 不明な理由は、証明書の認証要求が失敗する場合、.cer ファイルに、クライアント証明書をエクスポートし、コマンドを実行 

`certutil -f -urlfetch -verify certificatefilename.cer`

任意の CRL および delta CRL の場所の解決を確認してください。  Base CRL の内容に基づく delta CRL の場所を検出することに注意してください。

## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>参照 :ユーザー証明書の完全な一覧クレームの種類と値の例

|                                         要求の種類                                         |                              値の例                               |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version         |                                    3                                     |
|     https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm      |                                sha256RSA                                 |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer            |                 CN = entca、DC = domain, DC = contoso, DC = com                  |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername          |                 CN = entca、DC = domain, DC = contoso, DC = com                  |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore          |                           12/05/2016 20:50:18                            |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter           |                           12/05/2017 20:50:18                            |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/subject           |   E =user@contoso.comCN = ユーザー、CN = Users, DC = domain, DC = contoso, DC = com   |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname         |   E =user@contoso.comCN = ユーザー、CN = Users, DC = domain, DC = contoso, DC = com   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata           |                {Base64 でエンコードされたデジタル証明書データ}                 |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             Digitalsignature ビット                             |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             KeyEncipherment                              |
|  https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier   |                 9D11941EC06FACCCCB1B116B56AA97F3987D620A                 |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier  |    KeyID = d6 13 e3 6b bc e5 d8 15 52 0a fd 36 6a d5 0b 51 f3 0b 25 7 f     |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename |                                   ユーザー                                   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/san           | その他の名前プリンシパル名 =user@contoso.com、RFC822 名 =。user@contoso.com |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku           |                          1.3.6.1.4.1.311.10.3.4                          |

