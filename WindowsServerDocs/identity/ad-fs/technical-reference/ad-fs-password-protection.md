---
title: AD FS パスワード攻撃による保護
description: このドキュメントでは、AD FS ユーザーをパスワード攻撃から保護する方法について説明します。
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.author: billmath
ms.openlocfilehash: c17ef0524ed873c8a3d506df75542848e2c4bca7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956159"
---
# <a name="ad-fs-password-attack-protection"></a>AD FS パスワード攻撃による保護

## <a name="what-is-a-password-attack"></a>パスワード攻撃とは何ですか。

フェデレーションシングルサインオンの要件は、インターネット経由で認証するためのエンドポイントの可用性です。 インターネット上で認証エンドポイントが利用可能になると、ユーザーが企業ネットワーク上にいなくてもアプリケーションにアクセスできるようになります。

ただし、これは、一部の悪意のあるアクターがインターネット上で使用可能なフェデレーションエンドポイントを利用し、これらのエンドポイントを使用してパスワードを試行して判断したり、サービス拒否攻撃を行ったりすることも意味します。 このような攻撃の1つには、**パスワード攻撃**と呼ばれるものがあります。

一般的なパスワード攻撃には2種類あります。 ブルートフォースパスワード攻撃 & パスワードスプレー攻撃。

### <a name="password-spray-attack"></a>パスワードスプレー攻撃
パスワードスプレー攻撃では、これらの悪意のあるアクターは、さまざまなアカウントやサービスで最も一般的なパスワードを試して、検出可能なパスワード保護された資産にアクセスします。 通常、これらは多くの異なる組織および id プロバイダーにまたがります。 たとえば、攻撃者は、一般的に利用可能なツールキットを使用して複数の組織内のすべてのユーザーを列挙した後、これらのすべてのアカウントに対して "P@ $ $w 0rd" と "Password1" を試してみます。 アイデアを得るために、攻撃は次のようになります。


|  ターゲットユーザー   | ターゲットパスワード |
|----------------|-----------------|
| User1@org1.com |    Password1    |
| User2@org1.com |    Password1    |
| User1@org2.com |    Password1    |
| User2@org2.com |    Password1    |
|       …        |        …        |
| User1@org1.com |    P@$$w0rd     |
| User2@org1.com |    P@$$w0rd     |
| User1@org2.com |    P@$$w0rd     |
| User2@org2.com |    P@$$w0rd     |

この攻撃パターンは、個々のユーザーまたは企業の視点ポイントから、攻撃が失敗した分離されたログインのようなものであるため、ほとんどの検出手法を evades しています。

攻撃者にとって、これは数値ゲームです。私たちは、非常に一般的なパスワードがあることを認識しています。  攻撃者は、数千のアカウントが攻撃を受けた場合に成功します。 これらのアカウントを使用して、電子メールからデータを取得したり、連絡先情報を取得したり、フィッシングリンクを送信したり、パスワードスプレーターゲットグループだけを展開したりします。 攻撃者は、これらの最初のターゲットがだれであるかについてはあまり気にしません。

ただし、AD FS とネットワークを正しく構成するためにいくつかの手順を実行することで、AD FS エンドポイントをこれらの種類の攻撃に対してセキュリティで保護することができます。 この記事では、これらの攻撃から保護するために適切に構成する必要がある3つの領域について説明します。

### <a name="brute-force-password-attack"></a>ブルートフォースパスワード攻撃
この種の攻撃では、攻撃者は、対象となるアカウントのセットに対して複数のパスワードを試行します。 多くの場合、これらのアカウントは、組織内でより高いレベルのアクセス権を持つユーザーを対象とします。 これは、組織内の経営幹部や、重要なインフラストラクチャを管理する管理者である場合があります。

この種の攻撃によって、DOS パターンが生じる可能性もあります。 これは、サーバーの数が不足しているために ADFS が大量の要求を処理できない場合、またはユーザーが自分のアカウントからロックアウトされているユーザーレベルの場合に発生する可能性があります。

## <a name="securing-ad-fs-against-password-attacks"></a>パスワード攻撃に対する AD FS のセキュリティ保護

ただし、AD FS とネットワークを正しく構成するためにいくつかの手順を実行することで、AD FS エンドポイントをこれらの種類の攻撃から保護することができます。 この記事では、これらの攻撃から保護するために適切に構成する必要がある3つの領域について説明します。


- レベル1、ベースライン: これらは AD FS サーバーで構成する必要がある基本的な設定であり、悪意のあるアクターによるブルートフォース攻撃が、フェデレーションユーザーに強制されないようにする必要があります。
- レベル2、エクストラネットの保護: セキュリティで保護されたプロトコル、認証ポリシー、および適切なアプリケーションを使用するようにエクストラネットアクセスが構成されていることを保証するために、これらの設定を構成する必要があります。
- レベル3、エクストラネットアクセスの場合はパスワードを小さくします。これは、攻撃を受けやすいパスワードではなく、より安全な資格情報でフェデレーションリソースにアクセスできるようにするための高度な設定とガイドラインです。

## <a name="level-1-baseline"></a>レベル 1: ベースライン

1. ADFS 2016 の場合、[エクストラネットのスマートロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)を実装すると、スマートロックアウトがよく知られている場所を追跡し、その場所から以前に正常にログインしたことがあれば、有効なユーザーを通過させることができます。 エクストラネットのスマートロックアウトを使用することにより、悪意のあるアクターがユーザーと同時にブルートフォース攻撃を受けることができないようにすることで、正当なユーザーの生産性を高めることができます。
    - AD FS 2016 を使用していない場合は、AD FS 2016 に[アップグレード](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md)することを強くお勧めします。 AD FS 2012 R2 からの単純なアップグレードパスです。 AD FS 2012 R2 を使用している場合は、[エクストラネットロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)を実装します。 この方法の欠点の1つは、ブルートフォースパターンを使用している場合に、有効なユーザーがエクストラネットアクセスをブロックする可能性があることです。 サーバー2016の AD FS には、この欠点はありません。

2. 疑わしい IP アドレスを監視 & ブロックする
    - Azure AD Premium がある場合は、ADFS の Connect Health を実装し、提供されている[危険な IP レポート](/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview)通知を使用します。

        a. ライセンスはすべてのユーザーにとってではなく、25ライセンス/ADFS/WAP サーバーを必要とします。これは、お客様にとっては簡単です。

        b. 多数の失敗したログインを生成している IP を調査できるようになりました。

        c. この場合、ADFS サーバーで監査を有効にする必要があります。

3.  疑わしい IP のをブロックします。  これにより、DOS 攻撃がブロックする可能性があります。

    a. 2016の場合は、[*エクストラネットの禁止 ip アドレス*](../../ad-fs/operations/configure-ad-fs-banned-ip.md)機能を使用して、#3 によってフラグが設定された ip (または手動分析) からの要求をブロックします。

    b. AD FS 2012 R2 以降を使用している場合は、Exchange Online で IP アドレスを直接ブロックし、必要に応じてファイアウォールでブロックします。

4. Azure AD Premium がある場合は、 [Azure AD パスワード保護](/azure/active-directory/authentication/concept-password-ban-bad-on-premises)を使用して、推測パスワードを取得できないようにしてください Azure AD

    a. 推測パスワードを使用している場合は、1-3 回だけ試行してしまうことに注意してください。 この機能により、これらの設定が行われなくなります。

    b. プレビューの統計からは、新しいパスワードの約20-50% が設定されるのをブロックします。 これは、ユーザーの% がパスワードを推測しやすいという脆弱性を持つことを意味します。

## <a name="level-2-protect-your-extranet"></a>レベル 2: エクストラネットを保護する

5. エクストラネットからアクセスするすべてのクライアントの最新の認証に移行します。 メールクライアントは、このような大きな役割を持ちます。

    a. モバイルデバイスには Outlook Mobile を使用する必要があります。 新しい iOS ネイティブメールアプリでは、先進認証もサポートされています。

    b. Outlook 2013 (最新の CU 修正プログラムを適用) または Outlook 2016 を使用する必要があります。

6. すべてのエクストラネットアクセスに対して MFA を有効にします。 これにより、すべてのエクストラネットアクセスの保護が追加されます。

   a.  Premium Azure AD がある場合は、 [Azure AD 条件付きアクセスポリシー](/azure/active-directory/conditional-access/overview)を使用してこれを制御します。  これは、AD FS で規則を実装するよりも優れています。  これは、最新のクライアントアプリがより頻繁に適用されるためです。  これは、Azure AD 時に、更新トークンを使用して新しいアクセストークン (通常は1時間ごと) を要求したときに発生します。

   b.  Premium Azure AD がない場合、またはインターネットベースのアクセスを許可する AD FS に追加のアプリがある場合は、MFA を実装します (AD FS 2016 でも Azure MFA として使用できます)。また、すべてのエクストラネットアクセスに対して[グローバル MFA ポリシー](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally)を実行します。

## <a name="level-3-move-to-password-less-for-extranet-access"></a>レベル 3: エクストラネットアクセス用にパスワードを小さくする

7. ウィンドウ10に移動し、 [Hello For business](/windows/security/identity-protection/hello-for-business/hello-identity-verification)を使用します。

8. その他のデバイスの場合、AD FS 2016 では、第2要素として[AZURE MFA OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md)を最初の要素として使用できます。

9. モバイルデバイスの場合、MDM で管理されているデバイスのみを許可する場合は、[証明書](../../ad-fs/operations/configure-user-certificate-authentication.md)を使用してユーザーをに記録できます。

## <a name="urgent-handling"></a>緊急の処理

AD FS 環境がアクティブな攻撃を受けている場合は、次の手順を最も早い段階で実装する必要があります。

 - ADFS で U/P エンドポイントを無効にし、すべてのユーザーにアクセスを許可するか、ネットワーク内にあることを VPN に要求します。 そのためには、ステップ**レベル 2 #1a**完了している必要があります。 それ以外の場合、すべての内部 Outlook 要求は、EXO proxy auth 経由で引き続きクラウド経由でルーティングされます。
 - 攻撃が EXO を通じてのみ行われる場合は、認証ポリシーを使用して Exchange プロトコル (POP、IMAP、SMTP、EWS など) の基本認証を無効にすることができます。これらのプロトコルと認証方法は、これらの攻撃の大部分で使用されています。 さらに、EXO およびメールボックスごとのプロトコルの有効化のクライアントアクセスルールは、認証後に評価され、攻撃の緩和には役立ちません。
 - レベル 3 #1 3 を使用してエクストラネットアクセスを選択的に提供します。

## <a name="next-steps"></a>次のステップ

- [AD FS server 2016 へのアップグレード](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md)
- [AD FS 2016 でのエクストラネットのスマートロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [条件付きアクセスポリシーを構成する](/azure/active-directory/conditional-access/overview)
- [パスワード保護の Azure AD](/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
