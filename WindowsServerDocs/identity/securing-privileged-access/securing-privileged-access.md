---
title: 特権アクセスの保護
description: 特権アクセスをセキュリティで保護するための段階的アプローチ
ms.prod: windows-server
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: 806a2aced95421bd469ba885d4a81c219ae1b651
ms.sourcegitcommit: 457e88e5aa6be13a2bffdb8e434a8efc3698678f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548836"
---
# <a name="securing-privileged-access"></a>特権アクセスの保護

>適用先:Windows Server

特権アクセスをセキュリティで保護することは、現代の組織においてビジネス資産のセキュリティ保証を確立するための重要な第一歩です。 IT 組織内のほとんどまたはすべてのビジネス資産のセキュリティは、管理や開発に使用される特権アカウントの整合性に依存します。 サイバー攻撃者は、多くの場合これらのアカウントや特権アクセスの他の要素を攻撃の標的にし、[Pass-the-Hash および Pass-the-Ticket](https://www.microsoft.com/pth) のような資格情報を盗難する攻撃を使用して、データやシステムへのアクセスを取得します。

断固とした敵対者に対して特権アクセス権を保護するには、これらのシステムからリスクを切り離すための完全で十分に考慮されたアプローチを採用する必要があります。

## <a name="what-are-privileged-accounts"></a>特権アカウントとは

セキュリティで保護する方法について説明する前に、特権アカウントを定義しましょう。

Active Directory Domain Services の管理者のような特権アカウントは、IT 組織内のほとんどまたはすべての資産に直接または間接的にアクセスできるため、これらのアカウントのセキュリティ侵害は重大なビジネス リスクになります。

## <a name="why-securing-privileged-access-is-important"></a>特権アクセスのセキュリティ保護が重要な理由

サイバー攻撃は、組織の標的とするすべてのデータに迅速にアクセスするために、Active Directory (AD) のようなシステムの特権アクセスに焦点を合わせます。 従来のセキュリティの手法は、主要なセキュリティ境界としてネットワークとファイアウォールを重視してきましたが、次の 2 つの傾向によって、ネットワーク セキュリティの有効性は大幅に低下しました。

* 組織はデータやリソースを、従来のネットワークの境界外にあるモバイル エンタープライズ PC 、携帯電話やタブレットなどのデバイス、クラウド サービスおよび Bring Your Own Device (BYOD) でホストしています
* 敵対者は、フィッシングやその他の Web および電子メール攻撃を通じて、ネットワーク境界内のワークステーションへのアクセスを入手する、一貫性のある継続的な能力を実証しています。

これらの要因により、従来のネットワーク境界戦略に加えて、認証および承認 ID 制御から最新のセキュリティ境界を構築する必要があります。 ここでのセキュリティ境界は、資産とそれらに対する脅威との間の一貫した制御のセットとして定義されています。 特権アカウントは実際上この新しいセキュリティ境界の管理下におかれるため、特権アクセスを保護することが重要になります。

![組織の ID 層を示す図](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

管理アカウントを制御できるようになった攻撃者は、次の図のように、それらの権限を使用し、対象となる組織への影響を高めることができます。

![管理アカウントを制御できるようになった敵対者は、それらの権限を使用し、対象となる組織を犠牲にして、利益を追求できることを示す図](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

次の図は、2 つのパスを示しています。

* "青色" のパス。メールや Web 閲覧、日単位の作業など、リソースへの非特権アクセスには、標準ユーザー アカウントを使用します。

   > [!NOTE]
   > 後で説明する青色のパス項目は、管理者アカウントを超えて拡張される広範な環境保護を示しています。

* "赤色" のパス。フィッシングやその他の Web およびメール攻撃のリスクを軽減するために、特権アクセスはセキュリティが強化されたデバイスで発生します。

![Web の閲覧やメールへのアクセスのような危険度の高い標準ユーザーのタスクから特権アクセスのタスクを分離するために、ロードマップによって確立される管理用の個別の "パス" を示す図](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>特権アクセスのセキュリティ保護のロードマップ

ロードマップは、既に展開されている Microsoft テクノロジを最大限に利用し、クラウド テクノロジを活用してセキュリティを向上させ、既に展開されている可能性のあるサード パーティ製のセキュリティ ツールを統合するように設計されています。

Microsoft が推奨するロードマップは、次の 3 つのフェーズに分かれています。

* [フェーズ 1: 最初の 30 日間](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-1-quick-wins-with-minimal-operational-complexity)
   * 有意義なプラスの影響を伴う迅速な勝利。
* [フェーズ 2: 90 日間](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-2-significant-incremental-improvements)
   * 大幅な漸進的な改善。
* [フェーズ 3: 継続](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access#phase-3-security-improvement-and-sustainment)
   * セキュリティの向上と維持。

このロードマップは、これらの攻撃と解決方法の実装に関する経験に基づいて、最も効果的で最も迅速な実装をスケジュールするように、優先順位が設定されています。 

Microsoft では、断固とした敵対者に対して特権アクセスをセキュリティで保護するために、このロードマップに従うことをお勧めします。 既存の機能や、組織固有の要件に対応するように、このロードマップを調整してもかまいません。

> [!NOTE]
> 特権アクセスをセキュリティで保護するには、技術コンポーネント (ホストの防御、アカウントの保護、ID 管理など) を含むさまざまな要素だけでなく、プロセスへの変更や、管理業務と知識が必要になります。 ロードマップのタイムラインは概算であり、お客様の実装の経験に基づきます。 お客様の環境と、変更管理プロセスの複雑さによって、組織内で所要期間が異なることがあります。

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>フェーズ 1: 操作の複雑さを最小限に抑えた迅速な勝利

ロードマップのフェーズ 1 は、資格情報の盗難や悪用で最も頻繁に使用される攻撃手法を迅速に軽減することに焦点を当てています。 フェーズ 1 は約 30 日間で実装するよう設計されており、以下の図に内容を示しています。

![フェーズ 1 の図:1. 管理者とユーザーの個別のアカウント、2. Just in Time ローカル管理者パスワード、3. 管理ワークステーションのステージ 1、4. ID 攻撃の検出](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1.個別のアカウント

インターネット上のリスク (フィッシング攻撃、Web サイトの参閲覧) を特権アクセス アカウントから切り離すために、特権アクセスを持つすべてのスタッフに専用アカウントを作成します。 管理者は、高い特権のアカウントを使用して、Web を閲覧したり、メールをチェックしたり、日常の生産性タスクを実行したりしないでください。 詳細については、参考資料の[個別の管理アカウント](securing-privileged-access-reference-material.md#separate-administrative-accounts)に関するセクションをご覧ください。

オンプレミスの AD 環境と Azure AD 環境の両方で、管理者権限が永続的に割り当てられた、少なくとも 2 つの緊急アクセス用アカウントを作成するには、「[Azure AD で緊急アクセス用アカウントを管理する](/azure/active-directory/users-groups-roles/directory-emergency-access)」の記事のガイダンスに従ってください。 これらのアカウントは、従来の管理者アカウントが障害発生時などに必要なタスクを実行できない場合にのみ使用するためのものです。

### <a name="2-just-in-time-local-admin-passwords"></a>2.Just in Time ローカル管理者パスワード

敵対者がローカルの SAM データベースからローカル管理者アカウントのパスワード ハッシュを盗み、それを悪用してほかのコンピューターを攻撃するリスクを軽減するためには、組織で必ず、各マシンに一意の管理者パスワードを設定する必要があります。 ローカル管理者パスワード ソリューション (LAPS) ツールでは、ワークステーションごとに一意のランダム パスワードを構成できます。サーバーはそれらを、ACL によって保護された Active Directory (AD) に保存します。 これらのローカル管理者アカウントのパスワードのリセットを読み取ったり要求したりできるのは、資格のある承認済みユーザーのみです。 ワークステーションとサーバーで使用するための LAPS は [Microsoft ダウンロード センター](https://aka.ms/LAPS)で取得できます。

LAPS と PAW を使用する環境に関する追加のガイダンスは、「[クリーン ソースの原則に基づく運用基準](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle)」のセクションでご確認いただけます。

### <a name="3-administrative-workstations"></a>3.管理ワークステーション

Azure Active Directory と従来のオンプレミス Active Directory の管理者特権を持つユーザーのための最初のセキュリティ対策として、それらのユーザーが、[セキュリティが強化された Windows 10 デバイスの標準](/windows-hardware/design/device-experiences/oem-highly-secure)で構成された Windows 10 デバイスを使用していることを確認します。 特権のある管理者アカウントは、管理ワークステーションのローカル管理者グループのメンバーになることはできません。  ワークステーションに対する構成の変更が必要な場合は、ユーザー アクセス制御 (UAC) による特権の昇格を利用できます。  さらに、Windows 10 セキュリティ ベースラインをワークステーションに適用して、デバイスをさらに強化する必要があります。

### <a name="4-identity-attack-detection"></a>4.ID 攻撃の検出

[Azure Advanced Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp) はクラウド ベースのセキュリティ ソリューションであり、オンプレミスの Active Directory 環境を対象とする高度な脅威、侵害された ID、および悪意のあるインサイダーによるアクションの識別、検出、調査支援を行います。

## <a name="phase-2-significant-incremental-improvements"></a>フェーズ 2:大幅な漸進的な改善

フェーズ 2 は、フェーズ 1 で実行された作業に基づいており、約 90 日間で完了するように設計されています。 このステージの手順を次の図で示します。

![フェーズ 2 の図:1. Windows Hello for Business/MFA、2. PAW のロールアウト、3. Just in Time 特権、4. Credential Guard、5. 漏洩した資格情報、6. 横方向の移動の脆弱性の検出](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1.Windows Hello for Business と MFA が必要

管理者は、Windows Hello for Business に関連した使いやすさを活用できます。 管理者は、複雑なパスワードを PC の強力な 2 要素認証に置き換えることができます。 攻撃者はデバイスと生体認証情報または PIN の両方を手に入れる必要があり、従業員に知られずにアクセスを獲得することは非常に困難です。 Windows Hello for Business とロールアウトのパスの詳細については、[Windows Hello for Business の概要](/windows/security/identity-protection/hello-for-business/hello-overview)に関する記事を参照してください

Azure MFA を使用した Azure AD で、管理者アカウントの多要素認証 (MFA) を有効にします。 少なくとも、[ベースライン保護の条件付きアクセス ポリシー](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins)を有効にします。Azure Multi-Factor Authentication の詳細については、[クラウドベースの Azure Multi-Factor Authentication の Azure のデプロイ](/azure/active-directory/authentication/howto-mfa-getstarted)に関する記事を参照してください

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2.すべての特権付き ID アクセス アカウントの所有者に PAW をデプロイする

メール、Web 閲覧、およびその他の管理以外のタスクで検出された脅威から特権アカウントを分離するプロセスを続行するには、組織の情報システムへの特権アクセス権を持つすべての担当者に専用の特権アクセス ワークステーション (PAW) を実装する必要があります。 PAW のデプロイに関するその他のガイダンスについては、[特権アクセス ワークステーション](privileged-access-workstations.md#paw-phased-implementation)に関する記事を参照してください。

### <a name="3-just-in-time-privileges"></a>3.Just in Time 特権

特権の露出時間を削減し、使用の可視性を増やすには、次のように適切なソリューションや他のサードパーティのソリューションを使用して Just-In-Time (JIT) で特権を付与します。

* Active Directory Domain Services (AD DS) の場合は、Microsoft Identity Manager (MIM) の[特権アクセス マネージャー (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 機能を使用してください。
* Azure Active Directory の場合は、[Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 機能を使用してください。

### <a name="4-enable-windows-defender-credential-guard"></a>4.Windows Defender Credential Guard を有効にする

Credential Guard を有効にすると、NTLM パスワード ハッシュ、Kerberos チケット保証チケット、およびアプリケーションによってドメイン資格情報として保存された資格情報を保護することができます。 この機能により、盗難に遭った資格情報を使用した環境でのピボットの難易度を高めることで、Pass-the-Hash や Pass-the-Ticket などの資格情報盗用攻撃を防ぐことができます。 Credential Guard のしくみと展開方法については、「[Windows Defender Credential Guard によるドメインの派生資格情報の保護](/windows/security/identity-protection/credential-guard/credential-guard)」の記事をご覧ください。

### <a name="5-leaked-credentials-reporting"></a>5.漏洩した資格情報レポート

"Microsoft では、毎日、新たな脅威を特定し、顧客を保護するために、6 兆 5000 億の信号を分析しています" - [Microsoft By the Numbers](https://news.microsoft.com/bythenumbers/cyber-attacks)

Microsoft Azure AD Identity Protection を有効にすると、資格情報が漏洩したユーザーについてレポートを作成し、修復できるようにすることができます。 [Azure AD Identity Protection](/azure/active-directory/identity-protection/index) を利用して、組織が脅威からクラウド環境やハイブリッド環境を保護できるようにすることができます。

### <a name="6-azure-atp-lateral-movement-paths"></a>6.Azure ATP の横移動パス

特権アクセス アカウントの所有者が PAW を管理にのみ使用していることを確認して、侵害された特権のないアカウントが、Pass-the-Hash や Pass-the-Ticket などの資格情報盗用攻撃を介して特権アカウントにアクセスできないようにします。 [Azure ATP の横移動パス (LMP)](/azure-advanced-threat-protection/use-case-lateral-movement-path) では、特権アカウントが危険にさらされる可能性がある場所を特定するためのレポートを簡単に理解できます。

## <a name="phase-3-security-improvement-and-sustainment"></a>フェーズ 3: セキュリティの向上と維持

ロードマップのフェーズ 3 では、フェーズ 1 と 2 で実行した手順に基づいて、セキュリティ体制を強化します。 次の図にフェーズ 3 を視覚的に表現します。

![フェーズ 3: 1. RBAC を確認する、2. 攻撃を受ける可能性の低減、3. ログを SEIM と統合する、4. 漏洩した資格情報の自動化](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

これらの機能は前のフェーズからの手順を基盤とし、防御策をより予防的なものにします。 このフェーズには特定のタイムラインはなく、個々の組織に基づいて実装する時間が長くなる場合があります。

### <a name="1-review-role-based-access-control"></a>1.ロールベースのアクセス制御を確認する

「[Active Directory 管理層モデル](securing-privileged-access-reference-material.md)」の記事で説明されている 3 つの階層モデルを使用して、下位層の管理者が上位層のリソース (グループ メンバーシップ、ユーザー アカウントの ACL など) への管理アクセス権を持っていないことを確認します。

### <a name="2-reduce-attack-surfaces"></a>2.攻撃を受ける可能性の低減

ドメイン、ドメイン コントローラー、ADFS、Azure AD Connect などのシステムのいずれかが侵害されると、組織内の他のシステムが侵害される可能性があるため、これらの ID ワークロードを強化します。 「[Active Directory の攻撃を削減する](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md)」および「[ID インフラストラクチャを保護するための 5 つのステップ](/azure/security/azure-ad-secure-steps)」の記事で、オンプレミス環境とハイブリッド ID 環境をセキュリティで保護するためのガイダンスを提供しています。

### <a name="3-integrate-logs-with-siem"></a>3.ログを SIEM と統合する

一元管理された SIEM ツールにログを統合することにより、組織でセキュリティ イベントの分析、検出、対応を行うことができます。 「[Active Directory の侵害の兆候を監視する](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md)」および「[付録 L: 監視するイベント](../ad-ds/plan/appendix-l--events-to-monitor.md)」の記事で、環境で監視する必要があるイベントに関するガイダンスを提供しています。

セキュリティ情報およびイベント管理 (SIEM) でのアラートの集計、作成、およびチューニングには熟練したアナリストが必要なため、これは計画を超える部分です (すぐに使用できるアラートが含まれている 30 日の計画の Azure ATP とは異なります)

### <a name="4-leaked-credentials---force-password-reset"></a>4.漏洩した資格情報 - パスワードのリセットを強制する

パスワードが侵害された疑いがある場合に、Azure AD Identity Protection でパスワードのリセットを自動的に強制できるようにすることで、引き続きセキュリティ体制を強化します。 「[リスク イベントを使用して多要素認証とパスワード変更をトリガーする](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa)」の記事のガイダンスで、条件付きアクセス ポリシーを使用してこれを有効にする方法について説明しています。

## <a name="am-i-done"></a>ロードマップの完了

一言で答えると「いいえ」です。

悪意のある人は決して止まることがないため、あなたも止まることはできません。 攻撃者は絶えず進化し、うまく立ち回っていきますが、このロードマップは、現在知られている脅威から組織を保護するのに役立ちます。 ご使用の環境を狙う敵対者のコストを増加させることと、成功率を減らすことに重点を置いた継続的なプロセスとしてセキュリティを監視することをお勧めします。

組織のセキュリティ プログラムの唯一の部分ではありませんが、特権アクセスをセキュリティで保護することは、セキュリティ戦略の重要な要素です。
