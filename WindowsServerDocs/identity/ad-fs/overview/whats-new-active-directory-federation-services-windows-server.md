---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Active Directory フェデレーション サービスの Windows Server 2016 の新機能
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b8dd9174a869110d98ba1e65cbf2c2b6ec000b71
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Active Directory フェデレーション サービスの Windows Server 2016 の新機能

>Windows Server 2016 の適用対象:

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Active Directory フェデレーション サービスの Windows Server 2016 の新機能   
AD FS の以前のバージョンに関する情報を探している場合は、次の記事を参照してください。  
 [Windows Server 2012 または 2012 R2 での ADFS](https://technet.microsoft.com/library/hh831502.aspx)と[AD FS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 Active Directory フェデレーション サービスはアクセス制御とシングル サインオンで全体にわたるアプリケーションが Office 365、クラウド ベースの SaaS アプリケーションでは、企業ネットワーク上のアプリケーションなど、さまざまなします。  
* IT 組織のできますをで記号を入力し、アクセス制御モダンと従来の両方のアプリケーションに、クラウドおよび内部設置型に、同じ資格情報とポリシーのセットに基づきます。    
* ユーザーには、同じでなじみのあるアカウントの資格情報を使用してシームレスなサインインを提供します。  
* 開発者は、id は、アプリケーション、しない認証または identity、作業に集中できるように、組織のディレクトリに live ユーザーを認証する簡単な方法を提供します。  

この記事では、Windows Server 2016 (AD FS 2016) での AD FS の新機能について説明します。  

## <a name="eliminate-passwords-from-the-extranet"></a>エクストラネットからパスワードを排除します。  
Phished をリークしたしたり盗難されたりしたパスワードから AD FS 2016 により次の 3 つ用の新しいオプションをネットワークのリスクを避けるために組織を有効にすると、パスワードなしでサインインが侵害されます。 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure multi-factor Authentication を使用してログインします。
AD FS 2016 に基づいて、multi-factor authentication (MFA) 機能では、Windows Server 2012 R2 の AD FS の最初のユーザー名とパスワードを入力しなくても、Azure MFA コードのみを使用してサインオンできるようにしています。

* プライマリ認証方法として Azure MFA をで、ユーザー名と Azure Authenticator アプリからの OTP コード求められます。  
* Azure MFA のセカンダリまたは追加の認証方法として、Azure MFA ログイン ベースの OTP またはプライマリ認証が (Windows 統合認証、ユーザー名とパスワード、スマート カード、またはユーザーまたはデバイス証明書を使用)、資格情報、テキスト、音声のプロンプトが表示されます、ユーザーを提供します。  
* 新しい組み込み Azure MFA のアダプターと AD FS と Azure MFA のセットアップと構成がこれまでに簡単です。
* ご利用 Azure MFA の内部設置型 Azure MFA のサーバーの必要はありません。
* イントラネットまたはエクストラネット、またはすべてのアクセス制御ポリシーの一部として、azure MFA を構成することができます。

詳細については、AD FS と Azure MFA
*  [AD FS 2016 と Azure MFA を構成します。](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>対応デバイスからパスワードのないアクセス
AD FS 2016 のビルドでのサインインを有効にする前のデバイス登録の機能にし、デバイスのコンプライアンス状態ベースのアクセス制御します。 ユーザーがデバイス資格情報を使用してサインオンでき、対応が再評価されてデバイスの属性を変更するときにポリシーが適用されているを常に確認できるようにします。  これによって、ポリシーなど

* 管理されているか、または準拠しているデバイスからのみアクセスを有効にします。  
* 管理されているか、または準拠しているデバイスからのみへのエクストラネット アクセスを有効にします。  
* 管理されているまたは非準拠ではないコンピューターに対して多要素認証を要求します。  

AD FS では、ハイブリッド シナリオでは条件付きアクセス ポリシーの上の内部設置型コンポーネントを提供します。 クラウド リソースへの条件付きアクセス用の Azure AD にデバイスを登録するとき、デバイス ID を使用 for AD FS のポリシーもします。

![新機能します。](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 詳細については、デバイスを使用してベースのクラウドでの条件付きアクセス   
 *  [Azure Active Directory の条件付きアクセス](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)

詳細については、デバイスを使用してベースの AD FS による条件付きアクセス
*  [AD FS による条件付きアクセスをベースのデバイスの計画](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [AD FS のアクセス制御ポリシー](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>Windows Hello for Business でログインします。   
Windows 10 デバイスが Windows Hello と Windows Hello for Business をで保護されている強力なデバイスにバインドされたユーザーの資格情報を持つユーザーのパスワードの代わりに導入します。ユーザーのジェスチャ (PIN、指紋、顔認識などの生体認証ジェスチャ)。 AD FS 2016 サポートこれら新しいこれらの新しい Windows 10 機能するため、ユーザーにログインできる AD FS アプリケーションから、イントラネットまたはエクストラネットのパスワードを指定する必要はありません。

詳細については、Microsoft Windows Hello for Business を使った組織で
*  [有効にする Windows Hello for Business の組織で](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>セキュリティで保護されたアプリケーションにアクセスする

### <a name="modern-authentication"></a>最新の認証
AD FS 2016 では、Windows 10 だけでなく、最新の iOS および Android デバイスとアプリのより優れたユーザー エクスペリエンスを提供する最新のモダン プロトコルをサポートします。  

詳細については、次を参照してください[開発者向けの AD FS のシナリオ。](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>知る必要なく、アクセス制御ポリシーを構成する要求規則言語  
以前は、AD FS 管理者が AD FS の要求規則言語を使用してポリシーを構成するを構成し、ポリシーの管理が困難です。 アクセス制御ポリシーにより、管理者などの一般的なポリシーを適用するのに組み込みのテンプレートを使用できます。
* イントラネット アクセスのみを許可します。
* すべてのユーザーを許可し、エクストラネットから MFA が必要
* すべてのユーザーを許可し、特定のグループから MFA が必要

テンプレートは、例外またはその他のポリシーの規則を追加するプロセスを優先するウィザードを使用してをカスタマイズし、やすく一貫性のあるポリシーの実施の 1 つまたは複数のアプリケーションに適用することができます。

詳細については、次を参照してください。[AD FS のアクセス制御ポリシー。](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>AD 以外の LDAP ディレクトリと署名を有効にします。  
多くの組織では、Active Directory とディレクトリのサード パーティ製の組み合わせが必要です。 LDAP v3 に準拠したディレクトリに格納されているユーザーを認証するための AD FS サポートの追加によりは AD FS の使用できるようになりましたことができます。
* サード パーティ LDAP v3 準拠のディレクトリ内のユーザー
* Active Directory 双方向の信頼が構成されていない Active Directory フォレスト内のユーザー
* Active Directory ライトウェイト ディレクトリ サービス (AD LDS) 内のユーザー

詳細については、次を参照してください。[LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>サインイン エクスペリエンス向上
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>ログ内の AD FS のアプリケーション エクスペリエンスをカスタマイズします。  
おから聞こえる各アプリケーションのログオン エクスペリエンスをカスタマイズする機能が組織でアプリケーションを表す複数の異なる会社やブランドの署名を提供するために特別に、優れた使いやすさの改善になることです。  

以前は、Windows Server 2012 R2 の AD FS は、エクスペリエンスですべての証明書利用者のパーティ製アプリケーションの一般的な記号を提供、テキストのサブセットをカスタマイズする機能ベースのアプリケーションあたりのコンテンツ。 Windows Server 2016 では、だけでなく、メッセージが、画像、アプリケーションあたりのロゴと Web テーマをカスタマイズできます。 また、新しいカスタム Web テーマを作成し、これら証明書利用者ごとに適用パーティーします。  

詳細については、次を参照してください。[AD FS ユーザーのサインインにカスタマイズします。](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>管理容易性、および運用上の機能強化  
次のセクションでは、Windows Server 2016 での Active Directory フェデレーション サービスで導入された、強化された運用のシナリオについて説明します。  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>簡単に管理の監査の合理化  
Ad FS の Windows Server 2012 R2 がありますされた 1 つの要求の生成された多数の監査イベントおよび関連するログインまたはトークンの発行アクティビティについては、存在しないか、一部のバージョンの AD FS) の「または複数の監査イベントの間で分散します。 既定では、AD FS の詳細な性質、監査イベントが無効になります。  
AD FS 2016 のリリースから、監査になりより合理化された出力を少なくします。  

詳細については、次を参照してください。[Windows Server 2016 での AD FS の機能強化を監査します。](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Confederations への参加 SAML 2.0 との相互運用性の向上  
AD FS 2016 では、メタデータを含む複数のエンティティに基づく信頼をインポートするためのサポートを含む追加の SAML プロトコルのサポートが含まれています。 これにより、AD FS confederations InCommon フェデレーションおよび eGov 2.0 標準に準拠しているその他の実装などへの参加を構成することができます。  

詳細については、次を参照してください。[SAML 2.0 との相互運用性が向上します。](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>管理を簡素化されたパスワード フェデレーション O365 ユーザー  
AD FS によって保護されている証明書利用者のパーティ信頼 (アプリケーション) には、Active Directory フェデレーション サービス (AD FS) のパスワードの有効期限クレームを送信するを構成できます。 これらの要求を使用する方法は、アプリケーションに依存します。 たとえばと、証明書利用者として Office 365、更新プログラムを早くに-する-有効期限の切れてパスワードのフェデレーション ユーザーに通知するには、Exchange と Outlook に実装されています。  

詳細については、次を参照してください。[パスワードの有効期限クレームを送信する AD FS を構成します。](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>簡単には、Windows Server 2012 R2 の AD FS から Windows Server 2016 での AD FS に移行します。  
以前は、AD FS の新しいバージョンに移行するために必要な以前のファームから構成をエクスポートし、新しいか、並列のファームにインポートします。  

これで、Windows Server 2016 での AD FS を Windows Server 2012 R2 で AD FS から移動に簡単になりました。 Windows Server 2012 R2 のファームに新しい Windows Server 2016 サーバーを追加するだけの外観し、Windows Server 2012 R2 ファームと同じように動作するように、Windows Server 2012 R2 のファーム動作レベルで、ファームが機能する.  

次に、Windows Server 2016 の新しいサーバーをファームに追加、機能を検証および以前のサーバーをロード バランサーから削除します。 すべてのファーム ノードでは、Windows Server 2016 を実行している、いったんファームレベル動作 2016年へのアップグレードし、新機能の使用を開始することができます。  

詳細については、次を参照してください。[Windows Server 2016 での AD FS へのアップグレードします。](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
