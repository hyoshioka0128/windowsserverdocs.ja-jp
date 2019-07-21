---
title: 特権アクセスの保護
description: 特権アクセスの保護を段階的なアプローチ
ms.prod: windows-server-threshold
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 0d54a94d51a4d1e0a1d28f78ec39bf16bc3d9100
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822013"
---
# <a name="securing-privileged-access"></a>特権アクセスの保護

>適用先:Windows Server

特権アクセスをセキュリティで保護することは、現代の組織においてビジネス資産のセキュリティ保証を確立するための重要な第一歩です。 IT 組織内のほとんどまたはすべてのビジネス資産のセキュリティは、管理、管理、および開発するために使用する特権アカウントの整合性に依存します。 サイバー攻撃者は、これらのアカウントおよびデータとなどの資格情報の盗難攻撃を使用してシステムにアクセスする特権アクセスの他の要素に多くの場合、対象[Pass the Hash、Pass the Ticket](https://www.microsoft.com/pth)します。

敵対者に対して特権アクセスを保護するには、これらのシステム リスクからを分離する完全かつ熟慮されたアプローチを採用する必要があります。

## <a name="what-are-privileged-accounts"></a>特権アカウントとは

それらをセキュリティで保護する方法について説明する前に、特権アカウントを定義することができます。

Active Directory Domain Services の管理者はこれらのアカウントのセキュリティ侵害の重要なビジネス リスクを行うのでは、IT 組織では、ほとんどまたはすべての資産を直接的または間接的なアクセスをいるような特権を持つアカウント。

## <a name="why-securing-privileged-access-is-important"></a>なぜ特権アクセスをセキュリティで保護することが重要ですか。

すべての組織に迅速にアクセスする Active Directory (AD) には、データが対象となるようにシステムへのアクセス権限でサイバー攻撃フォーカスします。 従来のセキュリティの手法が、主要なセキュリティ境界としてネットワークとファイアウォールに重点を置いて、ネットワーク セキュリティの有効性が 2 つの傾向によって大幅に低下しました。

* 組織がデータをホストしていると、モバイル エンタープライズ Pc、タブレット、携帯電話などのデバイスでの従来のネットワークの境界外のリソースがクラウド サービス、および独自デバイス (BYOD)
* 敵対者は、フィッシングやその他の Web および電子メール攻撃を通じて、ネットワーク境界内のワークステーションへのアクセスを入手する、一貫性のある継続的な能力を実証しています。

これらの要因の認証と承認から最新のセキュリティ境界を構築するには、id コントロールだけでなく、従来のネットワーク境界の戦略が必要になります。 セキュリティの境界をここでは、一貫性のある資産とそれらの脅威についての間でのコントロールのセットとして定義されます。 特権アカウントが効果的に管理この新しいセキュリティ境界の特権アクセスを保護することが重要であるようにします。

![組織の ID 層を示す図](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

管理アカウントの制御を取得した攻撃者は、次のように、対象となる組織への影響を向上させるそれらの特権を使用できます。

![管理アカウントを制御できるようになった敵対者は、それらの権限を使用し、対象となる組織を犠牲にして、利益を追求できることを示す図](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

次の図は、2 つのパスを示しています。

* 電子メールと web 閲覧や日々 の作業などのリソースへのアクセスを特権のない標準ユーザー アカウントが使用されている"blue"パスが完了しました。

   > [!NOTE]
   > 後で説明されている青色のパス項目は、管理者アカウントを越える保護機能が広範な環境を示します。

* "Red"のパスをフィッシングやその他の web および電子メール攻撃のリスクを軽減するセキュリティを強化したデバイスの特権アクセスが発生します。

![管理用 web の閲覧や電子メールへのアクセスなど、危険度の高い標準ユーザー タスクから特権アクセスのタスクを分離するロードマップを確立する個別の"path"を示す図](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>特権アクセスのロードマップをセキュリティで保護します。

ロードマップは、既にデプロイした Microsoft テクノロジの使用、セキュリティを強化し、サード パーティ製のセキュリティ ツールが既に展開したを統合するクラウド テクノロジの活用を最大化する設計されています。

Microsoft の推奨事項のロードマップは、3 つのフェーズに分かれています。

* [フェーズ 1:最初の 30 日]()
   * 意味のある正の値への影響をすばやく有効になります。
* [フェーズ 2:90 日間]()
   * 増分大幅に向上します。
* [フェーズ 3:進行中]()
   * セキュリティの向上と sustainment します。

このロードマップは、これらの攻撃と解決方法の実装に関する経験に基づいて、最も効果的で最も迅速な実装をスケジュールするように、優先順位が設定されています。 

Microsoft では、断固とした敵対者に対して特権アクセスをセキュリティで保護するために、このロードマップに従うことをお勧めします。 既存の機能や、組織固有の要件に対応するように、このロードマップを調整してもかまいません。

> [!NOTE]
> 特権アクセスをセキュリティで保護するには、技術コンポーネント (ホストの防御、アカウントの保護、ID 管理など) を含むさまざまな要素だけでなく、プロセスへの変更や、管理業務と知識が必要になります。 ロードマップのタイムラインは概算であり、お客様の実装の経験に基づきます。 お客様の環境と、変更管理プロセスの複雑さによって、組織内で所要期間が異なることがあります。

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>フェーズ 1:最小限の運用の複雑さのクイック wins

ロードマップの第 1 段階は、資格情報の盗難や誤用の最も頻繁に使用される攻撃手法を迅速に軽減する重視されています。 フェーズ 1 では、約 30 日以内に実装する設計されており、この図に示すようには。

![フェーズ 1 図に示します。1. 独立した管理者とユーザー アカウント、2 です。 ジャスト イン タイムのローカル管理者パスワード、3。 管理ワークステーション ステージ 1、4 です。 Id 攻撃の検出](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. 個別のアカウント

インターネット上のリスクを分離するために (フィッシング攻撃、web 閲覧) 特権からアカウントへのアクセス、特権アクセスを持つすべてのスタッフに専用のアカウントを作成します。 管理者が自分の電子メールをチェックし、高い特権を持つアカウントを使用して日常の生産性のタスクの実行に対して、web は参照されませんする必要があります。 これの詳細については、セクションではあります[個別の管理アカウント](securing-privileged-access-reference-material.md#separate-administrative-accounts)のリファレンス ドキュメント。

この記事のガイダンスに従って[Azure AD で緊急アクセス用アカウントを管理](/azure/active-directory/users-groups-roles/directory-emergency-access)アカウントを作成するには少なくとも 2 つの緊急アクセス、両方で、オンプレミスで、完全に割り当てられている管理者の権限を持つ AD と Azure AD 環境. 従来の管理者アカウントで必要なタスクを実行できない場合に、これらのアカウントが使用するためだけは、災害の場合。

### <a name="2-just-in-time-local-admin-passwords"></a>2. ジャスト イン タイムのローカル管理者パスワード

組織はその他のコンピューターを攻撃する攻撃者に悪用してほか、ローカルの SAM データベースからローカル管理者アカウントのパスワード ハッシュを盗むことのリスクを軽減するために、すべてのコンピューターが一意のローカル管理者のパスワードを確認してください。 サーバーに格納で Active Directory (AD)、ACL によって保護されているし、ローカル管理者パスワード Solution (LAPS) ツールは、各ワークステーション上で一意のランダムなパスワードを構成できます。 資格のある承認されたユーザーのみでは、読み取るしたり、これらのローカル管理者アカウント パスワードのリセットを依頼することができます。 ワークステーションやサーバー上で使用するため、LAPS を取得する[、Microsoft ダウンロード センター](http://Aka.ms/LAPS)します。

LAPS と Paw の環境を操作するために追加のガイダンスについては、セクションで見つかる[クリーン ソースの原則に基づいて運用基準](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle)します。

### <a name="3-administrative-workstations"></a>3.管理ワークステーション

Azure Active Directory とオンプレミスでの従来の Active Directory の管理者特権を持つユーザーの初期のセキュリティ措置として確実に構成されている Windows 10 デバイスを使用している、[安全性の高い Windows 向けの標準案10 のデバイス](/windows-hardware/design/device-experiences/oem-highly-secure)します。 

### <a name="4-identity-attack-detection"></a>4。Id 攻撃の検出

[Azure の高度な Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp)は高度な脅威、侵害された id、および悪意のある内部関係者のアクションが、オンプレミスでのアクティブな転送を識別、検出すると、しに役立つクラウド ベースのセキュリティ ソリューションの調査ディレクトリの環境です。

## <a name="phase-2-significant-incremental-improvements"></a>フェーズ 2:重要な漸進的改良

フェーズ 2 では、フェーズ 1 で実行された作業はし、約 90 日間に完了するのには設計されています。 このステージの手順を次の図で示します。

![フェーズ 2 図に示します。1. Windows Hello for Business/MFA、2 です。 PAW ロールアウトでは、3。 ジャスト イン タイムの特権 4 です。 Credential Guard では、5 です。 漏洩した資格情報、6。 水平方向の活動の脆弱性の検出](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Windows Hello for Business と MFA が必要

管理者は、Windows Hello for Business に関連付けられている使いやすさを活用できます。 管理者は、各自の Pc で強力な 2 要素認証を使用した複雑なパスワードを置き換えることができます。 攻撃者は、デバイスと生体認証情報または暗証番号 (pin) の両方が必要、従業員の知識がなくてもアクセスする非常に困難です。 Windows Hello for Business とロールアウトへのパスの詳細については、情報の記事では[Windows Hello for Business の概要](/windows/security/identity-protection/hello-for-business/hello-overview)

Azure MFA を使用して Azure AD での管理者アカウントの多要素認証 (MFA) を有効にします。 最小有効にする で、[ベースラインの保護の条件付きアクセス ポリシー](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins) Azure Multi-factor Authentication の詳細については、情報の記事では[クラウド ベース Azure Multi-factor Authentication のデプロイ](/azure/active-directory/authentication/howto-mfa-getstarted)

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. すべての特権ユーザー アクセス アカウントの所有者に PAW を展開します。

電子メール、web の閲覧、およびその他の非管理タスクで検出された脅威から特権アカウントを分離するという処理を続行するには、実装することを専用の Privileged Access Workstations (PAW) へのアクセス権限を持つすべてのスタッフの組織の情報システム。 PAW の展開の追加のガイダンスについては、情報の記事で見つかる[Privileged Access Workstation](privileged-access-workstations.md#paw-phased-implementation)します。

### <a name="3-just-in-time-privileges"></a>3.ジャスト イン タイムの特権

特権の露出時間を削減し、可視性の使用を増やすするには、ジャスト イン タイム (JIT) の以下のように適切なソリューションまたはその他のサード パーティ製ソリューションを使用して権限を指定します。

* Active Directory Domain Services (AD DS) の場合は、Microsoft Identity Manager (MIM) の[特権アクセス マネージャー (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 機能を使用してください。
* Azure Active Directory の場合は、[Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 機能を使用してください。

### <a name="4-enable-windows-defender-credential-guard"></a>4。Windows Defender Credential Guard を有効にする

Credential Guard を有効にすると、NTLM パスワード ハッシュ、Kerberos Ticket Granting Ticket およびドメインの資格情報としてのアプリケーションによって保存された資格情報を保護するのに役立ちます。 この機能は、Pass the Hash、Pass The Ticket 盗まれた資格情報を使用して、環境でのピボットの難しさを増やすことでなどの資格情報盗難攻撃を防ぐのに役立ちます。 Credential Guard のしくみとデプロイする方法については、記事ではあります[保護は、Windows Defender Credential Guard でのドメイン資格情報を派生](/windows/security/identity-protection/credential-guard/credential-guard)します。

### <a name="5-leaked-credentials-reporting"></a>5。漏洩した資格情報の報告

「毎日では、Microsoft 分析して新たな脅威を識別し、お客様を保護するために信号を超える 6.5 兆」-[番号によって Microsoft](https://news.microsoft.com/bythenumbers/cyber-attacks)

漏洩した資格情報を持つユーザーをレポートを修復できるようにする Microsoft Azure AD Identity Protection を有効にします。 [Azure AD Identity Protection](/azure/active-directory/identity-protection/index)組織のクラウドおよびハイブリッド環境を脅威から保護支援を活用することができます。

### <a name="6-azure-atp-lateral-movement-paths"></a>6。Azure ATP の横移動パス

特権を確認します。 アカウント所有者を使用している、PAW 管理のセキュリティを侵害された、特権のないアカウントは Pass the Hash、Pass The Ticket などの資格情報盗難攻撃を使用して特権のアカウントにアクセスできないようにするためだけにアクセスします。 [Azure ATP 横移動パス (LMPs)](/azure-advanced-threat-protection/use-case-lateral-movement-path)特権アカウントが侵害を開いてありますを識別するためにレポートを理解する容易な提供します。

## <a name="phase-3-security-improvement-and-sustainment"></a>フェーズ 3:セキュリティの向上と sustainment

ロードマップのフェーズ 3 は、セキュリティに対する姿勢を強化するために、フェーズ 1 および 2 で実行される手順に基づいています。 フェーズ 3 は、この図では視覚的に示します。

![フェーズ 3:1. RBAC、2 を確認します。 攻撃対象領域、3 を削減します。 SEIM、4 と、ログを統合します。 漏洩した資格情報の自動化](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

これらの機能は、前のフェーズの手順でビルドしより予防的な対策を防御を移動します。 このフェーズでは、特定のタイムラインを持たず、時間がかかる実装するために個別の組織に基づきます。

### <a name="1-review-role-based-access-control"></a>1. ロールベースのアクセス制御を確認します。

記事に記載されている 3 つの階層化モデルを使用して[Active Directory 管理階層モデル](securing-privileged-access-reference-material.md)を確認して、下位層の管理者には、上位階層のリソース (グループ メンバーシップ、上の Acl への管理アクセスはありません確認します。ユーザー アカウントなど.)。

### <a name="2-reduce-attack-surfaces"></a>2. 攻撃対象領域を減らす

ドメインを含む、identity ワークロードを強化する、ドメイン コント ローラー、ad FS、およびこれらのシステムを損なうこととして Azure AD Connect は、組織の他のシステムの侵害になる可能性があります。 記事[Active Directory の攻撃対象領域を減らすこと](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md)と[5 つの手順で、id インフラストラクチャをセキュリティで保護する](/azure/security/azure-ad-secure-steps)オンプレミスおよびハイブリッド セキュリティで保護するためのガイダンスを提供する identity 環境。

### <a name="3-integrate-logs-with-siem"></a>3.ログを SIEM に統合します。

ログ記録を一元的な SIEM ツールに統合すると、分析、検出、およびセキュリティ イベントに応答する組織できます。 記事[侵害の兆候の監視の Active Directory](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md)と[付録 l:監視するイベント](../ad-ds/plan/appendix-l--events-to-monitor.md)環境内で監視する必要があるイベントに関するガイダンスを提供します。

これは、他の部分を作成する、集計、ためにの計画し、(ボックス アラート外を含む 30 日間計画に Azure ATP) とは異なり、熟練したアナリストのセキュリティ情報およびイベント管理 (SIEM) でアラートの調整が必要です

### <a name="4-leaked-credentials---force-password-reset"></a>4。漏洩した資格情報のパスワードのリセットを強制

パスワードがセキュリティ侵害の疑いがあるときに自動的にパスワードのリセットを強制する Azure AD Identity Protection を有効にすると、セキュリティ体制を強化するために続行します。 [チュートリアル:リスク イベントを使用して多要素認証とパスワード変更をトリガーする](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa)に記載されているガイダンスでは、条件付きアクセスポリシーを使用してこれを有効にする方法について説明しています。

## <a name="am-i-done"></a>ロードマップの完了

答えはありません。

悪意のあるユーザーが停止しない、どちらもすることができます。 このロードマップは、組織の保護を支援できます現在認識されている脅威攻撃者が常に進化し、シフトします。 コストを発生させると、環境を対象とする敵対者の成功率を減らすことに重点を置いた継続的なプロセスとしてセキュリティを表示することをお勧めします。

特権アクセスをセキュリティで保護する組織のセキュリティ プログラムの一部だけではありませんが、セキュリティ戦略の重要なコンポーネントです。
