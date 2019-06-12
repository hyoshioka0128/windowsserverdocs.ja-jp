---
title: AD FS パスワード攻撃からの保護
description: このドキュメントは、AD FS のユーザー パスワード攻撃から保護する方法を説明します
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5666943138070cfa8cfe62f1ba932c2793daa003
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501598"
---
# <a name="ad-fs-password-attack-protection"></a>AD FS パスワード攻撃からの保護

## <a name="what-is-a-password-attack"></a>パスワード攻撃とは何ですか。

フェデレーション シングル サインオンの要件は、インターネット経由で認証するエンドポイントの可用性です。 インターネット上の認証エンドポイントの可用性では、企業ネットワークにない場合でも、アプリケーションにアクセスすることができます。 

ただし、つまりもいくつかの問題のある相手が、インターネット上の使用可能なフェデレーション エンドポイントを利用してパスワードを確認するか、サービス拒否攻撃を作成するこれらのエンドポイントを使用できます。 一般的には、このような 1 つの攻撃対象と呼ばれる、**パスワード攻撃**します。 

パスワードの一般的な攻撃の 2 種類があります。 パスワード スプレー攻撃 & ブルート フォースのパスワード攻撃をします。 

### <a name="password-spray-attack"></a>パスワード スプレー攻撃
パスワード スプレー攻撃では、これらの問題のある相手は、多くのさまざまなアカウントとパスワードで保護された資産を検索できることをすべてにアクセスするサービスの間で、最も一般的なパスワードを試みます。 通常これら多くの異なる組織と id プロバイダーにまたがります。 たとえば、攻撃者はいくつかの組織のユーザーのすべてを列挙してから、"P@$$w0rd"と"Password1"これらのアカウントすべてに対して一般的なツールキットを使用します。 アイデアを与えると、攻撃を受けるようになります。


|  対象ユーザー   | ターゲットのパスワード |
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

個々 のユーザーまたは企業の観点から、攻撃のように見えます分離ログインに失敗したため、この攻撃のパターンはほとんど検出手法を evades します。

これは、攻撃者の番号ゲーム: 世の中にいくつかパスワードが非常に一般的ながあることを知っています。  攻撃者は攻撃を数千のアカウントごとに、いくつかの成功を取得し、有効にすれば十分です。 アカウントを使用して電子メールからデータを取得の連絡先情報を取得し、フィッシングのリンクを送信またはだけパスワード スプレー攻撃のターゲット グループを展開します。 攻撃者はありませんそれほど気はそれらの初期ターゲット — を活用できるいくつかの成果であることだけです。

これらの種類の攻撃に対して、AD FS を構成して、正しくネットワークをいくつかの手順を実行して AD FS のエンドポイントを保護できます。 この記事では、これらの攻撃に対する保護に役立つ適切に構成する必要がある 3 つの領域について説明します。

### <a name="brute-force-password-attack"></a>ブルート フォース パスワード攻撃 
この種の攻撃では、攻撃者はアカウントの対象セットに対して複数のパスワード試行に試みます。 多くの場合は、高いレベルのアクセスを組織内のユーザーに対してこれらのアカウントを対象になります。 これらにより、重要なインフラストラクチャを管理する管理者または組織内の役員可能性があります。  

この種の攻撃は、DOS のパターンにもなる可能性があります。 これにより、ADFS が大規模なサーバー数が不足しているために要求数を処理できないサービス レベルである可能性があります。 または、アカウントからユーザーがロックされているユーザー レベルである可能性があります。  

## <a name="securing-ad-fs-against-password-attacks"></a>パスワード攻撃からの AD FS をセキュリティで保護します。 

この種の攻撃に対して、AD FS を構成して、正しくネットワークをいくつかの手順を実行して AD FS のエンドポイントを保護できます。 この記事では、これらの攻撃に対する保護に役立つ適切に構成する必要がある 3 つの領域について説明します。 


- レベル 1 の場合は、基準:これらは、悪意のあるユーザーは、ブルート フォース攻撃がフェデレーション ユーザーをできないようにする AD FS サーバーを構成する必要がありますの基本的な設定です。 
- エクストラネットの保護レベル 2:これらは、設定、エクストラネット アクセスを構成してセキュリティで保護されたプロトコル、認証ポリシーと適切なアプリケーションを使用することを確認するように構成する必要があります。 
- エクストラネット アクセス用のレベル 3、パスワードのないへの移行:これらは、攻撃を受けのパスワードでより安全な資格情報はなくフェデレーション リソースにアクセスを有効にするには、設定とガイドラインに高度な。 

## <a name="level-1-baseline"></a>レベル 1:Baseline

1. ADFS 2016、実装する場合[エクストラネットのスマート ロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)エクストラネットのスマート ロックアウトは、場所を追跡し、以前ログインが正常にその場所から場合に有効なユーザーを許可します。 エクストラネットのスマート ロックアウトを使用すると、することができます悪意のあるユーザーがいないできるようにブルート フォース攻撃をユーザーの攻撃し、同時には正当なユーザーの生産性を使用します。
    - AD FS 2016 でない場合は強くお勧めする[アップグレード](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md)AD FS 2016 にします。 AD FS 2012 R2 からの単純なアップグレード パスになります。 AD FS 2012 R2 の場合は、実装[エクストラネットのロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)します。 このアプローチの欠点の 1 つは、ブルート フォース攻撃パターンを使用している場合、エクストラネット アクセスからの有効なユーザーをブロックする可能性があることです。 Server 2016 での AD FS には、この欠点はありません。

2. 監視とブロックの疑わしい IP アドレス 
    - Azure AD Premium があれば、ADFS を使用して接続の正常性を実装、[危険な IP レポート](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview)通知を提供します。

        a. ライセンスと、すべてのユーザーは、顧客を簡単になる可能性があります 25 ライセンス/ADFS/WAP サーバーが必要です。

        b. 失敗したログインの大きな数を生成している IP を調査することができますようになりました

        c. これで、ADFS サーバーで監査を有効にすることが必要です。

3.  不審な IP をブロックします。  これにより、DOS 攻撃を受ける可能性のあるブロックされます。

    a. 2016 年の場合は、使用、 [*エクストラネットの禁止された IP アドレス*](../../ad-fs/operations/configure-ad-fs-banned-ip.md) 3 (または手動の分析) の IP からの要求をブロックする機能フラグを設定します。

    b. AD FS 2012 R2 またはそれ以下の場合は、Exchange Online で直接、必要に応じて、ファイアウォール上の IP アドレスをブロックします。

4. 使用して、Azure AD Premium があれば、 [Azure AD のパスワード保護](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-on-premises)を Azure AD にパスワードの推測を防ぐために  

    a. いるパスワードの推測があれば、することができます解読にだけ 1 ~ 3 の試行に注意してください。 この機能では、これらの設定を取得できないようにします。 

    b. プレビュー統計からほぼ 20 ~ 50% の新しいパスワードの取得からブロック設定されています。 つまり、その % のユーザーが簡単に推測されたパスワードに対して脆弱になります。

## <a name="level-2-protect-your-extranet"></a>レベル 2:エクストラネットを保護します。

5. 先進認証をエクストラネットからアクセスするクライアントに移動します。 メール クライアントは、この大規模な部分です。 

    a. Outlook Mobile をモバイル デバイスに使用する必要があります。 新しい iOS のネイティブ メール アプリでは、最新の認証もサポートしています。 

    b. Outlook 2013 (最新の CU の更新プログラム) または Outlook 2016 を使用する必要があります。

6. MFA は、すべてのエクストラネット アクセスを有効にします。 これによりのエクストラネット アクセスの保護を追加します。

   a.  使用して、Azure AD premium があれば、 [Azure AD 条件付きアクセス ポリシー](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)これを制御します。  これは、AD FS で規則を実装するよりも優れています。  最新のクライアント アプリがより頻繁に適用されるためです。  これは、とき、Azure ad は、更新トークンを使用して新しいアクセス トークン (通常 1 時間ごと) を要求するときにします。  

   b.  Azure AD premium がない、またはがインターネットを許可する AD FS での他のアプリ ベースのアクセス、MFA (できます Azure MFA と AD FS 2016 で) を実装します。 操作を行います、[グローバル MFA ポリシー](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally)すべてのエクストラネット アクセス用。

## <a name="level-3-move-to-password-less-for-extranet-access"></a>レベル 3:エクストラネット アクセスの少ないパスワードへの移行

7. Window 10 を使用して[こんにちは For Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)します。

8. その他のデバイスの場合で AD FS 2016 を使用できます[Azure MFA の OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md)として最初の要素と第 2 要素としてのパスワード。 

9. モバイル デバイスは、MDM 管理対象のデバイスのみを許可する場合を使用できます[証明書](../../ad-fs/operations/configure-user-certificate-authentication.md)にユーザーをログインさせます。 

## <a name="urgent-handling"></a>緊急の処理

AD FS 環境がアクティブな攻撃を受けている場合、できるだけ早く、次の手順を実装する必要があります。

 - ADFS に U/P エンドポイントを無効にし、すべてのユーザーへのアクセスを取得するか、ネットワーク内で、VPN が必要です。 手順が必要ですこの**レベル 2 #1a**完了します。 EXO プロキシ認証を使用して、クラウド経由ではそれ以外の場合、する内部 Outlook のすべての要求がルーティングも
 - 攻撃の EXO 経由で発信のみ、Exchange プロトコル (POP、IMAP、SMTP、EWS など) の基本認証を無効にできます認証ポリシーを使用して、これらのプロトコルや認証方法で使用されているこれらの攻撃の大多数します。 さらに、EXO とメールボックスあたりのプロトコル対応のクライアント アクセス ルールが評価された後の認証で、攻撃を緩和することはできません。 
 - 選択的にレベル 3 1-3 を使用して、エクストラネット アクセスを提供します。

## <a name="next-steps"></a>次のステップ

- [AD FS サーバー 2016 へのアップグレードします。](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) 
- [AD FS 2016 でエクストラネットのスマート ロックアウト](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [条件付きアクセス ポリシーを構成します。](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Azure AD のパスワード保護](https://docs.microsoft.com/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
