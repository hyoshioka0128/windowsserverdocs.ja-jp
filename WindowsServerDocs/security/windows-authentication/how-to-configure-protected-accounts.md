---
title: 保護されるアカウントの構成方法
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 28296b588c87bddb0364b9c3e10ad443870dc52f
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266823"
---
# <a name="how-to-configure-protected-accounts"></a>保護されるアカウントの構成方法

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Pass-the-hash (PtH) 攻撃では、攻撃者はユーザーのパスワード (または他の資格情報の派生物) の基盤となる NTLM ハッシュを使用して、リモートのサーバーまたはサービスに対する認証を行うことができます。 マイクロソフトは以前に、Pass-the-Hash 攻撃を軽減させるための [ガイダンスを公開](https://www.microsoft.com/download/details.aspx?id=36036) しています。  Windows Server 2012 R2 には、さらに、このような攻撃を軽減するために新しい機能が含まれています。 資格情報の盗用を防ぐのに役立つ、その他のセキュリティ機能の詳細については、「 [資格情報の保護と管理](https://technet.microsoft.com/library/dn408190.aspx)」を参照してください。 このトピックでは、次の新機能を構成する方法を説明します。  
  
-   [保護されているユーザー](#protected-users)  
  
-   [認証ポリシー](#authentication-policies)  
  
-   [認証ポリシー サイロ](#authentication-policy-silos)  
  
Windows 8.1 および Windows Server 2012 R2 には、資格情報の盗用を防ぐために役立つ追加の軽減機能が内蔵されています。これらの機能については、以下のトピックで説明しています。  
  
-   [リモート デスクトップの制限付き管理モード](http://blogs.technet.com/b/kfalde/archive/20../restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)  
  
-   [LSA の保護](https://technet.microsoft.com/library/dn408187)  
  
## <a name="protected-users"></a>Protected Users  
Protected Users は、新しいユーザーや既存のユーザーを追加できる新しいグローバル セキュリティ グループです。 Windows 8.1 デバイスおよび Windows Server 2012 R2 ホストの資格情報の盗用に対する保護を強化するには、このグループのメンバーを持つ特別な動作があります。 グループのメンバー、または Windows Server 2012 R2 ホストの Windows 8.1 デバイスをキャッシュしません Protected Users に対するサポートされていない資格情報。 このグループのメンバーの場合、追加の保護があるいない Windows 8.1 より前のバージョンの Windows を実行しているデバイスにログオンしている場合。  
  
ユーザーがサインオンした Windows 8.1 デバイスに Protected Users のメンバーをグループ化し、Windows Server 2012 R2 ホストできる *不要になった* を使用します。  
  
-   既定の資格情報の委任 (CredSSP) - プレーンテキストの資格情報は、 **[既定の資格情報の委任を許可する]** ポリシーが有効な場合でもキャッシュされません  
  
-   Windows ダイジェスト - プレーンテキストの資格情報はそれらが有効な場合でもキャッシュされません  
  
-   NTLM - NTOWF はキャッシュされません  
  
-   Kerberos 長期キー - Kerberos チケット保証チケット (TGT) はログオン時に取得され、自動で再取得することはできません  
  
-   オフラインでのサインオン - キャッシュされたログオン検証は作成されません  
  
ドメインの機能レベルが Windows Server 2012 R2 の場合は、不要になったグループのメンバーが実行できます。  
  
-   NTLM 認証を使用した認証  
  
-   Kerberos 事前認証におけるデータ暗号化標準 (DES) または RC4 暗号スイートの使用  
  
-   制約なし/制約付き委任を使用した委任  
  
-   最初の 4 時間の有効期間後のユーザー チケット (TGT) の更新  
  
使用することができます、グループにユーザーを追加する[UI ツール](https://technet.microsoft.com/library/cc753515.aspx)など、Active Directory 管理センター (ADAC) または Active Directory ユーザーとコンピューター、またはコマンド ライン ツールなど[Dsmod グループ](https://technet.microsoft.com/library/cc732423.aspx)、または、WindowsPowerShell [Add-adgroupmember](https://technet.microsoft.com/library/ee617210.aspx)コマンドレット。 サービスとコンピューターのアカウントは、Protected Users グループのメンバーに*しないでください*。 これらのアカウントのメンバーシップでは、パスワードまたは証明書が常にホストで利用できるため、ローカル保護が提供されません。  
  
> [!WARNING]  
> 認証の制限には回避策はありません。つまり、Enterprise Admins グループや Domain Admins グループのように高い権限を持つグループのメンバーであっても、Protected Users グループの他のメンバーと同じ制限が適用されます。 そのような高い権限を持つグループのすべてのメンバーが Protected Users グループに追加されると、それらのアカウントがすべてロックアウトされる可能性があります。潜在的な影響についての十分なテストが完了するまで、高い権限を持つすべてのアカウントを Protected Users グループに追加することは避けてください。  
  
Protected Users グループのメンバーは、Kerberos で高度暗号化標準 (AES) を使用して認証できる必要があります。 この方法では、Active Directory のアカウントに対する AES キーが必要です。 パスワードが Windows Server 2008 を実行するドメイン コント ローラーに変更されたか、後でない限り、組み込みの管理者は AES キーを持ちません。 また、以前のバージョンの Windows Server が実行されているドメイン コントローラーでパスワードを変更したアカウントはロックアウトされます。そのため、次のベスト プラクティスに従ってください。  
  
-   テストしていないドメインにしない限り、 **2008 またはそれ以降、すべてのドメイン コント ローラーが Windows Server を実行**します。  
  
-   ドメインの**作成前**に作成されたすべてのドメイン アカウントの*パスワードを変更*してください。 そうしないと、これらのアカウントを認証できません。  
  
-   **パスワードの変更** アカウントを Protected Users に追加する前にユーザーごとにグループ化や、パスワードが Windows Server 2008 を実行するドメイン コント ローラーで最近変更された、またはそれ以降であることを確認します。  
  
### <a name="requirements-for-using-protected-accounts"></a>保護されたアカウントを使用するための要件  
保護されたアカウントを展開するには、次の要件があります。  
  
-   Protected Users に対するクライアント側の制限を提供するには、ホストは Windows 8.1 または Windows Server 2012 R2 を実行する必要があります。 ユーザーは、Protected Users グループのメンバーであるアカウントのみを使用してサインオンする必要があります。 Protected Users グループを作成してこの場合、 [プライマリ ドメイン コント ローラー (PDC) エミュレーターの役割を転送する](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) Windows Server 2012 R2 を実行しているドメイン コント ローラーにします。 そのグループのオブジェクトが他のドメイン コントローラーにレプリケートされた後に、以前のバージョンの Windows Server が実行されているドメイン コントローラーで PDC エミュレーターの役割をホストできます。  
  
-   NTLM 認証の使用を制限するのには、Protected Users に対するドメイン コント ローラー側の制限とその他の制限を提供するには、Windows Server 2012 R2 がドメインの機能レベルにあります。 機能レベルの詳細については、「 [AD DS の機能レベルとは](../../identity/ad-ds/active-directory-functional-levels.md)」をご覧ください。  
  
### <a name="troubleshoot-events-related-to-protected-users"></a>Protected Users に関連するイベントのトラブルシューティング  
このセクションでは、Protected Users に関連するイベントのトラブルシューティングに役立つ新しいログについて説明します。さらに、チケット保証チケット (TGT) の有効期限または委任に関する問題のいずれかのトラブルシューティングを行う際に、Protected Users がどのような影響を与えるかを説明します。  
  
#### <a name="new-logs-for-protected-users"></a>Protected Users 向けの新しいログ  
2 つの新しい運用管理ログを使用して、Protected Users に関連するイベントのトラブルシューティングに役立てることができます。ユーザー - クライアントのログと Protected User Failures - ドメイン コント ローラーのログを保護します。 これらの新しいログはイベント ビューアーにありますが、既定では無効になっています。 ログを有効化するには、 **[アプリケーションとサービス ログ]** 、 **[Microsoft]** 、 **[Windows]** 、 **[Authentication]** の順にクリックし、ログの名前をクリックして **[操作]** をクリックし (またはログを右クリック)、 **[ログの有効化]** をクリックします。  
  
これらのログのイベント詳細については、「 [認証ポリシーと認証ポリシー サイロ](https://technet.microsoft.com/library/dn486813.aspx)」をご覧ください。  
  
#### <a name="troubleshoot-tgt-expiration"></a>TGT の有効期限のトラブルシューティング  
通常、ドメイン コントローラーは、次の [グループ ポリシー管理エディター] ウィンドウに表示されるドメイン ポリシーに基づいて、TGT の有効期間と更新を設定します。  
  
![TGT の有効期間と更新ドメイン ポリシーに基づいて、ドメイン コント ローラーを設定する方法を示すグループ ポリシー管理エディター ウィンドウのスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
**Protected Users** の場合、次の設定がハードコーディングされています。  
  
-   ユーザー チケットの最長有効期間:240 分  
  
-   ユーザー チケット更新の最長有効期間:240 分  
  
#### <a name="troubleshoot-delegation-issues"></a>委任に関する問題のトラブルシューティング  
以前は、Kerberos 委任を使用するテクノロジで問題が発生すると、クライアント アカウントに **[アカウントは重要なので委任できない]** が設定されているかどうかを確認していました。 しかし、アカウントが **Protected Users** のメンバーである場合、この設定は Active Directory 管理センター (ADAC) で構成されていない可能性があります。 そのため、委任に関する問題のトラブルシューティングを行う場合は、この設定だけでなくグループ メンバーシップも確認してください。  
  
![スクリーン ショットを確認する場所を示す * * アカウントは重要なので委任できない * * UI 要素](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
### <a name="audit-authentication-attempts"></a>認証試行の監査  
**Protected Users** グループのメンバーの認証試行を明示的に監査するには、セキュリティ ログの監査イベントを引き続き収集するか、または新しい運用管理ログのデータを収集します。 これらのイベント詳細については、「 [認証ポリシーと認証ポリシー サイロ](https://technet.microsoft.com/library/dn486813.aspx)」をご覧ください。  
  
### <a name="provide-dc-side-protections-for-services-and-computers"></a>サービスとコンピューターに対して DC 側の保護を提供する  
サービスおよびコンピューター用のアカウントは、**Protected Users** のメンバーにすることはできません。 このセクションでは、これらのアカウントに提供できるドメイン コントローラー ベースの保護について説明します。  
  
-   NTLM 認証の拒否:経由でのみ構成可能な[NTLM ブロック ポリシー](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)します。  
  
-   Kerberos 事前認証でのデータ暗号化標準 (DES) の拒否:Kerberos と共にリリースされた Windows のすべてのバージョンは、RC4 もサポートしています。 理由だけ des 構成されている場合を除き、Windows Server 2012 R2 のドメイン コント ローラーは、コンピューター アカウントで DES を許可されません。  
  
-   Kerberos 事前認証での RC4 の拒否: 構成できません。  
  
    > [!NOTE]  
    > [サポートされている暗号化の種類の構成を変更する](http://blogs.msdn.com/b/openspecification/archive/20../windows-configurations-for-kerberos-supported-encryption-type.aspx)ことはできますが、コンピューター アカウントでこれらの設定を変更する場合は、あらかじめターゲット環境でテストすることをお勧めします。  
  
-   ユーザー チケット (TGT) を最初の 4 時間の有効期間に制限:認証ポリシーを使用します。  
  
-   制約なし/制約付き委任による委任を拒否:アカウントを制限するには、Active Directory 管理センター (ADAC) を開いて、 **[アカウントは重要なので委任できない]** チェック ボックスをオンにします。  
  
    ![アカウントを制限する場所を示すスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
## <a name="authentication-policies"></a>認証ポリシー  
認証ポリシーは AD DS の新しいコンテナーで、認証ポリシー オブジェクトが含まれています。 認証ポリシーを使用すると、資格情報が盗用される可能性を軽減するのに役立つ設定を指定することができます。たとえば、アカウントの TGT の有効期間を制限したり、その他の要求関連の条件を追加できます。  
  
Windows Server 2012 では、ダイナミック アクセス制御には、組織全体でファイル サーバーを構成する簡単な方法を提供する集約型アクセス ポリシーと呼ばれる Active Directory フォレスト スコープ オブジェクトのクラスが導入されました。 Windows Server 2012 r2、Windows Server 2012 R2 のドメイン内のアカウント クラスに認証の構成を適用する認証ポリシー (objectClass Msds-authnpolicies) と呼ばれる新しいオブジェクト クラスを使用できます。 次の Active Directory アカウント クラスがあります。  
  
-   ユーザー  
  
-   コンピューター  
  
-   管理されたサービス アカウントおよびグループの管理されたサービス アカウント (GMSA)  
  
### <a name="quick-kerberos-refresher"></a>クイック Kerberos リフレッシャー  
Kerberos 認証プロトコルは、次の 3 種類の交換 (サブプロトコルとも呼ばれます) で構成されます。  
  
![次の 3 つの種類の Kerberos 認証プロトコルの交換、サブプロトコルとも呼ばれますを示すスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbRefresher.gif)  
  
-   認証サービス (AS) 交換 (KRB_AS_*)  
  
-   チケット保証サービス (TGS) 交換 (KRB_TGS_*)  
  
-   クライアント/サーバー (AP) 交換 (KRB_AP_*)  
  
AS 交換は、チケット保証チケット (TGT) を要求する事前認証子を作成する、クライアントが、アカウントのパスワードまたは秘密キーを使用する場所です。 これは、ユーザーのサインオン時や、サービス チケットを初めて必要とする場合に発生します。  
  
TGS 交換では、サービス チケットを要求する認証子を作成するアカウントの TGT が使用されています。 これは、認証済みの接続が必要な場合に発生します。  
  
AP 交換は通常、アプリケーション プロトコル内部のデータとして発生し、認証ポリシーの影響を受けません。  
  
詳細については、「 [Kerberos バージョン 5 認証プロトコルの動作](https://technet.microsoft.com/library/cc772815(v=WS.10.aspx))」をご覧ください。  
  
### <a name="overview"></a>概要  
認証ポリシーは、アカウントに対して構成可能な制限を適用する方法を提供し、サービスおよびコンピューター用のアカウントにも制限を提供することで、Protected Users を補完します。 認証ポリシーは、AS 交換または TGS 交換の間に適用されます。  
  
次の設定を構成することで、最初の認証または AS 交換を制限できます。  
  
-   TGT の有効期間  
  
-   ユーザーのサインオンを制限するアクセス制御条件。AS 交換が発生するデバイスでこの条件を満たす必要があります  
  
![TGT の有効期間とアクセス制御条件をユーザーのサインオンに制限を構成することで、最初の認証を制限する方法を示すスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictAS.gif)  
  
次の設定を構成することで、チケット保証サービス (TGS) 交換を通じたサービス チケット要求を制限できます。  
  
-   クライアント (ユーザー、サービス、コンピューター) または TGS 交換が発生するデバイスで満たす必要があるアクセス制御条件  
  
### <a name="requirements-for-using-authentication-policies"></a>認証ポリシーを使用するための要件  
  
|ポリシー|必要条件|  
|-----|--------|  
|TGT の有効期間のカスタマイズ| Windows Server 2012 R2 のドメイン機能レベルのアカウント ドメイン|  
|ユーザー サインオンの制限|-ダイナミック アクセス制御のサポート Windows Server 2012 R2 のドメイン機能レベルのアカウント ドメイン<br />-Windows 8、Windows 8.1、Windows Server 2012 または Windows Server 2012 R2 のデバイスでダイナミック アクセス制御をサポートします。|  
|ユーザー アカウントとセキュリティ グループに基づくサービス チケット発行の制限| Windows Server 2012 R2 のドメイン機能レベルのリソース ドメイン|  
|ユーザー要求またはデバイス アカウント、セキュリティ グループ、または要求に基づくサービス チケット発行の制限| Windows Server 2012 R2 のドメイン機能レベルのリソース ドメインでダイナミック アクセス制御のサポート|  
  
### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>ユーザー アカウントを特定のデバイスおよびホストに制限する  
管理権限を持つ重要なアカウントは、**Protected Users** グループのメンバーである必要があります。 既定では、 **Protected Users** グループのメンバーになっているアカウントはありません。 このグループにアカウントを追加する前に、ドメイン コントローラーのサポートを構成し、障害となるような問題がないことを保証するための監査ポリシーを作成してください。  
  
#### <a name="configure-domain-controller-support"></a>ドメイン コントローラーのサポートを構成する  
ユーザーのアカウント ドメインは、Windows Server 2012 R2 のドメイン機能レベル (DFL) にする必要があります。 すべてのドメイン コント ローラーは、Active Directory ドメインと信頼関係を使用して、Windows Server 2012 R2 では、ように [dfl](https://technet.microsoft.com/library/cc753104.aspx) Windows Server 2012 R2 にします。  
  
**ダイナミック アクセス制御のサポートを構成するには**  
  
1.  既定のドメイン コントローラー ポリシーで、[コンピューターの構成]、[管理用テンプレート]、[システム]、[KDC] の順に展開し、 **[有効]** をクリックして **[要求、複合認証、および Kerberos 防御のキー配布センター (KDC) クライアント サポート]** を有効化します。  
  
    ![既定のドメイン コント ローラー ポリシー をクリックして **有効** 有効にする **信頼性情報、複合認証および Kerberos 防御のキー配布センター KDC クライアント サポート**コンピューターの構成 |管理用テンプレート |システム |KDC](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)  
  
2.  **[オプション]** のドロップダウン リスト ボックスで、 **[常に信頼性情報を提供する]** を選択します。  
  
    > [!NOTE]  
    > **サポートされている** も構成することができますが、ドメインは Dc を常にも、Windows Server 2012 R2 DFL にあるためクレームを使用するユーザー クレームに基づくアクセス確認を要求に非対応するデバイスを使用する場合に行うし、要求対応のサービスに接続するホストを提供します。  
  
    ![* * オプション * *、ドロップダウン リスト ボックスで、選択 * * 常に信頼性情報を提供](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)  
  
    > [!WARNING]  
    > 構成する **防御されていない認証要求を失敗** Windows 7 およびそれ以前のオペレーティング システムなどの Kerberos 防御をサポートしていない任意のオペレーティング システムまたは Windows 8 は、サポートするように明示的に構成されていないから始まるオペレーティング システムから認証エラーが発生します。  
  
#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>認証ポリシーのユーザー アカウント監査を ADAC で作成する  
  
1.  Active Directory 管理センター (ADAC) を開きます。  
  
    ![Active Directory 管理センターを示すスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_OpenADAC.gif)  
  
    > [!NOTE]  
    > 選択した **認証** ノードがドメインに Windows Server 2012 R2 DFL で表示します。 ノードが表示されない場合、もう一度やり直して Windows Server 2012 R2 DFL にあるドメインからドメイン管理者アカウントを使用しています。  
  
2.  **[認証ポリシー]** をクリックし、 **[新規]** をクリックして新しいポリシーを作成します。  
  
    ![Authentication Policies](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)  
  
    認証ポリシーには、既定で適用される表示名が必要です。  
  
3.  監査のみのポリシーを作成するには、 **[監査ポリシーの制限のみ]** をクリックします。  
  
    ![監査ポリシーの制限のみ](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)  
  
    認証ポリシーは、Active Directory のアカウントの種類に基づいて適用されます。 それぞれの種類に対する設定を構成することで、1 つのポリシーを 3 つのアカウントの種類すべてに適用できます。 次のアカウントの種類があります。  
  
    -   ユーザー  
  
    -   コンピューター  
  
    -   管理されたサービス アカウントおよびグループの管理されたサービス アカウント  
  
    キー配布センター (KDC) で使用できる新しいプリンシパルでスキーマを拡張した場合、新しいアカウントの種類は、最も近い派生アカウントの種類から分類されます。  
  
4.  ユーザー アカウントの TGT の有効期間を構成するには、 **[ユーザー アカウントのチケット保証チケットの有効期間を指定します]** チェック ボックスをオンにして、時間を分単位で入力します。  
  
    ![ユーザー アカウントのチケット保証チケットの有効期間を指定します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTLifetime.gif)  
  
    たとえば、TGT の最長有効期間を 10 時間にする場合は、画面に示すように「**600**」と入力します。 TGT の有効期間を構成しない場合、アカウントが **Protected Users** グループのメンバーであれば、TGT の有効期間および更新は 4 時間に設定されます。 そうでない場合、TGT の有効期間および更新はドメイン ポリシーによって異なります。例として、あるドメインの既定の設定が表示されている [グループ ポリシー管理エディター] ウィンドウを次に示します。  
  
    ![既定の設定で、ドメインのグループ ポリシー管理エディター ウィンドウ](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
5.  ユーザー アカウントを選択したデバイスに制限するには、 **[編集]** をクリックし、デバイスで必要な条件を定義します。  
  
    ![デバイスを選択するユーザー アカウントを制限する をクリックして * * 編集 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)  
  
6.  **[アクセス制御条件の編集]** ウィンドウで、 **[条件の追加]** をクリックします。  
  
    ![アクセス制御条件を編集します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCondition.png)  
  
##### <a name="add-computer-account-or-group-conditions"></a>コンピューター アカウントまたはグループの条件を追加する  
  
1.  コンピューター アカウントまたはグループを構成するには、ドロップダウン リストで **[次のそれぞれに所属する]** を選択し、 **[次のいずれかに所属する]** に変更します。  
  
    ![コンピューター アカウントまたはグループを構成します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompMember.png)  
  
    > [!NOTE]  
    > このアクセス制御では、ユーザーのサインオン元のデバイスまたはホストの条件を定義します。 アクセス制御の用語では、デバイスまたはホストのコンピューター アカウントはユーザーと呼ばれるため、選択できるオプションは **[ユーザー]** のみです。  
  
2.  **[項目の追加]** をクリックします。  
  
    ![項目を追加します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddItems.png)  
  
3.  オブジェクトの種類を変更するには、 **[オブジェクトの種類]** をクリックします。  
  
    ![オブジェクトの種類](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjects.gif)  
  
4.  Active Directory 内のコンピューター オブジェクトを選択するには、 **[コンピューター]** をクリックし、 **[OK]** をクリックします。  
  
    ![コンピューター](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)  
  
5.  ユーザーを制限するコンピューターの名前を入力し、 **[名前の確認]** をクリックします。  
  
    ![名前のチェックをクリックします。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)  
  
6.  [OK] をクリックし、コンピューター アカウントに対するその他の条件があれば作成します。  
  
    ![[Ok] をクリックし、コンピューター アカウントの他の条件を作成します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddConditions.png)  
  
7.  完了したら、 **[OK]** をクリックすると、コンピューター アカウントに対する定義済みの条件が表示されます。  
  
    ![完了 をクリックして * * ok * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompDone.png)  
  
##### <a name="add-computer-claim-conditions"></a>コンピューターの要求の条件を追加する  
  
1.  コンピューターの要求を構成するには、[グループ] ドロップダウン リストで要求を選択します。  
  
    ![でコンピューターの要求を構成するには、グループ ドロップダウン リストを、要求を選択します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaim.gif)  
  
    フォレストにプロビジョニング済みの要求のみを使用できます。  
  
2.  ユーザー アカウントのサインオンを制限する OU の名前を入力します。  
  
    ![ユーザー アカウントのサインオンを制限する OU の名前を入力します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimOUName.gif)  
  
3.  完了したら、[OK] をクリックすると、定義済みの条件が表示されます。  
  
    ![終了したら、[ok] をクリック](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimComplete.gif)  
  
##### <a name="troubleshoot-missing-computer-claims"></a>コンピューターの要求が見つからない場合のトラブルシューティング  
プロビジョニング済みの要求を使用できない場合、 **[コンピューター]** クラスに対してのみ構成されている可能性があります。  
  
たとえばを組織単位 (OU) に基づく認証を制限したいが限り、構成されているコンピューターの **コンピューター** クラスです。  
  
![コンピューターの組織単位 (OU) に基づく認証を制限する方法を示すスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictComputers.gif)  
  
要求を使用してユーザーのデバイスへのサインオンを制限できるようにするには、 **[ユーザー]** チェック ボックスをオンにします。  
  
![選択を確認して、デバイスへのサインオンにユーザーを制限する方法を示すスクリーン ショット * * * * ユーザー。  ](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)  
  
#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>ADAC で認証ポリシーをユーザー アカウントにプロビジョニングする  
  
1.  **[ユーザー]** アカウントで、 **[ポリシー]** をクリックします。  
  
    ![* * * * ユーザー アカウント、をクリックして * * * * ポリシー](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicy.gif)  
  
2.  **[このアカウントに認証ポリシーを割り当てます]** チェック ボックスをオンにします。  
  
    ![選択、* * アカウント * * チェック ボックスの認証ポリシーを割り当てる](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)  
  
3.  ユーザーに適用する認証ポリシーを選択します。  
  
    ![ユーザーに適用する認証ポリシーを選択します。](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicySelect.png)  
  
#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>デバイスおよびホストでダイナミック アクセス制御のサポートを構成する  
ダイナミック アクセス制御 (DAC) を構成しなくても、TGT の有効期間を構成することができます。 DAC が必要となるのは、AllowedToAuthenticateFrom および AllowedToAuthenticateTo を確認する場合のみです。  
  
グループ ポリシー エディターまたはローカル グループ ポリシー エディターを使用して、[コンピューターの構成]、[管理用テンプレート]、[システム]、[Kerberos] の順に展開し、 **[要求、複合認証、および Kerberos 防御の Kerberos クライアント サポート]** を有効化します。  
  
![グループ ポリシーまたはローカル グループ ポリシー エディターを使用して有効にする方法を示すスクリーン ショット * * 信頼性情報、複合認証および Kerberos 防御の Kerberos クライアント サポート * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)  
  
### <a name="troubleshoot-authentication-policies"></a>認証ポリシーのトラブルシューティング  
  
#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>認証ポリシーが直接割り当てられたアカウントの特定  
認証ポリシーの [アカウント] セクションには、ポリシーが直接適用されたアカウントが表示されます。  
  
![ポリシーが直接適用されたアカウントを示す認証ポリシーの [アカウント] セクションのスクリーン ショット](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AccountsAssigned.gif)  
  
#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Authentication Policy Failures - Domain Controller 管理ログの使用します。  
新しい **Authentication Policy Failures - ドメイン コント ローラー** 下にある管理ログ **アプリケーションとサービス ログ** > **Microsoft** > **Windows** > **認証** 、により、認証ポリシーのエラーを検出する容易に作成されました。 このログは、既定では無効になっています。 有効にするには、ログの名前を右クリックし、 **[ログの有効化]** をクリックします。 新しいイベントは、既存の Kerberos TGT やサービス チケットの監査イベントの内容とよく似ています。 これらのイベント詳細については、「 [認証ポリシーと認証ポリシー サイロ](https://technet.microsoft.com/library/dn486813.aspx)」をご覧ください。  
  
### <a name="manage-authentication-policies-by-using-windows-powershell"></a>Windows PowerShell を使用した認証ポリシーの管理  
次のコマンドは、**TestAuthenticationPolicy** という名前の認証ポリシーを作成します。 **UserAllowedToAuthenticateFrom** パラメーターは、ユーザーが someFile.txt という名前のファイルに含まれる SDDL 文字列によって認証できるデバイスを指定します。  
  
```  
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl  
```  
  
次のコマンドは、 **Filter** パラメーターで指定されるフィルターと一致するすべての認証ポリシーを取得します。  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com  
  
```  
  
次のコマンドは、指定された認証ポリシーの Description および **UserTGTLifetimeMins** プロパティを変更します。  
  
```  
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45  
```  
  
次のコマンドは、**Identity** パラメーターで指定される認証ポリシーを削除します。  
  
```  
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1  
```  
  
次のコマンドは、 **Get-ADAuthenticationPolicy** コマンドレットで **Filter** パラメーターを使用し、適用されていない認証ポリシーをすべて取得します。 結果セットは、パイプを使用して **Remove-ADAuthenticationPolicy** コマンドレットに渡されます。  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy  
```  
  
## <a name="authentication-policy-silos"></a>認証ポリシー サイロ  
認証ポリシー サイロは、ユーザー、コンピューター、およびサービス アカウント向けの AD DS 内の新しいコンテナー (objectClass msDS-AuthNPolicySilos) です。 このコンテナーは、重要なアカウントを保護するのに役立ちます。 すべての組織は、Enterprise Admins、Domain Admins、および Schema Admins グループのメンバーを保護する必要があります。攻撃者がフォレスト内にアクセスするためにこれらのアカウントを使用する可能性があるためです。その一方で、その他のアカウントも保護が必要になる場合があります。  
  
一部の組織では、ワークロードを分離するために、ワークロードに固有のアカウントを作成し、ローカルおよびリモートの対話型ログオンと管理者特権を制限するグループ ポリシー設定を適用しています。 認証ポリシー サイロは、ユーザー、コンピューター、および管理されたサービス アカウント間の関係を定義する方法を作成することで、このような作業を補完します。 アカウントが所属できるのは 1 つのサイロのみです。 それぞれのアカウントの種類に対して認証ポリシーを構成することで、次の項目を制御できます。  
  
1.  更新不可の TGT の有効期間  
  
2.  TGT を返すためのアクセス制御条件 (注: Kerberos 防御が必須であるため、システムに適用することはできません)  
  
3.  サービス チケットを返すためのアクセス制御条件  
  
また、認証ポリシー サイロのアカウントにはサイロ要求があり、ファイル サーバーなど、要求に対応するリソースでアクセス制御を行うために使用できます。  
  
サービス チケットの発行を制御するために、次の情報に基づいて新しいセキュリティ記述子を構成できます。  
  
-   ユーザー、ユーザーのセキュリティ グループ、またはユーザーの要求  
  
-   デバイス、デバイスのセキュリティ グループ、およびデバイスの要求  
  
リソースの Dc には、この情報を取得するには、ダイナミック アクセス制御が必要です。  
  
-   ユーザー要求:  
  
    -   ダイナミック アクセス制御をサポートする Windows 8 以降のクライアント  
  
    -   ダイナミック アクセス制御と要求をサポートするアカウント ドメイン  
  
-   デバイスおよびデバイス セキュリティ グループ:  
  
    -   ダイナミック アクセス制御をサポートする Windows 8 以降のクライアント  
  
    -   複合認証用に構成されたリソース  
  
-   デバイス要求:  
  
    -   ダイナミック アクセス制御をサポートする Windows 8 以降のクライアント  
  
    -   ダイナミック アクセス制御と要求をサポートするデバイス ドメイン  
  
    -   複合認証用に構成されたリソース  
  
認証ポリシーは、個々のアカウントに適用する代わりに、認証ポリシー サイロのすべてのメンバーに適用できます。また、サイロ内の異なるアカウントの種類に個別の認証ポリシーを適用することもできます。 たとえば、ある認証ポリシーを高い権限を持つユーザー アカウントに適用し、別のポリシーをサービス アカウントに適用できます。 認証ポリシー サイロを作成するには、事前に少なくとも 1 つの認証ポリシーを作成する必要があります。  
  
> [!NOTE]  
> 認証ポリシーは、認証ポリシー サイロのメンバーに適用できますが、サイロとは無関係に適用して特定のアカウント スコープを制限することもできます。 たとえば、1 つのアカウントまたは少数のアカウント セットを保護するため、それらのアカウントをサイロに追加せずに、ポリシーを直接設定できます。  
  
認証ポリシー サイロを作成するには、Active Directory 管理センターまたは Windows PowerShell を使用します。 既定では、認証ポリシー サイロのみサイロ ポリシーの監査を指定することと同じ、 **WhatIf** Windows PowerShell コマンドレットのパラメーターです。 この場合、ポリシー サイロの制限は適用されませんが、監査が生成され、制限が適用された場合にエラーが発生するかどうかが示されます。  
  
#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Active Directory 管理センターを使用して認証ポリシー サイロを作成するには  
  
1.  **Active Directory 管理センター**を開き、 **[認証]** をクリックして **[認証ポリシー サイロ]** を右クリックし、 **[新規]** 、 **[認証ポリシー サイロ]** の順にクリックします。  
  
    ![開いている * * Active Directory 管理センター * *、 をクリックして * * * *、認証を右クリックして * * 認証ポリシー サイロ * *、 をクリックして * * * *、新規をクリック * * 認証ポリシー サイロ * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)  
  
2.  **[表示名]** にサイロの名前を入力します。 **[許可されたアカウント]** で **[追加]** をクリックし、アカウントの名前を入力して、 **[OK]** をクリックします。 ユーザー、コンピューター、またはサービス アカウントを指定できます。 次に、すべてのプリンシパルに 1 つのポリシーを使用するか、またはそれぞれのプリンシパルの種類に個別のポリシーを使用するかを指定して、ポリシーの名前を指定します。  
  
    ![* * * * 名前を表示、サイロの名前を入力します。 [* * 許可されているアカウント * *、] をクリックして * * * *、追加、アカウントの名前を入力し、をクリックし、* * * * [ok]](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)  
  
### <a name="manage-authentication-policy-silos-by-using-windows-powershell"></a>Windows PowerShell を使用した認証ポリシー サイロの管理  
次のコマンドは、認証ポリシー サイロ オブジェクトを作成して適用します。  
  
```  
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce  
```  
  
次のコマンドは、**Filter** パラメーターで指定されたフィルターに一致する認証ポリシー サイロをすべて取得します。 出力は **Format-Table** コマンドレットに渡され、ポリシーの名前と各ポリシーの **Enforce** の値が表示されます。  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize  
  
Name  Enforce  
--  ----  
silo     True  
silos   False  
  
```  
  
次のコマンドは、**Get-ADAuthenticationPolicySilo** コマンドレットで **Filter** パラメーターを使用して、適用されていない認証ポリシー サイロをすべて取得し、パイプを使用してフィルターの結果を **Remove-ADAuthenticationPolicySilo** コマンドレットに渡します。  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo  
```  
  
次のコマンドは、*User01* という名前のユーザー アカウントに *Silo* という名前の認証ポリシー サイロへのアクセスを許可します。  
  
```  
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01  
```  
  
次のコマンドは、*User01* という名前のユーザー アカウントの *Silo* という名前の認証ポリシー サイロへのアクセスを取り消します。 **Confirm** パラメーターが **$False** に設定されているため、確認メッセージは表示されません。  
  
```  
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False  
```  
  
次の例では、最初に **Get-ADComputer** コマンドレットを使用して、 **Filter** パラメーターで指定されるフィルターに一致するコンピューター アカウントをすべて取得します。 このコマンドの出力は **Set-ADAccountAuthenticatinPolicySilo** に渡され、*Silo* という名前の認証ポリシー サイロと *AuthenticationPolicy02* という名前の認証ポリシーが割り当てられます。  
  
```  
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02  
```  
  

