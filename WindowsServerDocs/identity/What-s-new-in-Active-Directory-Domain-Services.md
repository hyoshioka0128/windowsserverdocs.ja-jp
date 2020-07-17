---
ms.assetid: 9a06cd41-426f-4cb9-89cf-f5be730e0b79
title: Active Directory Domain Services の新機能
ms.prod: windows-server
ms.technology: active-directory-domain-services
ms.topic: article
author: Femila
ms.author: billmath
ms.date: 05/31/2017
ms.openlocfilehash: 5e58bb229aa8fe02fb20f870a0e922d1aa8c34b7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825645"
---
# <a name="whats-new-in-active-directory-domain-services"></a>Active Directory Domain Services の新機能 

>適用対象: Windows Server 2016

Active Directory Domain Services (AD DS) の次の新機能により、組織は Active Directory 環境を保護し、クラウドのみのデプロイとハイブリッドデプロイに移行できるようになります。一部のアプリケーションとサービスはクラウドでホストされ、他のアプリケーションとサービスはオンプレミスでホストされます。 強化された機能は次のとおりです。  
  
-   [Privileged access management](https://technet.microsoft.com/library/mt150258.aspx   
)  
  
- [Azure Active Directory Join を使用したクラウド機能の Windows 10 デバイスへの拡張](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-overview/)   
  
- [Windows 10 エクスペリエンスのためにドメイン参加済みデバイスを Azure AD に接続する](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-devices-group-policy/)   
  
- [組織内の Microsoft Passport for Work を有効にする](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport-deployment/)    
  
-  [ファイルレプリケーションサービス (FRS) と Windows Server 2003 の機能レベルの廃止](ad-ds/active-directory-functional-levels.md)  
  
  
## <a name="privileged-access-management"></a><a name="BKMK_PAM"></a>Privileged access management  
Privileged access management (PAM) は、ハッシュ、スピアーフィッシング、同様の種類の攻撃など、資格情報の盗難手法によって発生する Active Directory 環境のセキュリティの問題を軽減するのに役立ちます。 Microsoft Identity Manager (MIM) を使用して構成された新しい管理アクセスソリューションを提供します。 PAM の導入:  
  
-   新しい要塞 Active Directory フォレスト。 MIM によってプロビジョニングされます。 要塞フォレストには、既存のフォレストとの特別な PAM 信頼があります。 これにより、悪意のあるアクティビティがないことがわかっている新しい Active Directory 環境が提供され、特権アカウントを使用するために既存のフォレストから分離されます。  
  
-   管理特権を要求する MIM の新しいプロセスと、要求の承認に基づいて新しいワークフローを作成します。  
  
-   管理者特権の要求に応じて、MIM によって要塞フォレストにプロビジョニングされた新しいシャドウセキュリティプリンシパル (グループ)。 シャドウセキュリティプリンシパルには、既存のフォレスト内の管理グループの SID を参照する属性があります。 これにより、シャドウグループは、アクセス制御リスト (Acl) を変更することなく、既存のフォレスト内のリソースにアクセスできるようになります。  
  
-   期限切れのリンク機能。シャドウグループの時間制限のメンバーシップを有効にします。 管理タスクを実行するために必要な時間だけ、ユーザーをグループに追加することができます。 タイムアウトしたメンバーシップは、Kerberos チケットの有効期間に反映される time-to-live (TTL) 値によって表されます。  
  
    > [!NOTE]  
    > 期限切れのリンクは、リンクされているすべての属性で使用できます。 ただし、PAM などの完全なソリューションで、期限切れリンク機能を使用するように事前構成されている唯一の例として、グループとユーザーの間のメンバー/memberOf のリンクされた属性リレーションシップがあります。  
  
-   KDC の機能強化は Active Directory ドメインコントローラーに組み込まれています。これにより、ユーザーが管理グループに複数の時間バインドメンバーシップを持っている場合に Kerberos チケットの有効期限 (TTL) の値を制限することができます。 たとえば、時間にバインドされたグループ A に追加した場合、ログオン時に Kerberos チケット保証チケット (TGT) の有効期間はグループ A の残りの時間と同じになります。また、グループ A よりも TTL が低い別のタイムバインドグループ B のメンバーである場合は、TGT の有効期間はグループ B の残りの時間と同じになります。  
  
-   アクセスの要求者、付与されたアクセス、実行されたアクティビティを簡単に識別できる新しい監視機能。  
  
**必要性**  
  
-   Microsoft Identity Manager  
  
-   Active Directory Windows Server 2012 R2 以降のフォレストの機能レベル。  
  
## <a name="azure-ad-join"></a><a name="BKMK_AzureADJoin"></a>Azure AD 結合  
Azure Active Directory Join を使用すると、企業や個人のデバイスの機能が向上し、enterprise、business、EDU の各顧客の id エクスペリエンスが向上します。  
  
利点:  
  
-   企業所有の Windows デバイスで**最新の設定を利用**できます。 酸素 Services は、個人の Microsoft アカウントを必要としなくなりました。コンプライアンスを確保するために、ユーザーの既存の職場アカウントを使用して実行されるようになりました。 酸素 Services は、オンプレミスの Windows ドメインに参加している Pc と、Azure AD テナント ("クラウドドメイン") に "参加" している Pc とデバイスで動作します。 これらの設定には次のものが含まれます。  
  
    -   ローミングまたは個人用設定、ユーザー補助の設定および資格情報  
  
    -   バックアップと復元  
  
    -   職場アカウントを使用した Microsoft Store へのアクセス  
  
    -   ライブタイルと通知  
  
-   Windows ドメインに参加できないモバイルデバイス (スマートフォン、phablets) の**組織のリソースにアクセス**する (企業所有か byod かにかかわらず)  
  
-   Office 365 およびその他の組織のアプリ、web サイト、リソースに**シングルサイン**オンします。  
  
-   **BYOD デバイスで**は、(オンプレミスのドメインまたは Azure AD から) 個人所有のデバイスに職場アカウントを追加して、条件付きアカウント制御やデバイスの正常性構成証明などの新しい機能に確実に準拠させることができるように、アプリと web で作業リソースの SSO を利用できます。  
  
-   **Mdm 統合**により、デバイスを mdm に自動登録できます (Intune またはサードパーティ)  
  
-   組織内の複数のユーザーに対して **"キオスク" モードと共有デバイスを設定**する  
  
-   **開発者エクスペリエンス**を使用すると、共有されたプログラミングスタックで企業と個人の両方のコンテキストに対応するアプリを構築できます。  
  
-   **イメージング**オプションを使用すると、イメージングを選択し、ユーザーが最初の実行時に企業所有のデバイスを直接構成できるようにすることができます。  
  
詳細については、「[エンタープライズ向け Windows 10: デバイスを仕事に使用する方法](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-windows10-devices-overview/?rnd=1)」を参照してください。  
  
## <a name="microsoft-passport"></a><a name="BKMK_IDLocker"></a>Microsoft Passport  
Microsoft Passport は、パスワードを超えた新しいキーベースの認証方法である組織とコンシューマーです。 この形式の認証では、侵害、盗難、phish のある資格情報に依存しています。  
  
ユーザーは、証明書または非対称キーペアにリンクされている情報を使用して、生体認証または PIN のログを使用してデバイスにログオンします。 Id プロバイダー (IDPs) は、ユーザーの公開キーを Idps にマップし、ワンタイムパスワード (OTP)、または別の通知メカニズムを使用してログオン情報を提供することによって、ユーザーを検証します。  
  
詳細については、「Microsoft Passport によるパスワードを使用し[ない id の認証](https://azure.microsoft.com/documentation/articles/active-directory-azureadjoin-passport/)」を参照してください。  
  
## <a name="deprecation-of-file-replication-service-frs-and-windows-server-2003-functional-levels"></a><a name="BKMK_FRSDeprecation"></a>ファイルレプリケーションサービス (FRS) と Windows Server 2003 の機能レベルの廃止  
ファイルレプリケーションサービス (FRS) と Windows Server 2003 の機能レベルは、以前のバージョンの Windows Server では非推奨とされていましたが、Windows Server 2003 オペレーティングシステムのサポートは終了しています。 その結果として、Windows Server 2003 を実行するすべてのドメイン コントローラーを、ドメインから削除する必要があります。 以前のバージョンの Windows Server を実行しているドメインコントローラーが環境に追加されないようにするには、ドメインとフォレストの機能レベルを少なくとも Windows Server 2008 に上げる必要があります。  
  
Windows Server 2008 以上のドメイン機能レベルでは、分散ファイル サービス (DFS) レプリケーションを使用して、ドメイン コントローラー間で SYSVOL フォルダーの内容をレプリケートします。 Windows Server 2008 ドメイン機能レベル以上で新しいドメインを作成した場合、SYSVOL のレプリケートには DFS レプリケーションが自動的に使用されます。 それより低い低い機能レベルでドメイン作成した場合は、SYSVOL のレプリケーションを FRS から DFS に移行する必要があります。 移行手順については、[TechNet の手順](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)に従うか、[ストレージ チームのファイル キャビネット ブログの合理化された一連の手順](https://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)を参照してください。  
  
Windows Server 2003 のドメインとフォレストの機能レベルは引き続きサポートされますが、SYSVOL レプリケーションの互換性とサポートを将来的に保証するために、機能レベルを Windows Server 2008 (またはそれ以上) に引き上げる必要があります。 さらに、より高い機能レベルで利用可能な他の多くの利点と機能もあります。 詳細については、次のリソースを参照してください。  
  
-   [Active Directory Domain Services (AD DS) の機能レベルについて](ad-ds/active-directory-functional-levels.md)  
  
-   [ドメインの機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
  
-   [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)  
  
