---
title: 特権アクセスの保護
description: 特権アクセスをセキュリティで保護する段階的アプローチ
ms.prod: windows-server
ms.topic: conceptual
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
ms.date: 02/25/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: e6ff22d0563fa11aa633004966b2cd2648ba5877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357705"
---
# <a name="securing-privileged-access"></a>特権アクセスの保護

>適用先:Windows Server

特権アクセスをセキュリティで保護することは、現代の組織においてビジネス資産のセキュリティ保証を確立するための重要な第一歩です。 IT 組織内のほとんどまたはすべてのビジネス資産のセキュリティは、の管理、管理、および開発に使用される特権アカウントの整合性に依存します。 サイバー攻撃者は、多くの場合、これらのアカウントおよび特権アクセスの他の要素をターゲットにして、[ハッシュのパススルーやチケットのパススルー](https://www.microsoft.com/pth)などの資格情報の盗難攻撃を使用してデータとシステムにアクセスできるようにします。

特定された敵対者に対する特権アクセスを保護するには、これらのシステムをリスクから分離するための完全で慎重なアプローチを行う必要があります。

## <a name="what-are-privileged-accounts"></a>特権アカウントとは

セキュリティ保護の方法について説明する前に、特権アカウントを定義します。

Active Directory Domain Services の管理者などの特権アカウントは、IT 組織内のほとんどまたはすべての資産に直接または間接的にアクセスできます。そのため、これらのアカウントのセキュリティが重大なリスクになります。

## <a name="why-securing-privileged-access-is-important"></a>特権アクセスをセキュリティで保護することが重要な理由

サイバー攻撃者は、Active Directory (AD) などのシステムへの特権アクセスに重点を置いて、組織が対象とするすべてのデータに迅速にアクセスできるようにします。 従来のセキュリティ手法は、主なセキュリティ境界としてネットワークとファイアウォールに焦点を合わせていますが、ネットワークセキュリティの効果は、次の2つの傾向によって大幅に低下しています。

* 組織は、モバイルエンタープライズ Pc、携帯電話やタブレットなどのデバイス、クラウドサービス、独自のデバイス (BYOD) を使用して、従来のネットワーク境界の外部にあるデータとリソースをホストしています。
* 敵対者は、フィッシングやその他の Web および電子メール攻撃を通じて、ネットワーク境界内のワークステーションへのアクセスを入手する、一貫性のある継続的な能力を実証しています。

これらの要因により、従来のネットワーク境界戦略に加えて、認証および承認 id の制御から、最新のセキュリティ境界を構築することができます。 ここでのセキュリティ境界は、アセットとそれらに対する脅威との間の一貫したコントロールのセットとして定義されています。 特権アカウントは、この新しいセキュリティ境界を効果的に制御できるため、特権アクセスを保護することが重要です。

![組織の ID 層を示す図](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

管理者アカウントの制御を獲得した攻撃者は、次に示すように、これらの権限を使用して、ターゲット組織への影響を高めることができます。

![管理アカウントを制御できるようになった敵対者は、それらの権限を使用し、対象となる組織を犠牲にして、利益を追求できることを示す図](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

次の図は、2つのパスを示しています。

* "Blue" パス。電子メールや web 閲覧、日単位の作業など、リソースへの非特権アクセスに標準ユーザーアカウントを使用します。

   > [!NOTE]
   > 後で説明する青いパス項目は、管理者アカウントを超えて拡張される広範な環境保護を示しています。

* セキュリティが強化されたデバイスで特権アクセスが発生し、フィッシングやその他の web および電子メール攻撃のリスクを軽減する "赤い" パス。

![Web 閲覧や電子メールへのアクセスなどの危険度の高い標準ユーザータスクから特権アクセスタスクを分離するために、ロードマップによって確立される管理用の個別の "パス" を示す図](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

## <a name="securing-privileged-access-roadmap"></a>特権アクセスのロードマップのセキュリティ保護

このロードマップは、既にデプロイされている Microsoft テクノロジの使用を最大化し、クラウドテクノロジを利用してセキュリティを強化し、既にデプロイされている可能性のあるサードパーティ製のセキュリティツールを統合するように設計されています。

Microsoft の推奨事項のロードマップは、次の3つのフェーズに分かれています。

* [フェーズ 1:最初の30日間]()
   * 重要なプラス効果を持つクイック wins。
* [フェーズ 2:90日]()
   * 大幅な増分向上。
* [フェーズ 3:メンテナンス]()
   * セキュリティの向上と sustainment。

このロードマップは、これらの攻撃と解決方法の実装に関する経験に基づいて、最も効果的で最も迅速な実装をスケジュールするように、優先順位が設定されています。 

Microsoft では、断固とした敵対者に対して特権アクセスをセキュリティで保護するために、このロードマップに従うことをお勧めします。 既存の機能や、組織固有の要件に対応するように、このロードマップを調整してもかまいません。

> [!NOTE]
> 特権アクセスをセキュリティで保護するには、技術コンポーネント (ホストの防御、アカウントの保護、ID 管理など) を含むさまざまな要素だけでなく、プロセスへの変更や、管理業務と知識が必要になります。 ロードマップのタイムラインは概算であり、お客様の実装の経験に基づきます。 お客様の環境と、変更管理プロセスの複雑さによって、組織内で所要期間が異なることがあります。

## <a name="phase-1-quick-wins-with-minimal-operational-complexity"></a>フェーズ 1:操作の複雑さを最小限に抑えたクイック wins

ロードマップのフェーズ1では、最も頻繁に使用される、資格情報の盗難および誤用の攻撃手法を迅速に軽減することに重点を置いています。 フェーズ1は、約30日以内に実装するように設計されており、次の図に示しています。

![フェーズ1の図:1. 別の管理者とユーザーアカウント、2。 ジャストインタイムローカル管理者パスワード、3。 管理ワークステーションステージ1、4。 Id 攻撃の検出](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

### <a name="1-separate-accounts"></a>1. 個別のアカウント

特権アクセスアカウントからインターネットのリスク (フィッシング攻撃、web 閲覧) を分離するために、特権アクセスを持つすべてのユーザーに専用のアカウントを作成します。 管理者は、高度な特権を持つアカウントを使用して、web を閲覧したり、電子メールをチェックしたり、日常の生産性タスクを実行したりしないでください。 詳細については、「リファレンスドキュメントの[個別の管理者アカウント](securing-privileged-access-reference-material.md#separate-administrative-accounts)」を参照してください。

オンプレミスの AD 環境と Azure AD 環境の両方で、管理者権限が永続的に割り当てられた、少なくとも2つの緊急アクセスアカウントを作成するには、 [Azure AD の緊急アクセスアカウントの管理](/azure/active-directory/users-groups-roles/directory-emergency-access)に関する記事のガイダンスに従ってください。 これらのアカウントは、従来の管理者アカウントが障害発生時などに必要なタスクを実行できない場合にのみ使用されます。

### <a name="2-just-in-time-local-admin-passwords"></a>2. ジャストインタイムローカル管理者パスワード

攻撃者がローカルの SAM データベースからローカルの管理者アカウントのパスワードハッシュを盗み、他のコンピューターを攻撃するリスクを軽減するために、組織はすべてのコンピューターに一意のローカル管理者パスワードがあることを確認する必要があります。 ローカル管理者パスワードソリューション (LAPS) ツールでは、ワークステーションごとに一意のランダムパスワードを構成できます。また、サーバーは、ACL によって保護された Active Directory (AD) に格納します。 資格のある権限のあるユーザーのみが、これらのローカル管理者アカウントのパスワードのリセットを読み取りまたは要求できます。 ワークステーションとサーバーで使用する LAPS は、 [Microsoft ダウンロードセンター](http://Aka.ms/LAPS)から入手できます。

LAPS と Paw で環境を運用するための追加のガイダンスについては、「[クリーンソースの原則に基づく運用標準](securing-privileged-access-reference-material.md#operational-standards-based-on-clean-source-principle)」を参照してください。

### <a name="3-administrative-workstations"></a>3.管理ワークステーション

Azure Active Directory と従来のオンプレミス Active Directory 管理者特権を持つユーザーのための最初のセキュリティ対策として、セキュリティが強化された[windows 10 デバイスの標準で構成された windows 10 デバイスを使用していることを確認します。](/windows-hardware/design/device-experiences/oem-highly-secure). 特権のある管理者アカウントは、管理ワークステーションのローカル管理者グループのメンバーになることはできません。  ワークステーションに対する構成の変更が必要な場合は、ユーザー Access Control (UAC) による特権昇格を利用できます。  さらに、Windows 10 のセキュリティベースラインをワークステーションに適用して、デバイスをさらに強化する必要があります。

### <a name="4-identity-attack-detection"></a>4。Id 攻撃の検出

[Azure Advanced Threat Protection (ATP)](/azure-advanced-threat-protection/what-is-atp)は、クラウドベースのセキュリティソリューションであり、高度な脅威、侵害された id、オンプレミスに送られる悪意のある insider アクションを識別、検出、および調査するのに役立ち Active Directoryenvironment.

## <a name="phase-2-significant-incremental-improvements"></a>フェーズ 2:大幅な増分向上

フェーズ2は、フェーズ1で実行された作業に基づいており、約90日以内に完了するように設計されています。 このステージの手順を次の図で示します。

![フェーズ2の図:1. Windows Hello for Business/MFA、2 です。 PAW ロールアウト、3。 ジャストインタイムの特権、4。 Credential Guard、5。 漏洩した資格情報、6。 横移動の脆弱性の検出](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

### <a name="1-require-windows-hello-for-business-and-mfa"></a>1. Windows Hello for Business と MFA が必要

管理者は、Windows Hello for Business に関連付けられている使いやすさを活用できます。 管理者は、複雑なパスワードを Pc の強力な2要素認証に置き換えることができます。 攻撃者は、デバイスと生体認証情報または PIN の両方を持っている必要があります。これにより、従業員の知識がなくてもアクセスが困難になります。 Windows Hello for Business とロールアウトへのパスの詳細については、情報の記事では[Windows Hello for Business の概要](/windows/security/identity-protection/hello-for-business/hello-overview)

Azure MFA を使用した Azure AD で、管理者アカウントの multi-factor authentication (MFA) を有効にします。 少なくとも、[ベースライン保護条件付きアクセスポリシー](/azure/active-directory/conditional-access/baseline-protection#require-mfa-for-admins)を有効にします。 azure Multi-Factor Authentication の詳細については、「[クラウドベースの azure のデプロイ Multi-Factor Authentication](/azure/active-directory/authentication/howto-mfa-getstarted) 」を参照してください。

### <a name="2-deploy-paw-to-all-privileged-identity-access-account-holders"></a>2. すべての特権 id アクセスアカウントの所有者に PAW をデプロイする

電子メール、web 閲覧、およびその他の管理以外のタスクで検出された脅威から特権アカウントを分離するプロセスを続行するには、の特権アクセスを持つすべての担当者に専用の Privileged Access Workstation (PAW) を実装する必要があります。組織の情報システム。 PAW のデプロイに関するその他のガイダンスについては、「 [Privileged Access workstation](privileged-access-workstations.md#paw-phased-implementation)」を参照してください。

### <a name="3-just-in-time-privileges"></a>3.ジャストインタイムの特権

特権の公開時間を短縮し、使用状況の可視性を向上させるには、以下のような適切なソリューションを使用してジャストインタイム (JIT) を提供し、その他のサードパーティソリューションを使用します。

* Active Directory Domain Services (AD DS) の場合は、Microsoft Identity Manager (MIM) の[特権アクセス マネージャー (PAM)](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 機能を使用してください。
* Azure Active Directory の場合は、[Azure AD Privileged Identity Management (PIM)](/azure/active-directory/privileged-identity-management/pim-deployment-plan) 機能を使用してください。

### <a name="4-enable-windows-defender-credential-guard"></a>4。Windows Defender Credential Guard を有効にする

Credential Guard を有効にすると、NTLM パスワードハッシュ、Kerberos チケット保証チケット、およびアプリケーションによってドメイン資格情報として格納されている資格情報を保護することができます。 この機能により、流用された資格情報を使用して環境内でピボットを行うことが困難になるため、ハッシュのパススルーやチケットのパススルーなど、資格情報の盗難攻撃を防ぐことができます。 Credential Guard のしくみとデプロイ方法については、「 [Windows Defender Credential guard による派生ドメイン資格情報の保護](/windows/security/identity-protection/credential-guard/credential-guard)」を参照してください。

### <a name="5-leaked-credentials-reporting"></a>5。漏洩した資格情報の報告

"毎日、マイクロソフトは、新たな脅威を特定し、顧客を保護するために、6兆5000億の信号を分析し[ます](https://news.microsoft.com/bythenumbers/cyber-attacks)。

Microsoft Azure AD Id 保護を有効にすると、資格情報が漏洩したユーザーに対してレポートを作成し、修復できます。 [Azure AD Identity Protection](/azure/active-directory/identity-protection/index)は、組織が脅威からクラウド環境やハイブリッド環境を保護するのに役立ちます。

### <a name="6-azure-atp-lateral-movement-paths"></a>6。横移動パスの Azure ATP

特権アクセスアカウントの所有者が PAW を管理にのみ使用していることを確認します。これにより、侵害されていない権限のないアカウントは、ハッシュパスやパススルーチケットなどの資格情報の盗難攻撃を通じて特権アカウントにアクセスできなくなります。 [Azure ATP 横移動パス (LMPs)](/azure-advanced-threat-protection/use-case-lateral-movement-path)を使用すると、特権のあるアカウントが危険にさらされる可能性がある場所を特定するためのレポートを簡単に把握できます。

## <a name="phase-3-security-improvement-and-sustainment"></a>フェーズ 3:セキュリティの向上と sustainment

ロードマップのフェーズ3では、セキュリティ体制を強化するために、フェーズ1と2で作成した手順について説明します。 フェーズ3は、次の図のように視覚的に表されます。

![フェーズ 3:1. RBAC、2を確認します。 攻撃対象領域を減らします。 3. ログを SEIM, 4 と統合します。 漏洩した資格情報の自動化](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

これらの機能は、前のフェーズの手順に基づいて構築され、防御をより積極的な体制に移行します。 このフェーズには特定のタイムラインはありません。個々の組織に基づいて実装する時間が長くなる場合があります。

### <a name="1-review-role-based-access-control"></a>1. ロールベースのアクセス制御を確認する

「[管理層モデル Active Directory](securing-privileged-access-reference-material.md)」の記事に記載されている3つの階層モデルを使用して、下位層の管理者が上位層のリソース (グループメンバーシップ、ユーザーアカウントの acl など) への管理アクセス権を持っていないことを確認します。

### <a name="2-reduce-attack-surfaces"></a>2. 攻撃対象領域の削減

ドメイン、ドメインコントローラー、ADFS、Azure AD Connect などの id ワークロードを強化することにより、これらのシステムのいずれかを侵害すると、組織内の他のシステムが侵害される可能性があります。 この記事では、 [Active Directory の攻撃対象領域を減らし](../ad-ds/plan/security-best-practices/reducing-the-active-directory-attack-surface.md)、 [id インフラストラクチャをセキュリティで保護する5つの手順](/azure/security/azure-ad-secure-steps)を説明します。オンプレミス環境とハイブリッド id 環境をセキュリティで保護するためのガイダンスを提供します。

### <a name="3-integrate-logs-with-siem"></a>3.ログを SIEM と統合する

集中管理された SIEM ツールにログを統合することにより、組織はセキュリティイベントの分析、検出、対応を行うことができます。 この記事では、[セキュリティ侵害の兆候](../ad-ds/plan/security-best-practices/monitoring-active-directory-for-signs-of-compromise.md)と[付録 L の Active Directory を監視しています。監視](../ad-ds/plan/appendix-l--events-to-monitor.md)するイベントは、環境内で監視する必要があるイベントに関するガイダンスを提供します。

これは、セキュリティ情報およびイベント管理 (SIEM) でのアラートの集計、作成、およびチューニングに熟練した Azure ATP アナリストが必要であるため、それ以上の計画に含まれています。

### <a name="4-leaked-credentials---force-password-reset"></a>4。漏洩した資格情報-パスワードのリセットを強制する

パスワードが侵害された場合にパスワードのリセットを自動的に強制的に強制するように Azure AD Identity Protection を有効にすることで、セキュリティ対策を継続的に強化します。 記事「 [Multi-Factor Authentication とパスワードの変更をトリガーするためのリスクイベントの使用](/azure/active-directory/authentication/tutorial-risk-based-sspr-mfa)」で説明されているガイダンスでは、条件付きアクセスポリシーを使用してこれを有効にする方法について説明します。

## <a name="am-i-done"></a>ロードマップの完了

短い回答は、"いいえ" です。

悪意のある人が決して停止することはないため、どちらもできません。 このロードマップは、攻撃者が絶えず進化していくため、現在認識されている脅威に対する組織の保護に役立ちます。 環境をターゲットとする敵対者の成功率を減らすことに重点を置いて、継続的なプロセスとしてセキュリティを確認することをお勧めします。

組織のセキュリティプログラムの唯一の部分ではありませんが、特権アクセスのセキュリティ保護は、セキュリティ戦略の重要な要素です。
