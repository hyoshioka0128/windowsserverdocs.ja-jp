---
title: セキュリティおよび保証
description: Windows Server 2016 のセキュリティの概要
ms.topic: article
ms.date: 07/27/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.openlocfilehash: f973d83c53fb4667163d950a169611721f53f78e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939479"
---
# <a name="security-and-assurance-in-windows-server"></a>Windows Server のセキュリティおよび保証

>適用先:Windows Server (半期チャネル)、Windows Server 2016

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/security.png" style='float:left; padding:.5em;' alt="Icon representing a lock"> オペレーティング システムに組み込まれている保護の新しい層を使用して、セキュリティ違反に対する防御を強化することができます。 悪意のある攻撃をブロックし、仮想マシン、アプリケーション、およびデータのセキュリティを強化するのを支援します。


### <a name="windows-server-security-blog-post"></a>[Windows Server のセキュリティについてのブログ記事](https://blogs.technet.microsoft.com/windowsserver/2016/04/25/ten-reasons-youll-love-windows-server-2016-8-security/)
Windows Server セキュリティ チームによるこのブログ記事では、ホスティングおよびハイブリッド クラウド環境のセキュリティを強化する数多くの Windows Servers の改良点が明らかにされています。

### <a name="datacenter-and-private-cloud-security-blog"></a>[Datacenter and Private Cloud Security Blog (データ センターおよびプライベート クラウドのセキュリティについてのブログ)](https://blogs.technet.microsoft.com/datacentersecurity/)
これは、Microsoft のデータ センターおよびプライベート クラウドのセキュリティ チームによる、技術コンテンツに関する中心的なブログ サイトです。

### <a name="addressing-emerging-threats-and-landscape-shifts"></a>[Addressing emerging threats and landscape shifts (新たな脅威とランドスケープの変化への対応)](https://www.youtube.com/watch?v=B5JMYxYWx1k&feature=youtu.be)
この 6 分間のビデオでは、Anders Vinberg 氏が、Microsoft のセキュリティおよび保証戦略の概要、セキュリティに関係する業界の動向と状況の変化について説明しています。 さらに、基礎となるファブリックからのワークロードを保護し、権限を持つアカウントからの直接的な攻撃から保護するための Microsoft の重要なイニシアティブについて説明しています。 最後に、セキュリティ侵害について、新しい検知および法科学機能が脅威の特定によりいっそう役立つことを説明しています。

### <a name="protecting-your-datacenter-and-cloud-from-emerging-threats-blog-post"></a>[Protecting Your Datacenter and Cloud from Emerging Threats (新たな脅威からのデータ センターとクラウドの保護) についてのブログ投稿](https://blogs.technet.com/b/windowsserver/archive/2015/11/18/protecting-your-datacenter-and-cloud-november-update.aspx)
このブログ投稿では、Microsoft のテクノロジを使用して、データ センターとクラウドへの投資を新たな脅威からどのように保護できるかについて説明されています。

### <a name="security-and-assurance-overview-session-at-ignite"></a>[Ignite でのセキュリティおよび保証の概要セッション](https://channel9.msdn.com/events/ignite/2015/brk2482)
この Ignite セッションでは、絶え間ない脅威、内部関係者による違反、組織によるサイバー犯罪、Microsoft クラウド プラットフォームのセキュリティ (オンプレミスおよび Azure による接続済みサービス) が説明されています。 これには、ワークロード、大規模なエンタープライズ テナント、およびサービス プロバイダーを保護するためのシナリオが含まれます。

## <a name="secure-virtualization-with-shielded-vms"></a>シールドされた VM による安全な仮想化

### <a name="shielded-vm-in-channel-9"></a>[シールドされた VM に関する Channel 9 のビデオ](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
シールドされた VM テクノロジとその利点の紹介です。

### <a name="shielded-vm-demo"></a>[シールドされた VM のデモ](https://www.youtube.com/watch?v=xip5Qtk-7d8)
この 4 分間のビデオでは、シールドされた VM の価値と、シールドされた VM とシールドされていない VM の違いが説明されています。

### <a name="shielded-virtual-machines-in-windows-server-video-walkthrough"></a>[Windows Server でのシールドされた仮想マシンについてのビデオ チュートリアル](http://microsoft-cloud.cloudguides.com/Guides/Shielded Virtual Machines in Windows Server.htm)
このビデオ チュートリアルでは、機密データを Hyper-V ホスト管理者による不正アクセスから守るために、ホスト ガーディアン サービスを使用して、シールドされた仮想マシンを有効にする方法が説明されています。

### <a name="harden-the-fabric-protecting-tenant-secrets-in-hyper-v-ignite-video"></a>[ファブリックの強化: Hyper-V のテナントの機密情報を保護する (Ignite ビデオ)](https://channel9.msdn.com/events/ignite/2015/brk3457)

この Ignite プレゼンテーションでは、Hyper-V および Virtual Machine Manager の機能強化と、シールドされた VM を有効にするための新しいホスト ガーディアン サーバーの役割が説明されています。

### <a name="guarded-fabric-deployment-guide"></a>[保護されたファブリックの展開ガイド](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)
このガイドには、保護されたファブリック ホストとシールドされた VM のための Windows Server と System Center Virtual Machine Manager のインストールおよび検証に関する情報が記載されています。

### <a name="shielded-vm-and-guarded-fabric-in-branch-offices"></a>[ブランチ オフィス内のシールドされた VM および保護されたファブリック](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office)
このガイドでは、ブランチ オフィス内でシールドされた仮想マシンを実行するためのベスト プラクティス、および Hyper-V ホストで HGS への接続が限定される時間がある可能性のあるその他のリモート シナリオについて説明します。

### <a name="shielded-vm-and-guarded-fabric-troubleshooting-guide"></a>[シールドされた VM と保護されたファブリックのトラブルシューティング ガイド](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-overview)
このガイドには、シールドされた VM の環境内で発生する可能性がある問題の解決方法についての情報が記載されています。

### <a name="shielded-vm-article"></a>[シールドされた VM についての記事](http://windowsitpro.com/hyper-v/super-secure-hyper-v-environments-shielded-vms-2016)
このホワイト ペーパーには、シールドされた VM によって全体的なセキュリティが改ざん防止のためにどのように強化されるのかについての概要が説明されています。

## <a name="privileged-access-management"></a>特権アクセスの管理
### <a name="securing-privileged-access"></a>[特権アクセスの保護](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access)
特権アクセスをセキュリティで保護する方法についてのロードマップ このロードマップは、サーバー セキュリティ チーム、Microsoft IT、Azure チーム、および Microsoft Consulting Services が有する知見を結集して作成されています。

### <a name="just-in-time-administration-with-microsoft-identity-manager"></a>[Microsoft Identity Manager による Just in Time 管理](https://technet.microsoft.com/library/mt150258.aspx)
この記事では、Just-In-Time (JIT) 特権アクセス管理のサポートなど、Microsoft Identity Manager に含まれている機能が説明されています。

### <a name="protecting-windows-and-microsoft-azure-active-directory-with-privileged-access-management"></a>[特権アクセス管理による Windows と Microsoft Azure Active Directory の保護](https://channel9.msdn.com/events/ignite/2015/brk3873)
この Ignite プレゼンテーションでは、Windows Server、PowerShell、Active Directory、Identity Manager、および Azure Active Directory で認証を強化して管理者アクセスのリスクに対処し、Just in Time と Just Enough Administration (JEA) を使用してアクセスを管理するための Microsoft による戦略と投資が取り上げられています。

### <a name="just-enough-administration-article"></a>[Just Enough Administration に関する記事](https://aka.ms/JEA)
このドキュメントには、Just Enough Administration (JEA) のビジョンと技術詳細が記載されています。JEA は、オペレーターによるアクセスを特定のタスクを実行するのに必要なものだけに制限し、組織のリスクを軽減するように設計された PowerShell のツールキットです。

### <a name="just-enough-administration-demo-video"></a>[Just Enough Administration のデモ ビデオ](https://www.youtube.com/watch?v=xnBrbkY9P20)
Just Enough Administration のデモ チュートリアルです。
## <a name="credential-protection"></a>資格情報の保護

### <a name="protect-derived-domain-credentials-with-credential-guard"></a>[Credential Guard によるドメインの派生資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)
Credential Guard は、特権を持つシステム ソフトウェアだけがシークレットにアクセスできるように、仮想化ベースのセキュリティを使用してシークレットを分離します。 これらのシークレットへの不正アクセスは、Pass-the-Hash や Pass-The-Ticket などの資格情報の盗難攻撃につながる可能性があります。 Credential Guard は、NTLM パスワード ハッシュと Kerberos の Ticket Granting Ticket を保護することで、これらの攻撃を防ぎます。

### <a name="protect-remote-desktop-credentials-with-remote-credential-guard"></a>[Remote Credential Guard によるリモート デスクトップ資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard)
Remote Credential Guard は、接続を要求しているデバイスに Kerberos 要求をリダイレクトすることにより、リモート デスクトップ接続での資格情報を保護するのに役立ちます。 リモート デスクトップ セッションでシングル サインオンのエクスペリエンスも提供します。                                                                                                        |
### <a name="credential-guard-demo-video"></a>[Credential Guard のデモ ビデオ](https://www.youtube.com/watch?v=eUpKOGSl7yk)
この 5 分間のビデオでは、Credential Guard と Remote Credential Guard のデモを行っています。

## <a name="hardening-the-os-and-applications"></a>OS とアプリケーションのセキュリティ強化
### <a name="windows-defender-application-control-wdac-deployment-guide"></a>[Windows Defender アプリケーション制御 (WDAC) 展開ガイド](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
WDAC は、企業が環境内で実行するアプリケーションを制御し、Windows 10 を実行する以外に特別なハードウェアまたはソフトウェア要件を必要としない構成可能なコードの整合性 (CI) ポリシーです。

### <a name="device-guard-demo-video"></a>[Device Guard のデモ ビデオ](https://www.youtube.com/watch?v=F-pTkesjkhI)
Device Guard は、WDAC とハイパーバイザーで保護されているコード整合性 (HVCI) を組み合わせたものです。 この 7 分間のビデオでは、Device Guard と、Windows Server 上での使い方を紹介します。

### <a name="transport-layer-security-registry-settings"></a>[トランスポート層セキュリティ レジストリ設定](https://docs.microsoft.com/windows-server/security/tls/tls-registry-settings)
トランスポート層セキュリティ (TLS) プロトコルと Secure Sockets Layer (SSL) プロトコルの Windows 実装に関するサポートされたレジストリ設定の情報です。

### <a name="control-flow-guard"></a>[制御フロー ガード](https://docs.microsoft.com/windows/desktop/SecBP/control-flow-guard)
制御フロー ガードは、一部のクラスのメモリ破損攻撃に対する組み込みの保護を提供します。

### <a name="windows-defender"></a>[Windows Defender](https://technet.microsoft.com/windows-server-docs/security/windows-defender/windows-defender-overview-windows-server)
Windows Defender は、アクティブな検出機能を提供して既知のマルウェアをブロックします。 Windows Server では、Windows Defender が既定でオンになっており、さまざまなサーバーの役割をサポートするために最適化されています。

## <a name="detecting-and-responding-to-threats"></a>脅威の検出と対応
### <a name="security-threat-analysis-using-microsoft-operations-management-suite"></a>[Microsoft Operations Management Suite を使用したセキュリティ上の脅威についての分析](https://channel9.msdn.com/events/ignite/2015/brk3464)
この Ignite プレゼンテーションでは、Operational Insights を使用して、どのようにセキュリティ上の脅威の分析を実行できるかについて説明されています。

### <a name="microsoft-operations-management-suite-oms"></a>[Microsoft Operations Management Suite (OMS)](https://www.microsoft.com/server-cloud/operations-management-suite/overview.aspx)
Microsoft Operations Management Suite (OMS) セキュリティおよび監査ソリューションは、オンプレミス環境とクラウド環境のセキュリティ ログとファイアウォール イベントを処理して、悪意のある動作を分析および検出します。

### <a name="oms-and-windows-server"></a>[OMS と Windows Server](https://www.youtube.com/watch?v=_SaDw1dRy2k)
この 3 分間のビデオでは、Windows Server によってブロックされる潜在的な悪意のある動作を検出するのに役立つ OMS を紹介しています。

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://blogs.technet.com/b/ad/archive/2015/07/22/microsoft-advanced-threat-analytics-coming-next-month.aspx)
このブログ投稿では、Active Directory のネットワーク トラフィックと SIEM データに基づいて潜在的な脅威を検出し、アラートを生成するオンプレミス製品である Microsoft Advanced Threat Analytics について説明されています。

### <a name="microsoft-advanced-threat-analytics"></a>[Microsoft Advanced Threat Analytics](https://www.youtube.com/watch?v=0nA9FeTRZFw&list=PL8nfc9haGeb5IZGM8HvmRozetHRpBDKSw)
この 3 分間のビデオでは、Microsoft が Windows Server に脅威分析機能をどのように追加しているのかについての概要が示されています。                                                                                 |

## <a name="network-security"></a>ネットワーク セキュリティ

### <a name="datacenter-firewall-overview"></a>[Datacenter Firewall の概要](https://technet.microsoft.com/library/dn920240.aspx)
この概要では、ネットワーク層で 5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス) を使用して動作するステートフルなマルチテナント ファイアウォールである Datacenter Firewall について説明されています。

### <a name="whats-new-in-dns-in-windows-server"></a>[Windows Server での DNS の新機能](https://technet.microsoft.com/windows-server-docs/networking/dns/what-s-new-in-dns-server)
この概要トピックには、DNS の新機能についての簡単な説明、および詳細情報へのリンクが記載されています。

## <a name="mapping-security-features-to-compliance-regulations"></a>コンプライアンスに関する規制へのセキュリティ機能のマッピング

コンプライアンスは、セキュリティ機能の重要な側面です。 コンプライアンスを実現する方法に関するアドバイスや信頼できるコンプライアンス アドバイザーによってのコンプライアンスは専門家にお任せしますが、Windows Server を評価するときに使用できる初期のマッピングを提供する必要があります。

-   [Hyper-V のシールドされた VM のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/6/D/0/6D06E149-B4C1-4EED-ACD5-DF6066E93CC0/Coalfire_Branded_Hyper_V_Shielded_VMs_Whitepaper_EN_US.pdf)

-   [JEA と JIT のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/2/7/A/27A2B5BB-6B52-4482-87C1-DA9D6B6D8C8D/Coalfire_Branded_Privileged_Identity_Manager_Whitepaper_EN_US.pdf)

-   [Device Guard のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/6/9/D/69D9E610-D23C-4F7E-A8CC-D65B87CEB4F8/Coalfire_Branded_Device_Guard_Whitepaper_EN_US.pdf)

-   [Credential Guard のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/8/1/2/812009C9-E4B8-4D4B-AADD-FDC373D0A076/Coalfire_Branded_Credential_Guard_Whitepaper_EN_US.pdf)

-   [Windows Defender のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/C/7/7/C778B7BB-0783-42D7-93A9-B86DFB5A7BAD/Coalfire_Branded_Windows_Defender_Whitepaper_EN_US.pdf)
