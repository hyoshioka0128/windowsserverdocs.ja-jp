---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: どのような&#39;s Active Directory Domain Services の新機能
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: ''
ms.suite: na
ms.technology: active-directory-domain-services
ms.tgt_pltfrm: na
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: ffa8bcb43b17ae8779c70d499bff27a8f77cce75
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841333"
---
# <a name="what39s-new-in-active-directory-domain-services"></a>どのような&#39;s Active Directory Domain Services の新機能 

>適用先:Windows Server 2016

Active Directory Domain Services (AD DS)、次の新機能は、Active Directory 環境をセキュリティで保護し、移行すると、クラウドのみのデプロイとハイブリッド展開では、いくつかのアプリケーションとサービスが組織の機能を向上させます。クラウドでホストされている他のユーザーがオンプレミスでホストされているとします。 機能強化は次のとおりです。  
  
-   [特権アクセス管理](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Azure Active Directory Join を使用の Windows 10 デバイスへのクラウド機能を拡張します。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [で Windows 10 用の Azure AD にドメイン参加済みデバイスを接続します。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [組織で Microsoft Passport for Work を有効にします。](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルの廃止](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>特権アクセス管理  
Privileged access management (PAM) は、セキュリティの軽減します。 このような pass the hash、スピア フィッシング、および類似した種類の攻撃の資格情報窃盗手法の懸念事項によって引き起こされる Active Directory 環境にします。 Microsoft Identity Manager (MIM) を使用して構成されている新しい管理アクセス ソリューションを提供します。 PAM が導入されています。  
  
-   新しい要塞 Active Directory フォレストは、MIM はプロビジョニングされています。 要塞フォレストは、既存フォレストを持つ特別な PAM 信頼関係にあります。 悪意のあるアクティビティ、および特権アカウントの使用の既存のフォレストからの分離の無料であることがわかっている新しい Active Directory 環境を提供します。  
  
-   要求の承認に基づく新しいワークフローと共に、管理特権を要求する MIM で新しいプロセス。  
  
-   新しいシャドウ セキュリティ プリンシパル (グループ) 管理者特権の要求に対する応答で MIM で要塞フォレストでプロビジョニングされています。 シャドウのセキュリティ プリンシパルには、既存のフォレスト内の管理グループの SID を参照する属性があります。 これにより、アクセス制御リスト (Acl) を変更することがなく既存のフォレストのリソースにアクセスするシャドウ グループです。  
  
-   有効期限により、期限付きのシャドウ グループ メンバーシップの機能にリンクします。 ユーザーは、管理タスクを実行に必要なのに十分な時間のグループに追加できます。 期限付きメンバーシップは、Kerberos チケットの有効期間に反映される有効期限 (TTL) 値によって表されます。  
  
    > [!NOTE]  
    > 有効期限が切れるリンクは、すべてのリンクされた属性で使用できます。 リンクのメンバー/memberOf 属性が、グループとユーザー間のリレーションシップが唯一の例では、有効期限が切れるリンク機能を使用する PAM などの完全なソリューションがあらかじめ構成されています。  
  
-   KDC の機能強化は、最小有効期限 (TTL) 値をユーザーが管理グループに複数の期限付きメンバーシップがある場合に Kerberos チケットの有効期間を制限する Active Directory ドメイン コント ローラー構築されます。 たとえば、Kerberos チケット保証チケット (TGT) 有効期間は、時間と同じにログオンするときに期限付きのグループ A に追加されている場合があるグループ A に残っています。B で、グループ A よりも低い TTL には、別の期限付きグループのメンバーである場合は、グループ B の残り時間と等しく、TGT の有効期間  
  
-   ため、簡単に新しい監視機能は、アクセスを要求したユーザー、アクセス権が付与された、および実行されたアクティビティを特定します。  
  
**必要条件**  
  
-   Microsoft Identity Manager  
  
-   Active Directory フォレストの機能レベルの Windows Server 2012 R2 またはそれ以降。  
  
## <a name="BKMK_AzureADJoin"></a>Azure AD Join  
Azure Active Directory Join、enterprise、business および EDU - お客様の会社と個人のデバイス用の強化された機能の使用の id エクスペリエンスが向上します。  
  
利点:  
  
-   **最新の設定の可用性**企業所有の Windows デバイスにします。 酸素サービスには、個人の Microsoft アカウントが不要になった: ユーザーの既存の職場アカウントを確実に遵守オフ実行ようになりました。 酸素サービスは、オンプレミスの Windows ドメインに参加している Pc、Pc と、Azure AD テナント (「クラウド ドメイン」) に「結合」されているデバイスで機能します。 これらの設定には次のものが含まれます。  
  
    -   移動またはパーソナル化、ユーザー補助の設定と資格情報  
  
    -   バックアップと復元  
  
    -   職場アカウントを使って Microsoft Store へのアクセス  
  
    -   ライブ タイルと通知  
  
-   **組織のリソースにアクセス**corp が所有しているかにかかわらず、Windows ドメインに参加できないモバイルのデバイス (携帯電話、ファブレット) または BYOD  
  
-   **シングル サインオン**Office 365 と他の組織のアプリ、web サイト、およびリソースにします。  
  
-   **BYOD デバイスで**(オンプレミスのドメインまたは Azure AD) から職場アカウントを個人所有のデバイスに追加し、条件付きのアカウントなどの新機能への準拠を維持する方法で作業できると、web アプリを使用して、リソースへの SSO をお楽しみくださいコントロールとデバイスの正常性構成証明書。  
  
-   **MDM 統合**MDM (Intune またはサード パーティ製) にデバイスの自動登録することができます  
  
-   **「キオスク」モードを設定し、共有デバイス**組織内の複数のユーザー  
  
-   **開発者エクスペリエンス**企業や個人のコンテキストを共有プログラミング スタックの両方に提供されるアプリを構築できます。  
  
-   **イメージング**オプションを使用して、最初の実行エクスペリエンス中に直接企業所有のデバイスを構成するイメージングとにより、ユーザーが選択できます。  
  
詳細については、「[エンタープライズ向け Windows 10。デバイスの作業を使用する方法](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1)します。  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport は、新しいキー ベースの認証方法、組織とコンシューマーは、パスワードを超えます。 この形式の認証は、侵害、盗難、およびフィッシングに対する耐性の資格情報に依存します。  
  
ユーザーは、生体認証または PIN のログを証明書または非対称キーのペアにリンクされている情報に、デバイスにログオンします。 Id プロバイダー (Idp) は、IDLocker に、ユーザーの公開キーをマップすることによって、ユーザーを検証し、ログを 1 つワンタイム パスワード (OTP)、Phonefactor または他の通知メカニズムを使用して情報を提供します。  
  
詳細については、「 [Microsoft Passport 経由でのパスワードしない id の認証](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルの廃止  
ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルは、Windows Server の以前のバージョンで非推奨とされた、繰り返しておく価値が Windows Server 2003 オペレーティング システムがサポートされていません。 その結果、Windows Server 2003 を実行している任意のドメイン コント ローラーをドメインから削除する必要があります。 ドメインとフォレストの機能レベルを以上に発生する必要がありますを環境に追加されない以前のバージョンの Windows Server を実行するドメイン コント ローラーを防ぐために Windows Server 2008。  
  
Windows Server 2008 以上のドメイン機能レベルでは、分散ファイル システム (DFS) レプリケーションを使用して、ドメイン コント ローラー間の SYSVOL フォルダーの内容をレプリケートします。 以降、Windows Server 2008 のドメイン機能レベルで新しいドメインを作成すると、SYSVOL をレプリケートする DFS レプリケーションが自動的に使用します。 低い機能レベル ドメインを作成した場合は、SYSVOL の DFS レプリケーションに FRS を使用してから移行する必要があります。 移行手順については、いずれかに従ってできます、 [technet プロシージャ](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)または参照できる、[ストレージ チームのファイル キャビネット ブログでの手順のセットを簡素化](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)。  
  
Windows Server 2003 のドメインとフォレストの機能レベルが引き続きサポートされますが、組織は、Windows Server 2008 (またはより高いは、可能な場合) の機能レベルを上げる必要がありますを SYSVOL レプリケーションの互換性を確保し、将来的にサポートします。 さらに、その他の多くのメリットと機能使用ではより高い機能レベルより高いです。 詳細については、次のリソースを参照してください。  
  
-   [Active Directory domain Services の (AD DS) の機能レベル](ad-ds/active-directory-functional-levels.md)  
  
-   [ドメイン機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)  
  
