---
ms.assetid: 70c99703-ff0d-4278-9629-b8493b43c833
title: "保護されたアカウントを構成する方法"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4de7b1c9e3d12556f67c4515467bccd124e5e73e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="how-to-configure-protected-accounts"></a>保護されたアカウントを構成する方法

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Pass-the-hash (PtH) 攻撃、によって、攻撃者は、ユーザーのパスワード (またはその他の資格情報の派生物) の基礎となる NTLM ハッシュを使用してリモート サーバーまたはサービスに認証できます。 Microsoft has previously [published guidance](https://www.microsoft.com/download/details.aspx?id=36036) to mitigate pass-the-hash attacks.  Windows Server 2012 R2 には、さらに、このような攻撃を軽減するために新しい機能が含まれています。 For more information about other security features that help protect against credential theft, see [Credentials Protection and Management](https://technet.microsoft.com/library/dn408190.aspx). このトピックでは、次の新機能を構成する方法について説明します。

-   [保護されているユーザー](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_AddtoProtectedUsers)

-   [認証ポリシー](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicies)

-   [認証ポリシー サイロ](../../ad-ds/manage/How-to-Configure-Protected-Accounts.md#BKMK_CreateAuthNPolicySilos)

Windows 8.1 と Windows Server 2012 R2 資格情報の盗用に対する保護のために、次のトピックでは説明に組み込まれている追加の軽減策があります。

-   [リモート デスクトップの制限付き管理モード](http://blogs.technet.com/b/kfalde/archive/2013/08/14/restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)

-   [LSA の保護](https://technet.microsoft.com/library/dn408187)

## <a name="BKMK_AddtoProtectedUsers"></a>保護されているユーザー
Protected Users は、新しいグローバル セキュリティ グループを新規または既存のユーザーを追加することができます。 Windows 8.1 デバイスおよび Windows Server 2012 R2 ホストの資格情報の盗用に対する保護を強化するには、このグループのメンバーの特別な動作があります。 グループのメンバーは、Windows 8.1 デバイスまたは Windows Server 2012 R2 ホストをキャッシュしません Protected Users に対するサポートされていない資格情報。 Windows 8.1 より前のバージョンの Windows を実行しているデバイスにログオンしている場合、このグループのメンバーによって追加の保護はあるありません。

ユーザーがサインオン Windows 8.1 デバイスに Protected Users のメンバーをグループ化し、Windows Server 2012 R2 ホストできる*不要になった*を使用します。

-   既定の資格情報の委任 (CredSSP) - プレーン テキストの資格情報がキャッシュされていない場合でも、**既定の資格情報の委任を許可する**ポリシーが有効になっています。

-   Windows ダイジェスト - プレーン テキストの資格情報がキャッシュが有効になっているときでも

-   NTLM - NTOWF はキャッシュされません。

-   Kerberos 長期キー - Kerberos チケット保証チケット (TGT) はログオン時が取得され、自動的に再取得できません。

-   サイン オン オフライン - キャッシュされたログオン検証は作成されません。

ドメインの機能レベルが Windows Server 2012 R2 の場合は、グループのメンバーが不要になったできます。

-   NTLM 認証を使用して認証します。

-   Kerberos 事前認証でのデータ暗号化標準 (DES) または RC4 暗号スイートを使用します。

-   制約なし/制約付き委任を使用して委任します。

-   最初の 4 時間の有効期間を超えるユーザー チケット (Tgt) の更新します。

To add users to the group, you can use [UI tools](https://technet.microsoft.com/library/cc753515.aspx) such as Active Directory Administrative Center (ADAC) or Active Directory Users and Computers, or a command-line tool such as [Dsmod group](https://technet.microsoft.com/library/cc732423.aspx), or the Windows PowerShell[Add-ADGroupMember](https://technet.microsoft.com/library/ee617210.aspx) cmdlet. サービスおよびコンピューター アカウント*いけない*Protected Users グループのメンバーであります。 パスワードまたは証明書は、ホスト上で利用可能な常にあるために、それらのアカウントのメンバーシップにローカル保護が用意されていません。

> [!WARNING]
> 認証の制限には、回避策は、Enterprise Admins グループまたは Domain Admins グループなど、高い特権を持つグループのメンバーは、Protected Users グループの他のメンバーと同じ制限されることを意味はあるありません。 このようなグループのすべてのメンバーは、Protected Users グループに追加する場合、すべてのそれらのアカウントがロックアウトされる可能性があります。潜在的な影響を十分にテストしているまでに、Protected Users グループにすべての高い権限を持つアカウントを追加する必要があることはありません。

Protected Users グループのメンバーは、高度暗号化標準 (AES) で Kerberos を使用して認証できる必要があります。 このメソッドでは、Active Directory のアカウントに対する AES キーが必要です。 組み込みの管理者は、パスワードが Windows Server 2008 を実行しているドメイン コント ローラーで変更されたか後しない限り、AES キーがありません。 さらに、すべてのアカウントでは、Windows Server の以前のバージョンを実行しているドメイン コントローラーで変更されたパスワードを持つ、ロックアウトされます。そのため、これらのベスト プラクティスに従ってください。

-   テストしていないドメインにしない限り、 **2008 またはそれ以降、すべてのドメイン コント ローラーが Windows Server を実行**します。

-   **パスワードの変更**作成されたすべてのドメイン アカウントの*する前に*ドメインを作成します。 それ以外の場合、これらのアカウントを認証できません。

-   **パスワードの変更**グループ アカウントを Protected Users に追加する前に各ユーザーのまたはパスワードが Windows Server 2008 を実行するドメイン コント ローラーで最近変更されたまたはそれ以降のことを確認します。

### <a name="BKMK_Prereq"></a>保護されたアカウントを使用するための要件
保護されたアカウントには、次の展開要件があります。

-   Protected Users に対するクライアント側の制限を提供するには、ホストは Windows 8.1 または Windows Server 2012 R2 を実行する必要があります。 ユーザーのみが、Protected Users グループのメンバーであるアカウントでサインインします。 In this case, the Protected Users group can be created by [transferring the primary domain controller (PDC) emulator role](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) to a domain controller that runs  Windows Server 2012 R2 . そのグループのオブジェクトは、その他のドメイン コント ローラーにレプリケートされた後は、Windows Server の以前のバージョンを実行しているドメイン コント ローラーで PDC エミュレーターの役割をホストできます。

-   NTLM 認証の使用を制限するのには、Protected Users に対するドメイン コント ローラー側の制限とその他の制限を提供するには、Windows Server 2012 R2 がドメインの機能レベルにあります。 機能レベルの詳細については、次を参照してください。[について Active Directory ドメイン サービス (AD DS) の機能レベル](../active-directory-functional-levels.md)します。

### <a name="BKMK_TrubleshootingEvents"></a>Protected Users に関連するイベントをトラブルシューティングします。
このセクションでは、Protected Users と保護されているユーザーが、チケット保証チケット (TGT) 有効期限または委任に関する問題のトラブルシューティングを行うへの変更に影響を与えるに関連するイベントのトラブルシューティングに役立つ新しいログについて説明します。

#### <a name="new-logs-for-protected-users"></a>Protected Users 向けの新しいログ

Protected Users に関連するイベントのトラブルシューティングに役立つ 2 つの新しい運用管理ログがある: 保護されたユーザー - クライアントのログと Protected User Failures - ドメイン コント ローラーのログ。 これらの新しいログは、イベント ビューアー内にあるし、既定で無効になっています。 ログを有効にする] をクリックして**アプリケーションとサービス ログ**、] をクリックして**Microsoft**、] をクリックして**Windows**、] をクリックして**認証**、ログの名前をクリックして] をクリックして**アクション**(または、ログを右クリックして)] をクリック**ログの有効化**します。

For more information about events in these logs, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx).

#### <a name="troubleshoot-tgt-expiration"></a>TGT の有効期限をトラブルシューティングします。
通常、ドメイン コント ローラーは、TGT の有効期間と次のグループ ポリシー管理エディター] ウィンドウに表示されるドメイン ポリシーに基づいて更新を設定します。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

**Protected Users**、次の設定では、ハード コードします。

-   ユーザー チケットの最長有効期間: 240 分

-   ユーザー チケットを更新できる最長有効期間: 240 分

#### <a name="troubleshoot-delegation-issues"></a>委任に関する問題をトラブルシューティングします。
以前は、Kerberos の委任を使用しているテクノロジが失敗している場合、クライアントのアカウントがオンになっているかどうかを**アカウントは重要なので委任できない**設定されました。 ただし、アカウントのメンバーである場合**Protected Users**、この設定を [Active Directory 管理センター (ADAC) を構成していない可能性があります。 委任に関する問題をトラブルシューティングする際に、設定とグループのメンバーシップをその結果、確認します。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

### <a name="BKMK_AuditAuthNattempts"></a>認証試行を監査します。
メンバーの認証の試行を明示的に監査、 **Protected Users**グループ、セキュリティ ログの監査イベントを収集する、または新しい運用管理ログのデータを収集する続行することができます。 For more information about these events, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx)

### <a name="BKMK_ProvidePUdcProtections"></a>サービスとコンピューターに対して DC 側の保護を提供します。
サービスおよびコンピューター用のアカウントのメンバーであることはできません**Protected Users**します。 このセクションでは、これらのアカウントに対してどのドメイン コント ローラー ベースの保護を提供できるについて説明します。

-   Reject NTLM authentication: Only configurable via [NTLM block policies](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

-   Kerberos 事前認証でのデータ暗号化標準 (DES) の拒否: Windows Server 2012 R2 のドメイン コント ローラーは DES を受け入れません Kerberos と共にリリースされた Windows のすべてのバージョンには、RC4 もサポートされている理由だけ des を構成していないコンピュータのアカウントです。

-   Kerberos 事前認証での RC4 の拒否: 構成できません。

    > [!NOTE]
    > ことはできますが[サポートされている暗号化の種類の構成を変更](http://blogs.msdn.com/b/openspecification/archive/2011/05/31/windows-configurations-for-kerberos-supported-encryption-type.aspx)、対象の環境でテストなしのコンピューター アカウントの設定を変更することが推奨されません。

-   ユーザー チケット (Tgt) を最初の 4 時間の有効期間に制限: 認証ポリシーを使用します。

-   制約なし/制約付き委任による委任を拒否: アカウントを制限するには、Active Directory 管理センター (ADAC) を開き、[、**アカウントは重要なので委任できない**チェック ボックスをオンします。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TshootDelegation.gif)

## <a name="BKMK_CreateAuthNPolicies"></a>認証ポリシー
認証ポリシーは、認証ポリシー オブジェクトを含む AD DS の新しいコンテナーです。 認証ポリシーは、アカウントの TGT 有効期間を制限することや、その他の信頼性情報に関連する条件を追加するなど、資格情報の盗難のリスクを軽減するための設定を指定できます。

Windows Server 2012 で、ダイナミック アクセス制御には、組織全体でファイル サーバーを構成する簡単な方法を提供する集約型アクセス ポリシーと呼ばれる Active Directory フォレスト スコープ オブジェクト クラスが導入されました。 Windows Server 2012 r2、Windows Server 2012 R2 のドメイン内のアカウント クラスに認証構成を適用する認証ポリシー (objectClass Msds-authnpolicies) と呼ばれる新しいオブジェクト クラスを使用できます。 Active Directory アカウント クラスがあります。

-   ユーザー

-   コンピューター

-   管理されたサービス アカウントとグループの管理されたサービス アカウント (GMSA)

### <a name="quick-kerberos-refresher"></a>クイック Kerberos リフレッシャー
Kerberos 認証プロトコルは、次の 3 つの種類の交換、サブプロトコルとも呼ばれるで構成されます。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbRefresher.gif)

-   認証サービス (AS) 交換 (krb_as _ *)

-   チケット保証サービス (TGS) 交換 (krb_tgs _ *)

-   クライアント/サーバー (AP) 交換 (krb_ap _ *)

AS 交換は、チケット保証チケット (TGT) を要求する事前認証子を作成する、クライアントが、アカウントのパスワードや秘密キーを使用する場所です。 これはユーザーのサインオンまたはサービス チケットが必要な最初の時間。

TGS 交換では、サービス チケットを要求する認証子を作成するアカウントの TGT が使用されています。 これは、認証済みの接続が必要な場合に発生します。

AP 交換は通常、アプリケーション プロトコル内部のデータとして発生し、認証ポリシーの影響を受けません。

詳細についてを参照してください。[方法 Kerberos バージョン 5 認証プロトコルの動作](https://technet.microsoft.com/library/cc772815(v=WS.10).aspx)します。

### <a name="overview"></a>概要
認証ポリシーは、アカウントに構成可能な制限を適用する方法を提供することで、およびサービスおよびコンピューター用のアカウントの制限を提供することで、Protected Users を補完します。 AS 交換または TGS のいずれかの中に認証ポリシーが適用される exchange します。

構成することによって、最初の認証または AS 交換を制限できます。

-   TGT 有効期間

-   ユーザー サインオン、元の AS 交換が送られているデバイスが満たす必要がありますを制限するアクセス制御条件

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictAS.gif)

構成することによって、チケット保証サービス (TGS) 交換を通じたサービス チケット要求を制限できます。

-   クライアント (ユーザー、サービス、コンピューター) が満たす必要があるアクセス制御条件または TGS 交換が近日公開元となるデバイス

### <a name="BKMK_ReqForAuthnPolicies"></a>認証ポリシーを使用するための要件

|ポリシー|要件|
|----------|----------------|
|カスタムの TGT の有効期間を指定します。| Windows Server 2012 R2 のドメイン機能レベルのアカウント ドメイン|
|ユーザーのサインオンを制限します。|-ダイナミック アクセス制御のサポート Windows Server 2012 R2 のドメイン機能レベルのアカウント ドメイン<br />Windows 8、Windows 8.1、Windows Server 2012 またはダイナミック アクセス制御を持つデバイスの Windows Server 2012 R2 のサポートします。|
|ユーザー アカウントおよびセキュリティ グループに基づくサービス チケット発行を制限します。| Windows Server 2012 R2 のドメイン機能レベルのリソース ドメイン|
|ユーザーの信頼性情報またはデバイス アカウント、セキュリティ グループ、または信頼性情報に基づくサービス チケット発行を制限します。| ダイナミック アクセス制御のサポートを Windows Server 2012 R2 のドメイン機能レベルのリソース ドメイン|

### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>特定のデバイスやホストにユーザー アカウントを制限します。
管理者特権を持つ高価値アカウントのメンバーである必要があります、 **Protected Users**グループ。 既定では、アカウントがないのメンバー、 **Protected Users**グループ。 グループにアカウントを追加する前に、ドメイン コント ローラーのサポートを構成し、ブロックの問題がないことを確認する監査ポリシーを作成します。

#### <a name="configure-domain-controller-support"></a>ドメイン コント ローラーのサポートを構成します。

ユーザーのアカウント ドメインは、Windows Server 2012 R2 のドメイン機能レベル (DFL) にある必要があります。 Ensure all the domain controllers are  Windows Server 2012 R2 , and then use Active Directory Domains and Trusts to [raise the DFL](https://technet.microsoft.com/library/cc753104.aspx) to  Windows Server 2012 R2 .

**ダイナミック アクセス制御のサポートを構成するには**

1.  既定のドメイン コント ローラー ポリシー] をクリックして**有効**を有効にする**信頼性情報、複合認証、および Kerberos 防御のキー配布センター (KDC) クライアント サポート**[コンピューターの構成 |管理用テンプレート |システム |KDC します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)

2.  **オプション**、ドロップダウン リスト ボックスで選択**常に信頼性情報を提供**します。

    > [!NOTE]
    > **サポートされている**も構成することができますが、ドメインの Dc を常にも、Windows Server 2012 R2 DFL であるためクレームを使用するユーザーの信頼性情報ベースのアクセス確認を行う要求に非対応のデバイスを使用する場合と信頼性情報に対応するサービスに接続するホストを提供します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)

    > [!WARNING]
    > 構成**防御されていない認証要求を失敗**Windows 7 およびそれ以前のオペレーティング システムなどの Kerberos 防御をサポートしていないすべてのオペレーティング システムまたは Windows 8 は、サポートするように明示的に構成されていない以降のオペレーティング システムからの認証エラーが発生します。

#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>認証ポリシーのユーザー アカウント監査を ADAC で作成します。

1.  Active Directory 管理センター (ADAC) を開きます。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_OpenADAC.gif)

    > [!NOTE]
    > 選択した**認証**ノードがドメインに Windows Server 2012 R2 DFL で表示します。 ノードが表示されない場合、再試行して Windows Server 2012 R2 DFL にあるドメインからドメイン管理者アカウントを使用しています。

2.  をクリックして**認証ポリシー**、] をクリックし、**新規**新しいポリシーを作成します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)

    認証ポリシーは、表示名が必要され、既定で適用されます。

3.  監査のみのポリシーを作成する] をクリックして**監査ポリシーの制限のみ**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)

    認証ポリシーは、Active Directory アカウントの種類に基づいて適用されます。 1 つのポリシーは、各種類の設定を構成することによって、次の 3 つのアカウントの種類をすべてに適用できます。 アカウントの種類があります。

    -   ユーザー

    -   コンピューター

    -   管理されたサービス アカウントの管理されたサービス アカウントとグループ

    キー配布センター (KDC) で使用できる新しいプリンシパルでスキーマを拡張する場合、新しいアカウントの種類は、最も近い派生アカウントの種類から分類されます。

4.  ユーザー アカウントの TGT 有効期間を構成するには、選択、**のユーザー アカウントのチケット保証チケットの有効期間を指定**チェック ボックスをオンにし、時間を分単位で入力します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTLifetime.gif)

    たとえば、10 時間最大 TGT 有効期間を実行する場合に、入力**600**示すようにします。 TGT の有効期間が構成されていない場合、アカウントのメンバーである場合、 **Protected Users** TGT の有効期間をグループ化し、更新は 4 時間です。 それ以外の場合、TGT の有効期間および更新は、ドメインの既定の設定の次のグループ ポリシー管理エディター] ウィンドウに表示されるドメイン ポリシーに基づいています。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_TGTExpiration.png)

5.  デバイスを選択するユーザー アカウントを制限する] をクリックして**編集**デバイスに必要な条件を定義します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)

6.  **アクセス制御条件の編集**] ウィンドウで、をクリックして**条件を追加**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCondition.png)

##### <a name="add-computer-account-or-group-conditions"></a>コンピューター アカウントまたはグループの条件を追加します。

1.  ドロップダウン リストでコンピューター アカウントまたはグループを構成するには、ドロップダウン リスト ボックスを選択**の各メンバー**し、変更**いずれかのメンバー**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompMember.png)

    > [!NOTE]
    > このアクセス制御では、デバイスまたはユーザーがサインオン元となるホストの条件を定義します。 アクセス制御の用語でデバイスまたはホストのコンピューター アカウントは、ユーザーは、その理由は、**ユーザー**唯一のオプションです。

2.  をクリックして**項目を追加**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddItems.png)

3.  オブジェクトの種類を変更する] をクリックして**オブジェクトの種類**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjects.gif)

4.  Active directory コンピューター オブジェクトを選択する] をクリックして**コンピューター**、] をクリックし、 **OK**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)

5.  ユーザーを制限し、[コンピュータの名前を入力**名前の確認**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)

6.  [Ok] をクリックし、コンピューター アカウントの他の条件を作成します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompAddConditions.png)

7.  完了したら、クリックして**OK**され、コンピューター アカウントの定義済みの条件が表示されます。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AddCompDone.png)

##### <a name="add-computer-claim-conditions"></a>コンピューターの要求の条件を追加します。

1.  コンピューターの要求を構成するには、ドロップダウン グループ要求を選択します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaim.gif)

    要求では、フォレスト内に既にプロビジョニングされている場合のみです。

2.  ユーザー アカウントのサインオンを制限する必要があります、OU の名前を入力します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimOUName.gif)

3.  完了したら、[ok] をクリックし、ボックスは定義された条件を表示します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CompClaimComplete.gif)

##### <a name="troubleshoot-missing-computer-claims"></a>不足しているコンピューターの要求をトラブルシューティングします。
要求は準備されているが使用できない場合、それ可能性がありますのみに構成する**コンピューター**クラス。

たとえばを組織単位 (OU) に基づく認証を制限したいがに対してのみが、既に構成されていると、コンピューターの**コンピューター**クラス。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictComputers.gif)

要求ができるように、デバイスへのユーザーのサインオンを制限するには、選択、**ユーザー**チェック ボックスをオンします。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)

#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>ADAC で認証ポリシーを持つユーザー アカウントをプロビジョニングします。

1.  **ユーザー**アカウント] をクリックして**ポリシー**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicy.gif)

2.  選択、**をこのアカウントに認証ポリシーを割り当てる**チェック ボックスをオンします。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)

3.  次に、ユーザーに適用する認証ポリシーを選択します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_UserPolicySelect.png)

#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>デバイスおよびホストでダイナミック アクセス制御のサポートを構成します。
ダイナミック アクセス制御 (DAC) を構成しなくても、TGT の有効期間を構成できます。 DAC は、AllowedToAuthenticateFrom および AllowedToAuthenticateTo を確認するためだけ必要です。

グループ ポリシーまたはローカル グループ ポリシー エディターを使用して、有効にする**信頼性情報、複合認証、および Kerberos 防御の Kerberos クライアント サポート**[コンピューターの構成 |管理用テンプレート |システム |Kerberos:

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)

### <a name="BKMK_TroubleshootAuthnPolicies"></a>認証ポリシーをトラブルシューティングします。

#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>認証ポリシーが直接割り当てられているアカウントを決定します。
認証ポリシー [アカウント] セクションでは、ポリシーが直接適用されたアカウントを示します。

![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_AccountsAssigned.gif)

#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Authentication Policy Failures - Domain Controller 管理ログの使用します。
新しい**Authentication Policy Failures - ドメイン コント ローラー**下にある管理ログ**アプリケーションとサービス ログ** > **Microsoft** > **Windows** > **認証**、認証ポリシーが原因のエラーを検出するが簡単に作成されました。 ログは既定で無効にします。 これを有効にする [ログ名を右クリックし、] をクリックして**ログの有効化**します。 新しいイベントは、コンテンツ、既存の Kerberos TGT やサービス チケットの監査イベントを非常に似ています。 For more information about these events, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx).

### <a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Windows PowerShell を使用して認証ポリシーを管理します。
このコマンドは、という名前の認証ポリシーを作成します。 **TestAuthenticationPolicy**します。 **UserAllowedToAuthenticateFrom**パラメーターは、元のユーザーが someFile.txt という名前のファイルの SDDL 文字列によって認証できるデバイスを指定します。

```
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl
```

このコマンドは、フィルターに一致するすべての認証ポリシーを取得する、**フィルター**パラメーターを指定します。

```
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com

```

このコマンドは、説明を変更し、 **UserTGTLifetimeMins**指定された認証ポリシーのプロパティ。

```
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45
```

このコマンドは、認証ポリシーを削除する、 **Identity**パラメーターを指定します。

```
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1
```

このコマンドを使用して、 **Get-adauthenticationpolicy**コマンドレットと、**フィルター**パラメーターが適用されていないすべての認証ポリシーを取得します。 結果セットは、パイプを使用して、**削除 ADAuthenticationPolicy**コマンドレット。

```
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy
```

## <a name="BKMK_CreateAuthNPolicySilos"></a>認証ポリシー サイロ
認証ポリシー サイロは、[AD DS のユーザー、コンピューター、およびサービス アカウントに新しいコンテナー (objectClass Msds-authnpolicysilos) です。 これらは、高価値アカウントを保護するためです。 すべての組織では、フォレスト内にアクセスする攻撃者によってこれらのアカウントが使用されるため、Enterprise Admins、Domain Admins および Schema Admins グループのメンバーを保護する必要がありますが、他のアカウントに保護が必要もあります。

一部の組織は、それらに固有のアカウントを作成し、ローカルおよびリモートの対話型ログオンと管理者特権を制限するグループ ポリシー設定を適用して、ワークロードを分離します。 認証ポリシー サイロは、ユーザー、コンピューター、および管理されたサービス アカウント間の関係を定義する方法を作成することでこの作業を補完します。 アカウントは、1 つのサイロのみ所属できます。 アカウントの種類ごとの認証ポリシーを制御するために構成できます。

1.  更新不可の TGT 有効期間

2.  アクセス制御条件の TGT を返すため (注: Kerberos 防御が必要になるために、システムに適用できません)

3.  サービス チケットを返すためのアクセス制御条件

さらに、認証ポリシー サイロのアカウントはサイロ要求がアクセスを制御するファイル サーバーなどの信頼性情報に関連するリソースで使用できるがあります。

基づくサービス チケットの発行を制御するには、新しいセキュリティ記述子を構成できます。

-   ユーザー、ユーザーのセキュリティ グループ、またはユーザーの信頼性情報

-   デバイス、デバイスのセキュリティ グループ、およびデバイスの信頼性情報

リソースの Dc には、この情報を取得するには、ダイナミック アクセス制御が必要です。

-   ユーザーの信頼性情報:

    -   Windows 8 およびそれ以降のクライアントがダイナミック アクセス制御をサポートします。

    -   ダイナミック アクセス制御と要求をサポートするアカウント ドメイン

-   デバイスおよびデバイス セキュリティ グループ:

    -   Windows 8 およびそれ以降のクライアントがダイナミック アクセス制御をサポートします。

    -   複合認証用に構成されたリソース

-   デバイスの信頼性情報:

    -   Windows 8 およびそれ以降のクライアントがダイナミック アクセス制御をサポートします。

    -   ダイナミック アクセス制御と要求をサポートするデバイス ドメイン

    -   複合認証用に構成されたリソース

認証ポリシーは、すべての代わりに、個々 のアカウントに、認証ポリシー サイロのメンバーに適用できますか、サイロ内のアカウントの種類に個別の認証ポリシーを適用できます。 たとえば、1 つの認証ポリシーは、高い特権を持つユーザー アカウントに適用でき、サービス アカウントに、別のポリシーを適用できます。 認証ポリシー サイロを作成する前に、少なくとも 1 つの認証ポリシーを作成する必要があります。

> [!NOTE]
> 認証ポリシーは、認証ポリシー サイロのメンバーに適用することができますか、特定のアカウント スコープを制限するサイロとは無関係に適用できます。 たとえば、1 つのアカウントまたは少数のアカウントを保護するのにポリシーことができますを設定するこれらのアカウントで、アカウントをサイロに追加することがなくします。

Active Directory 管理センターまたは Windows PowerShell を使用して、認証ポリシー サイロを作成することができます。 既定では、認証ポリシー サイロのみサイロ ポリシーの監査を指定することと同等である、 **WhatIf** Windows PowerShell コマンドレットのパラメーターです。 この場合は、ポリシー サイロの制限は適用されませんが、監査は制限が適用されている場合にエラーが発生するかどうかを示すために生成されます。

#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Active Directory 管理センターを使用して、認証ポリシー サイロを作成するには

1.  開いている**Active Directory 管理センター**、] をクリックして**認証**、右クリックして**認証ポリシー サイロ**、] をクリックして**新規**、] をクリックし、**認証ポリシー サイロ**します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)

2.  **表示名**、サイロの名前を入力します。 **許可されたアカウント**、] をクリックして**追加**、アカウントの名前を入力し、[クリックして**OK**します。 ユーザー、コンピューター、またはサービス アカウントを指定することができます。 すべてのプリンシパルまたはプリンシパルの各種類と、ポリシーまたはポリシーの名前に対して個別のポリシーの 1 つのポリシーを使用するかどうかを指定します。

    ![保護されたアカウント](media/How-to-Configure-Protected-Accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)

### <a name="BKMK_ManageAuthnSilosUsingPSH"></a>Windows PowerShell を使用して認証ポリシー サイロを管理します。
このコマンドは、認証ポリシー サイロ オブジェクトを作成し、それを適用します。

```
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce
```

このコマンドを取得、すべての認証ポリシー サイロによって指定されるフィルターに一致する、**フィルター**パラメーター。 渡されますが、出力、 **Format-table**ポリシーとの値の名前を表示するコマンドレット**実施**ポリシーごとにします。

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize

Name  Enforce
----  -------
silo     True
silos   False

```

このコマンドを使用して、 **Get ADAuthenticationPolicySilo**コマンドレットと、**フィルター**をすべて適用されていない認証ポリシー サイロとパイプするフィルターの結果を取得するパラメーター、**削除 ADAuthenticationPolicySilo**コマンドレット。

```
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo
```

このコマンドは、という名前の認証ポリシー サイロへのアクセスを*サイロ*という名前のユーザー アカウントに*User01*します。

```
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01
```

このコマンドは、という名前の認証ポリシー サイロへのアクセスを取り消します*サイロ*という名前のユーザー アカウント*User01*します。 あるため、 **Confirm**パラメーターに設定されて**$False**、確認メッセージは表示されません。

```
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False
```

この例を使用して、 **Get-adcomputer**フィルターに一致するすべてのコンピューター アカウントを取得するコマンドレットを**フィルター**パラメーターを指定します。 このコマンドの出力に渡される**Set-adaccountauthenticatinpolicysilo**という名前の認証ポリシー サイロに*サイロ*という名前の認証ポリシーと*AuthenticationPolicy02*にします。

```
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02
```



