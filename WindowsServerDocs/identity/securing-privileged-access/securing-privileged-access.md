---
title: "特権アクセスをセキュリティで保護します。"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5dec0c2-06fe-4c91-9bdc-67cc6a3ede60
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: eb83903204b00ef6c1eb116554ec54bc2211a399
ms.sourcegitcommit: 7b01b54032ec56432116626e08fbd92508c3a7d5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/09/2018
---
# <a name="securing-privileged-access"></a>特権アクセスをセキュリティで保護します。

>Windows Server 2016 の適用対象:

特権のあるセキュリティで保護するアクセスは、現代の組織のビジネス資産のセキュリティ保証を確立するための重要な第一歩です。 組織内のほとんどまたはすべてのビジネス資産のセキュリティは、IT システムを管理する特権アカウントの整合性に依存します。 サイバー攻撃には、これらのアカウントと対象のデータおよびシステムのような資格情報盗難攻撃を使用する場合に迅速にアクセスする特権アクセスの他の要素が対象とする、[-Pass-the-hash およびチケット Pass](https://www.microsoft.com/pth)します。

に対して管理アクセス権を保護するには、敵対者では、これらのシステム リスクからを分離する完全かつ当てはめるアプローチを採用する必要がありますが決定されます。 この図は、分離し、このロードマップで管理を保護するための推奨事項の 3 つの段階を示します。

![分離し、このロードマップで管理を保護するための推奨事項の 3 つのステージの図](../media/securing-privileged-access/PAW_LP_Fig1.JPG)

ロードマップ目標:

-   **2-4 週間計画**: 最も頻繁に使用される攻撃手法を迅速に軽減

-   **1-3 か月計画**: 可視性と管理アクティビティの制御を構築

-   **6 か月超計画**: より予防的なセキュリティ体制を防策の確立を継続

特定された敵対者に対して特権アクセスをセキュリティで保護するには、このロードマップに従うことをお勧めします。 既存の機能と、組織内の特定の要件に対応するためには、このロードマップを調整することがあります。

> [!NOTE]
> 特権のあるセキュリティで保護するアクセスには、広範な技術コンポーネント (ホストの防御、アカウントの保護、id 管理など) だけでなく、プロセスへの変更などの要素と管理業務と知識が必要です。

## <a name="why-is-securing-privileged-access-important"></a>重要な特権アクセスをセキュリティで保護するなぜですか。
ほとんどの組織では、ほとんどまたはすべてのビジネス資産のセキュリティは、IT システムを管理する特権アカウントの整合性に依存します。 サイバー攻撃者に重点を置いてシステムへのアクセス権限のすべての組織に迅速にアクセスするための Active Directory データを対象とするようにします。

従来のセキュリティの手法が、主要なセキュリティ境界として組織ネットワークの入口と出口のポイントを使用してに重点を置いてがネットワークのセキュリティの有効性が 2 つの傾向を大幅に低下しました。

-   組織では、データとモバイル エンタープライズ Pc、従来のネットワークの境界の外部にあるリソース、携帯電話、タブレット、クラウド サービスなどのデバイスおよび BYOD デバイスをホストしています。

-   敵対者は、フィッシングやその他の Web および電子メール攻撃を通じて、ネットワーク境界内のワークステーションのアクセスを取得する一貫した継続的な能力を実証されました。

複雑な現代の企業でネットワーク セキュリティの境界の自然な代替は、組織の ID 層で認証と承認のコントロールです。 特権管理アカウントはこの新しい「セキュリティ境界」のコントロールで効果的に特権アクセスを保護することが重要ようにします。

![組織の ID 層を示す図](../media/securing-privileged-access/PAW_LP_Fig2.JPG)

管理者アカウントの制御を取得した敵対者は、以下の図のように対象となる組織を犠牲にして、利益を追求するのにそれらの権限を使用できます。

![管理者アカウントの制御を獲得している攻撃者がそれらの権限を使用して、対象となる組織を犠牲にして、利益を追求する方法を示す図](../media/securing-privileged-access/PAW_LP_Fig3.JPG)

一般的に攻撃者による管理アカウントの制御につながる攻撃の種類の詳細についてを参照してください、[Pass The Hash Web サイト](https://www.microsoft.com/pth)ホワイト ペーパー、ビデオなどのためです。

この図は、ロードマップは、Web の閲覧や電子メールへのアクセスのような危険度の高い標準ユーザー タスクから特権アクセスのタスクを分離によって確立される管理用の個別の「チャネル」を示しています。

![管理用 Web の閲覧や電子メールへのアクセスのような危険度の高い標準ユーザー タスクから特権アクセスのタスクを分離する、ロードマップによって確立する個別の「チャネル」を示す図](../media/securing-privileged-access/PAW_LP_Fig4.JPG)

のさまざまな方法を使用して特権アクセスの制御できるように、敵対者は、このリスクを軽減が必要に包括的かつ詳細な技術的アプローチこのロードマップで説明したようにします。 ロードマップは分離し、この図の防御列の各領域で軽減策を構築して特権アクセスを有効にする環境内で要素のセキュリティを強化します。

![攻撃と防御の列を示す表](../media/securing-privileged-access/PAW_LP_Fig5.JPG)

## <a name="security-privileged-access-roadmap"></a>セキュリティ特権アクセスのロードマップ
ロードマップが既にありますテクノロジを最大限に利用するように設計、展開されている、現在および今後の主要なセキュリティ テクノロジを活用し、サード パーティ製セキュリティ ツールが既に展開したを統合します。

マイクロソフトの推奨事項のロードマップは、3 つのステージに分かれています。

-   2 ~ 4 週間計画 - 最も頻繁に使用される攻撃手法を迅速に軽減

-   1-3 か月計画 - 可視性と管理アクティビティの制御を構築

-   6 か月超計画 - より予防的なセキュリティ体制を防策の確立を継続

ロードマップの各ステージは、コストと特権アクセスを社内の攻撃し、クラウドの資産を敵対者の難易度を上げるに設計されています。 ロードマップは、優先順位を最も効果的なと最初にこれらの攻撃やソリューションの実装の経験に基づいた最も迅速な実装スケジュールを設定します。

> [!NOTE]
> ロードマップのタイムラインは概算であり、経験とお客様の実装に基づいています。 お客様の環境と、変更管理プロセスの複雑さに応じて、組織では、期間によって異なります。

### <a name="security-privileged-access-roadmap-stage-1"></a>セキュリティ特権アクセスのロードマップ: ステージ 1
ロードマップのステージ 1 は、資格情報の盗難や悪用の最も頻繁に使用される攻撃手法を迅速に軽減するのに重点を置いています。 ステージ 1 は約 2 ~ 4 週間で実装するよう設計されています。と、次の図に示すようには。

![そのステージ 1 を示す図が約 2 ~ 4 週間で実装するように設計されています](../media/securing-privileged-access/PAW_LP_Fig6.JPG)

セキュリティ特権アクセスのロードマップのステージ 1 は、これらのコンポーネントが含まれます。

**1. 管理者アカウントの管理タスク用の分離します。**

インターネット上のリスクを切り離すために (フィッシング攻撃、Web の閲覧) から管理者特権は、管理者特権を持つすべてのスタッフに専用アカウントを作成します。 公開された PAW の手順で追加のガイダンスについては、これが含まれている[ここ](http://Aka.ms/CyberPAW)します。

**2. privileged Access Workstation (Paw) フェーズ 1: Active Directory 管理者**

インターネット上のリスクを切り離すために (フィッシング攻撃、Web の閲覧) をドメイン管理特権から AD 管理特権を持つ担当者の専用の特権アクセス ワークステーション (Paw) を作成します。 これは PAW プログラムの最初の手順は、公開されているガイダンスのフェーズ 1[ここ](http://Aka.ms/CyberPAW)します。

**3。ワークステーションの一意のローカル管理者パスワード**

**4。サーバーの一意のローカル管理者パスワード**

敵対者は、それを悪用して、ローカルの SAM データベースからローカル管理者アカウントのパスワード ハッシュを盗むその他のコンピューターを攻撃するリスクを軽減するには、各ワークステーションとサーバーで一意のランダムなパスワードを構成して、それらのパスワードを Active Directory に登録する、LAPS ツールを使用する必要があります。 ワークステーションとサーバーで使用するローカル管理者パスワード ソリューションを取得する[ここ](http://Aka.ms/LAPS)します。

LAPS と Paw を使用する環境に関する追加のガイダンスを参照して[ここ](http://aka.ms/securitystandards)します。

### <a name="security-privileged-access-roadmap-stage-2"></a>セキュリティ特権アクセスのロードマップ: ステージ 2
第 2 段階では、ステージ 1 の軽減策を構築し、約 1-3 か月で実装するよう設計されています。 このステージの手順は次の図に示すようにします。

![第 2 段階の手順を示す図](../media/securing-privileged-access/PAW_LP_Fig7.JPG)

**1 PAW フェーズ 2 および 3: すべての管理者およびその他の強化。**

すべての管理特権アカウントからインターネット上のリスクを個別には、ステージ 1 で開始した PAW を続行し、特権アクセスを持つすべてのスタッフに専用のワークステーションを実装します。 ガイダンスのフェーズ 2 および 3 にマップされるこの公開[ここ](http://Aka.ms/CyberPAW)します。

**2. 期限付きの特権 (非永続的な管理者)**

特権の露出時間を削減し、その使用に可視性が向上には、ジャスト イン タイム (JIT) 次のように適切なソリューションを使用して権限を提供します。

-   Active Directory ドメイン サービス (AD DS)、Microsoft Identity Manager (MIM) の使用[Privileged Access Manager (PAM)](https://technet.microsoft.com/en-us/library/mt150258.aspx)機能します。

-   Azure Active Directory で使用[Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM)機能します。

**3 期限付き昇格の multi-factor です。**

管理者認証の保証レベルを上げるためには、権限を付与する前に、多要素認証を必要とする必要があります。
これは、MIM PAM と Azure の多要素認証 (MFA) を使用して Azure AD PIM で実現できます。

**4。DC のメンテナンスのための just Enough Admin (JEA)**

ドメイン管理特権を持ち、関連するリスクの露出を持つアカウントの数を減らすためには、PowerShell の Just Enough Administration (JEA) 機能を使用して、ドメイン コントローラー上の一般的なメンテナンス操作を実行します。 JEA テクノロジにより、特定のユーザー (ドメイン コントローラー) などのサーバーで管理者権限を与えることがなく特定の管理タスクを実行します。 このガイドからのダウンロード[TechNet](http://aka.ms/JEA)します。

**5。ドメインおよび Dc の攻撃対象領域を低い**

敵対者のフォレストを制御するための機会を減らすためには、ドメイン コントローラーまたはドメインのコントロール内のオブジェクトを制御する攻撃者が利用の経路を減らす必要があります。 公開されたこのリスクを軽減するガイダンスに従ってください[ここ](http://aka.ms/HardenAD)します。

**6. 攻撃の検出**

アクティブな資格情報の盗難や ID に可視性を取得する攻撃できるように、イベントに迅速に対応して、破損が含まれている展開して構成する[Microsoft Advanced Threat Analytics (ATA)](https://www.microsoft.com/ata)します。

ATA をインストールする前に ATA が検出する大きなセキュリティ インシデントに対処するために、プロセスがあることを確認する必要があります。

-   インシデント レスポンス プロセスの設定の詳細については、次を参照してください。[IT セキュリティ インシデントへの応答](https://aka.ms/irr)と、"への応答の疑わしいアクティビティ"と"侵害から Recover"のセクションの[Mitigating-Pass-the-hash およびその他の資格情報の盗難](https://www.microsoft.com/pth)、バージョン 2 です。

-   ATA が生成するイベントや ATA を展開するための IR プロセスの準備を支援する Microsoft サービスとの提携によるについて詳しくは、アクセスすることによって、Microsoft の担当者にお問い合わせください。[このページ](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)します。

-   アクセス[このページ](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)インシデントからの回復や調査を支援する Microsoft サービスの利用の詳細については

-   実装 ata、利用可能な展開ガイドに従います[ここ](http://aka.ms/ata)します。

### <a name="security-privileged-access-roadmap-stage-3"></a>セキュリティ特権アクセスのロードマップ: ステージ 3
ロードマップのステージ 3 を強化し、幅広く軽減策を追加するには、ステージ 1 と 2 の軽減策を構築します。 次の図にステージ 3 を視覚的に示します。

![ステージ 3 を示す図](../media/securing-privileged-access/PAW_LP_Fig8.JPG)

これらの機能を前のフェーズからの軽減策を構築し、防策をより予防的な体制に移動します。

**1。役割および委任モデルの現代化します。**

セキュリティ上のリスクを減らすためには、役割と委任モデルの階層モデルの規則に準拠する、クラウド サービスの管理者の役割に対応し、主要理念として管理者の利便性を組み込むのすべての側面を再設計する必要があります。 このモデル必要があります機能を活用して、JIT および JEA、前のステージだけでなくタスク自動化テクノロジに展開されているこれらの目標を達成します。

**2. スマート カードまたはパスポート認証用のすべての管理者**

保証レベルと管理者認証の使いやすさを向上させるのには、Azure Active directory と Windows Server Active Directory (クラウド サービスにフェデレーション アカウントを含む) でホストされているすべての管理者アカウントの強力な認証を必要とする必要があります。

**3。Active Directory 管理者用の管理者フォレスト**

Active Directory 管理者用の最も強力な保護を提供するには、運用 Active Directory にセキュリティの依存関係を持たずはすべての攻撃が、運用環境で最も信頼性の高いシステムから分離された環境を設定します。 ESAE アーキテクチャの詳細については、次を参照してください。[このページ](http://aka.ms/esae)します。

**4. コードの整合性ポリシーの Dc (Server 2016)**

承認されていないプログラム敵対者攻撃操作や不注意な管理上のエラーからドメイン コントローラー上のリスクを制限するためには、カーネル (ドライバー) とユーザー モード (アプリケーション) コンピューター上で実行する権限のある実行可能ファイルのみを許可する Windows Server 2016 コードの整合性を構成します。

**5。仮想 Dc (Server 2016 Hyper-V ファブリック) のシールドされた Vm**

物理的なセキュリティのバーチャル マシンの固有の損失を悪用する攻撃ベクトルから仮想化ドメイン コントローラーを保護するのにには、仮想 Dc から Active Directory の機密情報の盗難を防ぐためにこの新しい Server 2016 Hyper-V 機能を使用します。 このソリューションを使用して、検査、盗難、および記憶域とネットワーク管理者による改ざんから VM のデータを保護できるだけでなく、Hyper-V ホスト管理者の攻撃に対して VM へのアクセスのセキュリティを強化する第 2 世代 Vm を暗号化することができます。

## <a name="am-i-done"></a>ロードマップの完了
このロードマップの完了を実現するは、現在既知およびに利用可能な敵対者今日の攻撃に対して特権アクセスの強力な保護します。 残念ながら、セキュリティの脅威は常に進化し、ため、コストを発生させると、環境を狙う敵対者の成功率を減らすことに重点を置いた継続的なプロセスとしてセキュリティを表示することをお勧めします。

アクセス権限をセキュリティで保護する現代の組織のビジネス資産のセキュリティ保証を確立するための重要な第一歩は、ポリシー、操作、情報セキュリティ、サーバー、アプリケーション、Pc、デバイス、クラウド ファブリック、およびその他のコンポーネントが必要なセキュリティ保証を提供するように要素が含まれる完全なセキュリティ プログラムの一部だけではありません。

完全なセキュリティ ロードマップを構築について詳しくは、利用可能なエンタープライズ アーキテクト ドキュメントの Microsoft Cloud Security の「お客様の責任範囲とロードマップ」セクションを参照してください。[ここ](http://aka.ms/securecustomer)します。

これらのトピックのいずれかを支援する Microsoft サービスとの提携によるについて詳しくは、Microsoft の担当者に問い合わせるかを参照してください[このページ](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)します。

### <a name="related-topics"></a>関連するトピック
[プレミアの特長: Pass the Hash やその他の資格情報の盗難を軽減する方法](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytics](http://aka.ms/ata)

[Credential Guard によるドメインの派生資格情報を保護します。](https://technet.microsoft.com/en-us/library/mt483740%28v=vs.85%29.aspx)

[Device Guard の概要](https://technet.microsoft.com/en-us/library/dn986865(v=vs.85).aspx)

[セキュリティで保護された管理ワークステーションを高価値資産を保護します。](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[Dave Probert による (Channel 9)、Windows 10 の分離ユーザー モード](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[ユーザー モード プロセスと Logan による Windows 10 の機能を分離 Gabriel (Channel 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[プロセスと Dave Probert (Channel 9) による Windows 10 の分離ユーザー モードで機能の詳細](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Windows 10 分離ユーザー モード (Channel 9) を使用して資格情報の盗難の軽減](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Windows Kerberos での KDC の厳密な検証を有効にします。](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Windows Server 2012 の Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)

[Windows Server 2008 R2 で AD DS の認証メカニズム保証 Step-by-Step Guide](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[トラステッド プラットフォーム モジュール](https://docs.microsoft.com/en-us/windows/device-security/tpm/trusted-platform-module-overview)
