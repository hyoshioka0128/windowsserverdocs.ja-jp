---
ms.assetid: 6a852428-c1ec-4703-b3b3-a4bfdf8cbb9d
title: "新; s を Windows Server 2016 での Active Directory ドメイン サービスの新機能"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1fdd012af6f025d58340f63f98da0d8dc11df0e0
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-in-active-directory-domain-services-for-windows-server-2016"></a>新; s Active Directory ドメイン サービスの Windows Server 2016 の新機能

>Windows Server 2016 の適用対象:

Active Directory ドメイン サービス (AD DS) で次の新機能では、組織は Active Directory 環境をセキュリティで保護し、クラウドのみの展開とハイブリッドの展開、一部のアプリケーションとサービスが、クラウドでホストされている、他のユーザーはオンプレミスでホストに移行するための機能が改善します。 機能強化は、次のとおりです。  
  
-   [特権アクセス管理](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Windows 10 デバイスを Azure Active Directory に参加するクラウドの機能を拡張します。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [エクスペリエンスの Windows 10 用の Azure AD にドメインに参加しているデバイスを接続します。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [組織で Microsoft Passport for Work を有効にします。](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルの廃止](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="BKMK_PAM"></a>特権アクセス管理  
特権アクセス管理 (PAM) は、セキュリティの軽減します。このような - pass-the-hash、スピア フィッシング、およびのような種類の攻撃資格情報窃盗手法の問題が原因で発生する Active Directory 環境です。 Microsoft Identity Manager (MIM) を使用して構成されている新しい管理用アクセス ソリューションを提供します。 PAM が導入されています。  
  
-   新しい要塞 Active Directory フォレストは、MIM は、プロビジョニングされています。 要塞フォレストは、既存のフォレストで特別な PAM 信頼関係にあります。 悪意のあるアクティビティ、および権限を持つアカウントを使用するための既存のフォレストから分離のフリーであることが判明している新しい Active Directory 環境を提供します。  
  
-   要求の承認に基づく新しいワークフローと共に、管理特権を要求する MIM で新しいプロセスです。  
  
-   新しいシャドウ セキュリティ プリンシパル (グループ)、要塞フォレスト内で管理者特権の要求に応答 MIM によってプロビジョニングされています。 シャドウのセキュリティ プリンシパルは、既存のフォレスト内の管理グループの SID を参照する属性を持ちます。 これにより、任意のアクセス制御リスト (Acl) を変更することがなく、シャドウ グループに既存のフォレストのリソースにアクセスします。  
  
-   有効期限が切れるリンク機能、これにより、期限付きグループのメンバー、シャドウします。 ユーザーは、管理タスクを実行するために必要十分な時間をグループに追加できます。 期限付きのメンバーシップは、Kerberos チケットの有効期間に伝達される live 時間 (TTL) の値で表されます。  
  
    > [!NOTE]  
    > 有効期限が切れるリンクは、リンクされたすべての属性でご確認いただけます。 メンバー/memberOf リンクされた属性が、グループとユーザー間の関係は PAM などの完全なソリューションが有効期限が切れるリンク機能を使用して事前に構成されている唯一の例を示します。  
  
-   KDC の機能強化は、考えられるライブ時間 (TTL) の最低値、ユーザーが管理グループに複数の期限付きのメンバーシップがある場合に、Kerberos チケットの有効期間を制限する Active Directory ドメイン コントローラーに組み込まれています。 たとえば、Kerberos チケット保証チケット (TGT) 有効期間は、時間と同じにログオンすると、期限付きグループ A に追加する場合があるグループ A に残っています。B で、グループ A よりも低い TTL には、別の期限付きグループのメンバーでも場合と同じグループ B に残っていることができる期間に、TGT の有効期間  
  
-   新しいの監視機能を簡単にするのには、アクセスを要求したユーザー、どのようなアクセスが許可されました、およびどのようなアクティビティが実行されたを識別します。  
  
**要件**  
  
-   Microsoft Identity Manager  
  
-   Active Directory フォレストの機能レベルを Windows Server 2012 R2 またはそれ以降。  
  
## <a name="BKMK_AzureADJoin"></a>Azure AD に参加させる  
Azure Active Directory への参加、enterprise、ビジネスおよび EDU お客様の企業と個人のデバイス用の強化された機能を備えたの identity エクスペリエンスが向上します。  
  
利点:  
  
-   **モダン設定の可用性**corp が所有する Windows デバイスでします。 酸素サービス個人用 Microsoft アカウントが必要なくなった: ユーザーの既存の職場アカウントを順守するため無効実行できるようになりました。 酸素サービスは、内部設置型 Windows ドメインに参加している Pc、Pc やデバイスに"に参加している"(「クラウド ドメイン」)、Azure AD テナント動作します。 これらの設定は次のとおりです。  
  
    -   ローミングまたは個人設定]、アクセシビリティの設定と資格情報  
  
    -   バックアップと復元  
  
    -   職場アカウントを Microsoft ストアへのアクセス  
  
    -   ライブ タイルや通知  
  
-   **組織のリソースにアクセス**モバイル デバイス (電話、ファブレット corp 所有しているかどうかを Windows ドメインに参加できない) または BYOD  
  
-   **シングル サイン オン**Office 365 とその他の組織のアプリ、Web サイトとリソースにします。  
  
-   **BYOD デバイスで**(、オンプレミスのドメインまたは Azure AD) から個人所有のデバイスに職場アカウントを追加し、条件付きのアカウントの制御とデバイスの正常性構成証明などの新しい機能を遵守を確実な方法で仕事用リソースと、Web でのアプリ経由への SSO を利用します。  
  
-   **MDM 統合**デバイス (Intune またはサード パーティ製)、MDM の自動登録することができます  
  
-   **「キオスク」モードを設定し、デバイスを共有**、組織内の複数のユーザー  
  
-   **開発者のエクスペリエンス**企業と個人のコンテキストを共有プログラミング スタックの両方に対応するアプリを作成できます。  
  
-   **イメージング**オプションを使用して、最初の実行エクスペリエンス中に直接 corp が所有するデバイスを構成するイメージングと、ユーザーを許可するのかを選択できます。  
  
詳細については、「[企業向けの Windows 10: 作業用デバイスを使用する方法は](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1)します。  
  
## <a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport では、キー ベースの認証を新しい組織やコンシューマーにパスワードを超えるアプローチです。 この形式の認証は、違反、盗難、およびフィッシングにくい資格情報に依存します。  
  
証明書または非対称キーのペアにリンクされている情報上の生体認証または PIN ログにユーザーがデバイスにログオンします。 Id プロバイダー (Idp) は、ユーザーの公開キーを IDLocker にマップすることによってユーザーを検証し、1 時間パスワード (OTP)、Phonefactor または異なる通知メカニズムを使用して情報をログを提供します。  
  
詳細については、「[Microsoft Passport を使用してパスワードを使わない ID 認証](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport/)  
  
## <a name="BKMK_FRSDeprecation"></a>ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルの廃止  
ファイル レプリケーション サービス (FRS) と Windows Server 2003 の機能レベルは、Windows Server の以前のバージョンで廃止されましたが Windows Server 2003 オペレーティング システムがサポートされている不要になったことを繰り返しを負いません。 その結果、Windows Server 2003 を実行している任意のドメイン コントローラーをドメインから削除する必要があります。 ドメインとフォレストの機能レベルは、発生するには、少なくとも、環境に追加されない以前のバージョンの Windows Server を実行するドメイン コントローラーを防ぐために Windows Server 2008 します。  
  
Windows Server 2008 とより高いドメイン機能レベルでは、分散ファイル サービス (DFS) レプリケーションを使用してドメイン コントローラー間で SYSVOL フォルダーの内容をレプリケートします。 Windows Server 2008 ドメインの機能レベルが以上に新しいドメインを作成する場合、DFS レプリケーションは自動的に SYSVOL をレプリケートする使用します。 低い機能レベルでドメインを作成した場合は、SYSVOL の DFS レプリケーションに FRS を使用してから移行する必要があります。 移行手順については、いずれかのフォローできます、 [TechNet の「手順](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)または参照することができます、[一連の記憶域チーム File Cabinet ブログ手順を合理化](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)します。  
  
Windows Server 2003 のドメインとフォレストの機能レベルは引き続きサポートされますが、組織が Windows Server 2008 (または可能であれば、高い) の機能レベルを上げる必要がありますを SYSVOL レプリケーションの互換性を確保し、将来的にサポートします。 さらがあるその他の多くの利点と機能、上位の機能レベルでより高い。 詳細については、次のリソースを参照してください。  
  
-   [サービス (AD DS) の機能レベルの Active Directory ドメインを理解します。](ad-ds/active-directory-functional-levels.md)  
  
-   [ドメインの機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)  
  
