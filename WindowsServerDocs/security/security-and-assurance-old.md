---
title: セキュリティおよび保証
description: Windows Server 2016 のセキュリティの概要
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/27/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.openlocfilehash: fed0587b74873005f14a216bac22f952bcc65a4f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447290"
---
# <a name="security-and-assurance-in-windows-server"></a>Windows Server のセキュリティおよび保証 

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<img src="../media/landing-icons/security.png" style='float:left; padding:.5em;' alt="Icon representing a lock"> オペレーティング システムに組み込まれている保護の新しい層を使用して、セキュリティ違反に対する防御を強化することができます。 悪意のある攻撃をブロックし、仮想マシン、アプリケーション、およびデータのセキュリティ強化を支援します。


### <a name="windows-server-security-blog-posthttpsblogstechnetmicrosoftcomwindowsserver20160425ten-reasons-youll-love-windows-server-2016-8-security"></a>[Windows Server セキュリティ ブログの投稿](https://blogs.technet.microsoft.com/windowsserver/2016/04/25/ten-reasons-youll-love-windows-server-2016-8-security/)
Windows Server セキュリティ チームによるこのブログ記事では、ホスティングおよびハイブリッド クラウド環境のセキュリティを強化する数多くの Windows Servers の改良点が明らかにされています。

### <a name="datacenter-and-private-cloud-security-bloghttpsblogstechnetmicrosoftcomdatacentersecurity"></a>[データ センターおよびプライベート クラウドのセキュリティ ブログ](https://blogs.technet.microsoft.com/datacentersecurity/)
マイクロソフトのデータ センターおよびプライベート クラウドのセキュリティ チームによる技術コンテンツの中心的なブログ サイトです。                                    

### <a name="addressing-emerging-threats-and-landscape-shiftshttpswwwyoutubecomwatchvb5jmyxywx1kfeatureyoutube"></a>[シフト新種の脅威とランドス ケープをアドレス指定](https://www.youtube.com/watch?v=B5JMYxYWx1k&feature=youtu.be)
この 6 分間のビデオでは、Anders Vinberg 氏が、Microsoft のセキュリティおよび保証戦略の概要、セキュリティに関係する業界の動向と状況の変化について説明しています。 さらに、基礎となるファブリックからのワークロードを保護し、権限を持つアカウントからの直接的な攻撃から保護するためのマイクロソフトの重要なイニシアティブについて説明しています。 最後に、セキュリティ侵害について、新しい検知および法科学機能が脅威の特定によりいっそう役立つことを説明しています。

### <a name="protecting-your-datacenter-and-cloud-from-emerging-threats-blog-posthttpblogstechnetcombwindowsserverarchive20151118protecting-your-datacenter-and-cloud-november-updateaspx"></a>[Emerging Threats ブログの投稿からのデータ センターとクラウドを保護します。](http://blogs.technet.com/b/windowsserver/archive/2015/11/18/protecting-your-datacenter-and-cloud-november-update.aspx)
このブログ記事では、Microsoft のテクノロジを使用して、データ センターとクラウドへの投資を新たな脅威からどのように保護できるかについて説明しています。                   

### <a name="security-and-assurance-overview-session-at-ignitehttpchannel9msdncomeventsignite2015brk2482"></a>[Ignite でのセキュリティおよび保証の概要セッション](http://channel9.msdn.com/events/ignite/2015/brk2482)
この Ignite セッションでは、絶え間ない脅威、内部関係者による違反、組織的サイバー犯罪、Microsoft Cloud プラットフォームのセキュリティ (オンプレミスおよび Azure による接続済みサービス) について説明しています。 これには、ワークロード、大規模なエンタープライズ テナント、およびサービス プロバイダーを保護するためのシナリオが含まれます。                                                                   

## <a name="secure-virtualization-with-shielded-vms"></a>シールドされた VM による安全な仮想化

### <a name="shielded-vm-in-channel-9httpchannel9msdncomshowsmechanicsintroduction-to-shielded-virtual-machines-in-windows-server-2016"></a>[Channel 9 でシールドされた VM](http://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
シールドされた VM テクノロジとその利点の紹介です。                           

### <a name="shielded-vm-demohttpswwwyoutubecomwatchvxip5qtk-7d8"></a>[シールドされた VM のデモ](https://www.youtube.com/watch?v=xip5Qtk-7d8)
この 4 分間のビデオでは、シールドされた VM の価値と、シールドされた VM とシールドされていない VM の違いが説明されています。                                   

### <a name="shielded-virtual-machines-in-windows-server-video-walkthroughhttpmicrosoft-cloudcloudguidescomguidesshielded-virtual-machines-in-windows-serverhtm"></a>[Windows Server のビデオ チュートリアルでシールドされた仮想マシン](http://microsoft-cloud.cloudguides.com/Guides/Shielded Virtual Machines in Windows Server.htm)
このビデオ チュートリアルでは、機密データを Hyper-V ホスト管理者による不正アクセスから守るために、ホスト ガーディアン サービスを使用して、シールドされた仮想マシンを有効にする方法が説明されています。

### <a name="harden-the-fabric-protecting-tenant-secrets-in-hyper-v-ignite-videohttpchannel9msdncomeventsignite2015brk3457"></a>[ファブリックを強化します。HYPER-V でテナントのシークレットを保護する (Ignite ビデオ)](http://channel9.msdn.com/events/ignite/2015/brk3457)

この Ignite プレゼンテーションでは、Hyper-V および Virtual Machine Manager の機能強化と、シールドされた VM を有効にするための新しいホスト ガーディアン サーバーの役割が説明されています。                

### <a name="guarded-fabric-deployment-guidehttpsdocsmicrosoftcomwindows-servervirtualizationguarded-fabric-shielded-vmguarded-fabric-deploying-hgs-overview"></a>[保護されたファブリックの展開ガイド](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-deploying-hgs-overview)
このガイドには、保護されたファブリック ホストとシールドされた VM のための Windows Server と System Center Virtual Machine Manager のインストールおよび検証に関する情報が記載されています。

### <a name="shielded-vm-and-guarded-fabric-in-branch-officeshttpsdocsmicrosoftcomwindows-servervirtualizationguarded-fabric-shielded-vmguarded-fabric-manage-branch-office"></a>[シールドされた VM とブランチ オフィスで保護されたファブリック](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office)
このガイドでは、ブランチ オフィス内でシールドされた仮想マシンを実行するためのベスト プラクティス、および Hyper-V ホストで HGS への接続が限定される時間がある可能性のあるその他のリモート シナリオについて説明します。

### <a name="shielded-vm-and-guarded-fabric-troubleshooting-guidehttpsdocsmicrosoftcomwindows-servervirtualizationguarded-fabric-shielded-vmguarded-fabric-troubleshoot-overview"></a>[シールドされた VM と保護されたファブリックのトラブルシューティング ガイド](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-overview)
このガイドには、シールドされた VM の環境内で発生する可能性がある問題の解決方法についての情報が記載されています。

### <a name="shielded-vm-articlehttpwindowsitprocomhyper-vsuper-secure-hyper-v-environments-shielded-vms-2016"></a>[シールドされた VM の記事](http://windowsitpro.com/hyper-v/super-secure-hyper-v-environments-shielded-vms-2016)
このホワイト ペーパーには、シールドされた VM によって全体的なセキュリティが改ざん防止のためにどのように強化されるのかについての概要が説明されています。                                         

## <a name="privileged-access-management"></a>特権アクセスの管理
### <a name="securing-privileged-accesshttpstechnetmicrosoftcomwindows-server-docssecuritysecuring-privileged-accesssecuring-privileged-access"></a>[特権アクセスの保護](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access)
特権アクセスをセキュリティで保護する方法についてのロードマップを示します。 このロードマップは、サーバー セキュリティ チーム、Microsoft IT、Azure チーム、および Microsoft Consulting Services の知見を結集して作成されています。                           

### <a name="just-in-time-administration-with-microsoft-identity-managerhttpstechnetmicrosoftcomlibrarymt150258aspx"></a>[ジャスト イン タイム管理を Microsoft Identity Manager](https://technet.microsoft.com/library/mt150258.aspx)
この記事では、Just in Time (JIT) 特権アクセス管理のサポートなど、Microsoft Identity Manager の機能について説明されています。                                                                    

### <a name="protecting-windows-and-microsoft-azure-active-directory-with-privileged-access-managementhttpchannel9msdncomeventsignite2015brk3873"></a>[Privileged Access Management での Windows と Microsoft Azure Active Directory を保護します。](http://channel9.msdn.com/events/ignite/2015/brk3873)
この Ignite プレゼンテーションでは、Windows Server、PowerShell、Active Directory、Identity Manager、および Azure Active Directory で認証を強化して管理者アクセスのリスクに対処し、Just in Time と Just Enough Administration (JEA) を使用してアクセスを管理するための Microsoft による戦略と投資が取り上げられています。

### <a name="just-enough-administration-articlehttpakamsjea"></a>[Just Enough Administration に関する記事](http://aka.ms/JEA)
このドキュメントには、Just Enough Administration のビジョンと技術詳細が記載されています。Just Enough Administration は、オペレーターによるアクセスを特定のタスクを実行するのに必要なものだけに制限し、組織のリスクを軽減するように設計された PowerShell のツールキットです。

### <a name="just-enough-administration-demo-videohttpswwwyoutubecomwatchvxnbrbky9p20"></a>[Enough Administration のデモ ビデオだけです。](https://www.youtube.com/watch?v=xnBrbkY9P20)
Just Enough Administration のデモ チュートリアルです。                                                                                                                  
## <a name="credential-protection"></a>資格情報の保護

### <a name="protect-derived-domain-credentials-with-credential-guardhttpsdocsmicrosoftcomwindowssecurityidentity-protectioncredential-guardcredential-guard"></a>[Credential Guard によるドメインの派生資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard)
Credential Guard は、特権を持つシステム ソフトウェアだけがシークレットにアクセスできるように、仮想化ベースのセキュリティを使用してシークレットを分離します。 これらのシークレットへの未承認のアクセスは、Pass-the-Hash や Pass-the-Ticket など、資格情報の盗難攻撃につながる可能性があります。 Credential Guard は、NTLM パスワード ハッシュや Kerberos チケット保証チケットを保護することでこれらの攻撃を防ぎます。

### <a name="protect-remote-desktop-credentials-with-remote-credential-guardhttpsdocsmicrosoftcomwindowssecurityidentity-protectionremote-credential-guard"></a>[Remote Credential Guard によるリモート デスクトップ資格情報の保護](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard)
Remote Credential Guard は、接続を要求しているデバイスに Kerberos 要求をリダイレクトすることにより、リモート デスクトップ接続での資格情報を保護するのに役立ちます。 リモート デスクトップ セッションでシングル サインオンのエクスペリエンスも提供します。                                                                                                        |
### <a name="credential-guard-demo-videohttpswwwyoutubecomwatchveupkogsl7yk"></a>[Credential Guard のデモ ビデオ](https://www.youtube.com/watch?v=eUpKOGSl7yk)
この 5 分のビデオでは、Credential Guard と Remote Credential Guard のデモを行います。         

## <a name="hardening-the-os-and-applications"></a>OS とアプリケーションのセキュリティ強化
### <a name="windows-defender-application-control-wdac-deployment-guidehttpsdocsmicrosoftcomwindowssecuritythreat-protectionwindows-defender-application-controlwindows-defender-application-control"></a>[Windows Defender アプリケーション制御 (WDAC) 展開ガイド](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control)
WDAC は、企業が環境内で実行するアプリケーションを制御し、Windows 10 を実行する以外に特別なハードウェアまたはソフトウェア要件を必要としない構成可能なコードの整合性 (CI) ポリシーです。

### <a name="device-guard-demo-videohttpswwwyoutubecomwatchvf-ptkesjkhi"></a>[デバイス Guard のデモ ビデオ](https://www.youtube.com/watch?v=F-pTkesjkhI)
Device Guard は、WDAC とハイパーバイザーで保護されているコード整合性 (HVCI) を組み合わせたものです。 この 7 分のビデオでは、Device Guard と Windows Server でのその使用方法を示します。

### <a name="transport-layer-security-registry-settingshttpsdocsmicrosoftcomwindows-serversecuritytlstls-registry-settings"></a>[トランスポート層セキュリティ レジストリ設定](https://docs.microsoft.com/windows-server/security/tls/tls-registry-settings)
トランスポート層セキュリティ (TLS) プロトコルと Secure Sockets Layer (SSL) プロトコルの Windows 実装に関するサポートされたレジストリ設定の情報です。

### <a name="control-flow-guardhttpsdocsmicrosoftcomwindowsdesktopsecbpcontrol-flow-guard"></a>[制御フロー ガード](https://docs.microsoft.com/windows/desktop/SecBP/control-flow-guard)
制御フロー ガードは、一部のクラスのメモリ破損攻撃に対する組み込みの保護を提供します。

### <a name="windows-defenderhttpstechnetmicrosoftcomwindows-server-docssecuritywindows-defenderwindows-defender-overview-windows-server"></a>[Windows Defender](https://technet.microsoft.com/windows-server-docs/security/windows-defender/windows-defender-overview-windows-server)
Windows Defender は、アクティブな検出機能を提供して既知のマルウェアをブロックします。 Windows Defender は既定では有効になっており、Windows Server でさまざまなサーバーの役割をサポートするために最適化されています。

## <a name="detecting-and-responding-to-threats"></a>脅威の検出と対応
### <a name="security-threat-analysis-using-microsoft-operations-management-suitehttpschannel9msdncomeventsignite2015brk3464"></a>[Microsoft Operations Management Suite を使用してセキュリティの脅威の分析](https://channel9.msdn.com/events/ignite/2015/brk3464)
この Ignite プレゼンテーションでは、Operational Insights を使用して、どのようにセキュリティ上の脅威の分析を実行できるかについて説明されています。

### <a name="microsoft-operations-management-suite-omshttpswwwmicrosoftcomen-usserver-cloudoperations-management-suiteoverviewaspx"></a>[Microsoft Operations Management Suite (OMS)](https://www.microsoft.com/en-us/server-cloud/operations-management-suite/overview.aspx)
Microsoft Operations Management Suite (OMS) セキュリティおよび監査ソリューションは、オンプレミス環境とクラウド環境のセキュリティ ログとファイアウォール イベントを処理して、悪意のある動作を分析および検出します。

### <a name="oms-and-windows-serverhttpswwwyoutubecomwatchvsadw1dry2k"></a>[OMS と Windows Server](https://www.youtube.com/watch?v=_SaDw1dRy2k)
この 3 分間のビデオでは、Windows Server によってブロックされる潜在的な悪意のある動作を検出するのに役立つ OMS を紹介しています。  

### <a name="microsoft-advanced-threat-analyticshttpblogstechnetcombadarchive20150722microsoft-advanced-threat-analytics-coming-next-monthaspx"></a>[Microsoft Advanced Threat Analytics](http://blogs.technet.com/b/ad/archive/2015/07/22/microsoft-advanced-threat-analytics-coming-next-month.aspx)
このブログ記事では、Active Directory のネットワーク トラフィックと SIEM データに基づいて潜在的な脅威を検出し、アラートを生成するオンプレミス製品である Microsoft Advanced Threat Analytics について説明されています。

### <a name="microsoft-advanced-threat-analyticshttpswwwyoutubecomwatchv0na9fetrzfwlistpl8nfc9hageb5izgm8hvmrozethrpbdksw"></a>[Microsoft Advanced Threat Analytics](https://www.youtube.com/watch?v=0nA9FeTRZFw&list=PL8nfc9haGeb5IZGM8HvmRozetHRpBDKSw)
この 3 分間のビデオでは、Microsoft が Windows Server に脅威分析機能をどのように追加しているのかについての概要が示されています。                                                                                 |

## <a name="network-security"></a>ネットワーク セキュリティ

### <a name="datacenter-firewall-overviewhttpstechnetmicrosoftcomlibrarydn920240aspx"></a>[データ センターのファイアウォールの概要](https://technet.microsoft.com/library/dn920240.aspx)
この概要では、ネットワーク層で 5 組 (プロトコル、発信元と宛先のポート番号、送信元と送信先の IP アドレス) を使用して動作するステートフルなマルチテナント ファイアウォールである Datacenter Firewall について説明されています。

### <a name="whats-new-in-dns-in-windows-serverhttpstechnetmicrosoftcomwindows-server-docsnetworkingdnswhat-s-new-in-dns-server"></a>[新機能 Windows server DNS の新機能](https://technet.microsoft.com/windows-server-docs/networking/dns/what-s-new-in-dns-server)
この概要トピックには、DNS の新機能についての簡単な説明、および詳細情報へのリンクが記載されています。                                                                           

## <a name="mapping-security-features-to-compliance-regulations"></a>コンプライアンスに関する規制へのセキュリティ機能のマッピング

コンプライアンスは、セキュリティ機能の重要な側面です。 コンプライアンスを実現する方法に関するアドバイスや信頼できるコンプライアンス アドバイザーによってのコンプライアンスは専門家にお任せしますが、Windows Server を評価するときに使用できる初期のマッピングを提供する必要があります。

-   [HYPER-V のシールドされた Vm のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/6/D/0/6D06E149-B4C1-4EED-ACD5-DF6066E93CC0/Coalfire_Branded_Hyper_V_Shielded_VMs_Whitepaper_EN_US.pdf)

-   [JEA と JIT のコンプライアンスのマッピング ホワイト ペーパー](https://download.microsoft.com/download/2/7/A/27A2B5BB-6B52-4482-87C1-DA9D6B6D8C8D/Coalfire_Branded_Privileged_Identity_Manager_Whitepaper_EN_US.pdf)

-   [デバイス ガード コンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/6/9/D/69D9E610-D23C-4F7E-A8CC-D65B87CEB4F8/Coalfire_Branded_Device_Guard_Whitepaper_EN_US.pdf)

-   [Credential Guard のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/8/1/2/812009C9-E4B8-4D4B-AADD-FDC373D0A076/Coalfire_Branded_Credential_Guard_Whitepaper_EN_US.pdf)

-   [Windows Defender のコンプライアンスのマッピングに関するホワイト ペーパー](https://download.microsoft.com/download/C/7/7/C778B7BB-0783-42D7-93A9-B86DFB5A7BAD/Coalfire_Branded_Windows_Defender_Whitepaper_EN_US.pdf)
