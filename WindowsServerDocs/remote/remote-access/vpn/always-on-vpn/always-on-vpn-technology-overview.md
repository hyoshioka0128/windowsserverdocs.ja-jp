---
title: Always On VPN テクノロジの概要
description: 'このページで詳細なドキュメントへのリンクを Always On VPN テクノロジの概要。 '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: fd3f7c6ca8555e270aabf04bbee6800ed284080c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821263"
---
# <a name="always-on-vpn-technology-overview"></a>Always On VPN テクノロジの概要
>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

&#171;  [**先の：** Always On VPN の機能強化について説明します](always-on-vpn-enhancements.md)<br>
&#187;  [**次に：** Always On VPN の高度な機能について説明します](deploy/always-on-vpn-adv-options.md)

この展開のする必要があります、Windows Server 2016 を実行している新しいリモート アクセス サーバーをインストールするだけでなく、既存のインフラストラクチャのデプロイの一部を変更します。

次の図は、Always On VPN を展開するために必要なインフラストラクチャを示します。

![Always On VPN インフラストラクチャ](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

この図に示すように、接続プロセスは、次の手順から成ります。

1. Windows 10 の VPN クライアントを公開 DNS サーバーを使用して VPN ゲートウェイの IP アドレスの名前解決のクエリを実行します。

2. DNS によって返された IP アドレスを使用して、VPN クライアントは、VPN ゲートウェイに接続要求を送信します。

3. VPN ゲートウェイが、リモート認証ダイヤルイン ユーザー サービスとしても構成されている\(RADIUS\)クライアントは、VPN RADIUS クライアントは、接続要求の処理の組織/企業の NPS サーバーに接続要求を送信します。

4. NPS サーバーでは、承認、および認証の実行など、接続要求を処理し、許可するか、接続要求を拒否するかどうかを決定します。

5. NPS サーバーは、VPN ゲートウェイへのアクセス許可や、アクセス拒否応答を転送します。

6. 接続を開始または終了される VPN サーバーを NPS サーバーから受信した応答に基づいて。

上記の図に示した各インフラストラクチャ コンポーネントの詳細については、次のセクションを参照してください。

>[!NOTE]
>既にある場合、ネットワークに展開されているこれらのテクノロジの一部では、この展開の目的のテクノロジの追加の構成を実行するこの展開ガイドで指示を使用できます。

## <a name="domain-name-system-dns"></a>ドメイン ネーム システム (DNS)

内部および外部の両方のドメイン ネーム システム (DNS) ゾーンが必要な場合は、内部のゾーン (たとえば、corp.contoso.com と contoso.com など) は、外部のゾーンの委任されたサブドメインであることを想定しています。

詳細については[ドメイン ネーム システム (DNS)](../../../../networking/dns/dns-top.md)または[コア ネットワーク ガイド](../../../../networking/core-network-guide/core-network-guide.md)します。




>[!NOTE] 
>その他の DNS スプリット ブレインの DNS (を使用して、同じドメイン名内部および外部で個別の DNS ゾーンで) などのデザインまたは関係のない内部と外部ドメイン (contoso.local と contoso.com など) も考えられます。 スプリット ブレイン DNS 展開の詳細については、次を参照してください。[分割/ブレイン DNS 展開の DNS ポリシーを使用する](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)します。

## <a name="firewalls"></a>ファイアウォール

ファイアウォールが正常に機能する VPN、RADIUS の両方の通信に必要なトラフィックを許可することを確認します。

詳細については、次を参照してください。 [RADIUS トラフィックのファイアウォールの構成](../../../../networking/technologies/nps/nps-firewalls-configure.md)します。

## <a name="remote-access-as-a-ras-gateway-vpn-server"></a>RAS ゲートウェイの VPN サーバーとしてのリモート アクセス

ルーターとリモート アクセス サーバーの両方を実行する Windows Server 2016 でリモート アクセス サーバーの役割が設計されていますそのため、さまざまな機能をサポートします。 このデプロイ ガイダンスについては、これらの機能のごく一部のみを必要とします。 IKEv2 VPN 接続と LAN ルーティングをサポートします。

IKEv2 は、VPN トンネリング プロトコルのコメント 7296 Internet Engineering Task Force の要求で説明します。 IKEv2 の主な利点は、基になるネットワーク接続の中断が許容できることです。 たとえば、接続が一時的に失われた場合、または、ユーザーでは、1 つのネットワークからクライアント コンピューターを移動する場合は、IKEv2 によって自動的に復元 VPN 接続のネットワーク接続が再度確立される: ユーザーの介入なしですべてです。

RAS ゲートウェイを使用して、組織のネットワークおよびリソースへのリモート アクセスでエンドユーザーに提供する VPN 接続を展開できます。 リモート コンピューターがインターネットに接続するたびに、クライアントと、組織のネットワークの間で永続的な接続を維持する Always On VPN を展開します。 RAS ゲートウェイを使用しても、プライマリ オフィスとブランチ オフィス間など、異なる場所にある 2 つのサーバー間のサイト対サイト VPN 接続を作成およびネットワーク アドレス変換を使用することができます\(NAT\)ように内部のユーザー、ネットワークは、インターネットなどの外部リソースにアクセスできます。 また、RAS ゲートウェイは、リモート オフィスの場所では、BGP をサポートするエッジ ゲートウェイもがある場合は、動的ルーティング サービスを提供するボーダー ゲートウェイ プロトコル (BGP) をサポートします。

Windows PowerShell コマンドとリモート アクセス Microsoft 管理コンソール (MMC) を使用して、リモート アクセス サービス (RAS) ゲートウェイを管理できます。



## <a name="network-policy-server-nps"></a>ネットワーク ポリシー サーバー (NPS)

NPS を作成し、接続要求の認証と承認のため、組織全体のネットワーク アクセス ポリシーを適用することができます。 NPS をリモート認証ダイヤルイン ユーザー サービス (RADIUS) サーバーとして使用する場合は、NPS の RADIUS クライアントとして、VPN サーバーなどのネットワーク アクセス サーバーを構成します。

また、NPS が接続要求を承認するために使用するネットワーク ポリシーを構成して、NPS がアカウンティング情報をローカル ハード ディスク上のログ ファイルまたは Microsoft SQL Server データベースに記録するように RADIUS アカウンティングを構成できます。

詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](../../../../networking/technologies/nps/nps-top.md)します。


## <a name="active-directory-certificate-services"></a>Active Directory 証明書サービス

証明機関 (CA) サーバーでは、Active Directory Certificate Services を実行している証明機関です。 VPN 構成には、Active Directory ベースの公開キー基盤 (PKI) が必要です。

組織では、ユーザー、デバイス、またはサービスの id を対応する公開キーにバインドすることによってセキュリティを強化するために AD CS を使用できます。 AD CS には、証明書の登録と失効多様な拡張性の高い環境で管理できるようにする機能も含まれています。 詳細については、次を参照してください。 [Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx)と[公開キー インフラストラクチャの設計ガイダンス](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)します。

デプロイの完了時に、CA で次の証明書テンプレートを構成します。

-   ユーザー認証証明書テンプレート

-   VPN サーバー認証証明書テンプレート

-   NPS サーバー認証証明書テンプレート

### <a name="certificate-templates"></a>証明書テンプレート

証明書テンプレートは、証明機関 (CA) の管理タスクを選択したタスクのあらかじめ構成されている証明書を発行することで簡略化が大幅にできます。 証明書テンプレート MMC スナップインで、次のタスクを実行することができます。

-   各証明書テンプレートのプロパティを表示します。

-   コピーして、証明書テンプレートを変更します。

-   ユーザーを制御し、コンピューターがテンプレートの読み取りし、証明書を登録します。

-   証明書テンプレートに関連するその他の管理タスクを実行します。

証明書テンプレートは、エンタープライズ証明機関 (CA) の不可欠な部分です。 これらは、一連のルールと証明書の登録、使用、および管理の形式では、環境の証明書ポリシーの重要な要素です。

詳細については、次を参照してください。[証明書テンプレート](https://technet.microsoft.com/library/cc730705.aspx)します。

### <a name="digital-server-certificates"></a>サーバーのデジタル証明書

このデプロイ ガイドでは、Active Directory 証明書サービス (AD CS) を使用して登録して、リモート アクセス サーバーと NPS インフラストラクチャ サーバーに証明書を自動的に登録するための手順を提供します。 AD CS を使用すると、公開キー基盤 (PKI) を構築し、組織の公開キーの暗号化、デジタル証明書、およびデジタル署名機能を提供できます。

デジタル サーバー証明書、ネットワーク上のコンピューター間の認証を使用する場合、証明書を提供します。

1.  暗号化による機密性。

2.  デジタル署名によって整合性。

3.  コンピューター ネットワーク上のコンピューター、ユーザー、またはデバイス アカウントと証明書のキーを関連付けることによって認証されます。

詳細については、次を参照してください。 [AD CS のステップ バイ ステップ ガイド。2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)します。

## <a name="active-directory-domain-services-ad-ds"></a>Active Directory ドメイン サービス (AD DS)

AD DS では、分散データベースにより、ネットワーク リソース、およびディレクトリ対応アプリケーションに固有のデータが保存、管理されます。 管理者は、AD DS を使用して、ユーザー、コンピューター、その他のデバイスなどのネットワーク要素を、階層化された格納構造で管理できます。 階層化された格納構造は、Active Directory フォレスト、フォレスト内のドメイン、および各ドメイン内の組織単位 (OU) から構成されます。 AD DS を実行するサーバーは、ドメイン コントローラーと呼ばれます。

AD DS には、ユーザー アカウント、コンピューター アカウント、およびユーザーの資格情報を認証し、VPN 接続要求の承認を評価するによって保護されている拡張認証プロトコル (PEAP) に必要なアカウントのプロパティが含まれています。 AD DS の展開方法の詳細については、Windows Server 2016 を参照してください。[コア ネットワーク ガイド](../../../../networking/core-network-guide/Core-Network-Guide.md)します。



この展開の手順の完了時に、ドメイン コント ローラーで、次の項目を構成します。

-   コンピューターとユーザーのグループ ポリシーで証明書の自動登録を有効にします。

-   VPN ユーザーのグループを作成します。

-   VPN サーバーのグループを作成します。

-   NPS サーバーのグループを作成します。

### <a name="active-directory-users-and-computers"></a>Active Directory ユーザーとコンピューター

Active Directory ユーザーとコンピューターは、コンピューター、ユーザー、またはセキュリティ グループなどの物理エンティティを表すアカウントを含む AD DS のコンポーネントです。 セキュリティ グループは、管理者は、1 つの単位として管理できるユーザーまたはコンピューターのアカウントのコレクションです。 特定のグループに属しているユーザーおよびコンピューターのアカウントは、グループのメンバーと呼ばれます。

しない限り、Active Directory ユーザーとコンピューターのユーザー アカウントが NPS が承認プロセスの中に評価されるダイヤルイン プロパティを持つ、**ネットワーク アクセス許可**ユーザー アカウントのプロパティに設定されて**コントロールNPS ネットワーク ポリシーでアクセス**します。 これは、すべてのユーザー アカウントの既定の設定です。 場合によっては、ただし、この設定があります、別の VPN を使用した接続からユーザーをブロックする構成。 この可能性を防ぐには、ユーザー アカウントのダイヤルイン プロパティを無視する NPS サーバーを構成できます。

詳細については、次を参照してください。[無視ユーザーのアカウントのダイヤルイン プロパティを構成する NPS](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)します。



### <a name="group-policy-management"></a>グループ ポリシーの管理

グループ ポリシーの管理は、セキュリティとユーザーの情報を含む、ユーザーとコンピューターの設定の変更と構成をディレクトリ ベースで管理できます。 グループ ポリシーを使用して、ユーザーとコンピューターのグループの構成を定義します。

グループ ポリシーとは、レジストリ エントリ、セキュリティ、ソフトウェアのインストール、スクリプト、フォルダー リダイレクト、リモート インストール サービス、および Internet Explorer のメンテナンスの設定を指定できます。 作成したグループ ポリシー設定は、グループ ポリシー オブジェクト (GPO) 内に格納されます。 GPO を選択した Active Directory システム コンテナーに関連付けることによって、サイト、ドメイン、および Ou、ユーザーとこれらの Active Directory コンテナー内のコンピューターに GPO の設定を適用することができます。 企業全体にわたるグループ ポリシー オブジェクトを管理するには、グループ ポリシー管理エディター Microsoft 管理コンソール (MMC) を使用することができます。


## <a name="windows-10-vpn-clients"></a>Windows 10 の VPN クライアント

サーバーのコンポーネントに加えて、VPN を使用するように構成するクライアント コンピューターで Windows 10 Anniversary Update (バージョン 1607) を実行していることを確認します。 Windows 10 の VPN クライアントを Active Directory ドメインにドメインに参加している必要があります。


Windows 10 の VPN クライアントは、高い構成可能な多くのオプションを提供しています。 このシナリオでは、特定の機能をよく示すためには、表 1 は、このデプロイで参照 VPN 機能のカテゴリおよび特定の構成を識別します。 この展開の後半で説明した VPNv2 構成サービス プロバイダー (CSP) を使用して、これらの機能の個別の設定を構成します。 

表 1. VPN の機能とこのデプロイで説明されている構成

| **VPN 機能** | **展開シナリオの構成**         |
|-----------------|-----------------------------------------------|
| 接続の種類 | ネイティブの IKEv2                                  |
| ルーティング         | 分割トンネリング                               |
| 名前解決 | ドメイン名情報一覧と DNS サフィックス   |
| トリガーします。      | 常にオンおよび信頼されたネットワーク検出       |
| 認証  | TPM で保護されたユーザー証明書と共に PEAP-TLS で |
---

>[!NOTE] 
>PEAP-TLS と TPM の「保護されている拡張認証プロトコルとトランスポート層セキュリティ」と「トラステッド プラットフォーム モジュール」をそれぞれされます。

### <a name="vpnv2-csp-nodes"></a>VPNv2 CSP ノード

この展開では、それを ProfileXML VPNv2 CSP ノードを使用する、Windows 10 クライアント コンピューターに配信される VPN プロファイルを作成します。 構成サービス プロバイダー (Csp) は、Windows クライアント; 内のさまざまな管理機能を公開するインターフェイスです。概念的には、Csp は動作グループ ポリシーのしくみに似ています。 各 CSP が、個々 の設定を表すノードを構成します。 グループ ポリシーの設定と同様に、レジストリ キー、ファイル、アクセス許可を CSP 設定を関連付けることができます。 グループ ポリシー管理エディターを使用してグループ ポリシー オブジェクト (Gpo) を構成する方法と同様の Microsoft Intune などのモバイル デバイス管理 (MDM) ソリューションを使用して CSP のノードを構成します。 Intune などの MDM 製品では、オペレーティング システムで、CSP を構成するユーザー フレンドリな構成オプションを提供します。

![CSP の構成をモバイル デバイス管理](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

ただし、Intune 管理コンソールのようなユーザー インターフェイス (UI) から直接 CSP ノードを構成することはできません。 このような場合は、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 設定を構成する必要があります手動でします。 OMA Uri を構成するには、OMA Device Management protocol (OMA-DM)、最近のほとんどの Apple、Android、および Windows デバイスをサポートする汎用デバイス管理の仕様を使用します。 、OMA-DM 仕様に準拠している限り、すべての MDM 製品が、同じ方法でこれらのオペレーティング システムと対話する必要があります。

Windows 10 には、多くの Csp が提供していますが、VPNv2 CSP を使用して、VPN クライアントを構成するこの展開に重点を置いています。 VPNv2 CSP 一意 CSP ノードで Windows 10 の各 VPN プロファイルの設定の構成を許可します。 という名前のノードは、VPNv2 CSP にも含まれている*それを ProfileXML*、すべての設定を構成することのできる 1 つのノードではなく、個別にします。 それを ProfileXML の詳細については、このデプロイでは後で「それを ProfileXML の概要」セクションを参照してください。 詳細については、各 VPNv2 CSP ノードは、次を参照してください。、 [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp)します。



## <a name="next-steps"></a>次のステップ

- [高度な Always On VPN 機能の一部について説明します](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 展開の計画を開始します。](deploy/always-on-vpn-deploy-deployment.md)


---

## <a name="related-topics"></a>関連トピック
- [Microsoft Azure 仮想マシンのマイクロソフト サーバー ソフトウェア サポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines):この記事では、Microsoft Azure の仮想マシン環境 (インフラストラクチャとしてのサービス) で Microsoft サーバー ソフトウェアを実行するためのサポート ポリシーについて説明します。

- [リモート アクセス](../../Remote-Access.md):このトピックでは、Windows Server 2016 でのリモート アクセス サーバーの役割の概要を示します。

- [Windows 10 の VPN に関するテクニカル ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide):このガイドでは、社内の VPN ソリューションでの Windows 10 クライアントと、展開を構成する方法が決定説明します。 このガイドでは、VPNv2 構成サービス プロバイダー (CSP) を参照し、モバイル デバイス管理 (MDM) の構成手順が Windows 10 用 Microsoft Intune と VPN プロファイルのテンプレートを使用してを提供します。

- [コア ネットワーク ガイド](../../../../networking/core-network-guide/Core-Network-Guide.md):このガイドは、計画およびネットワークが完全に機能し、新しいフォレスト内の新しい Active Directory ドメインに必要なコア コンポーネントを展開する方法について説明します。

- [ドメイン ネーム システム (DNS)](../../../../networking/dns/dns-top.md):このトピックでは、ドメイン ネーム システム (DNS) の概要を示します。 Windows Server 2016 では、DNS とは、サーバー マネージャーまたは Windows PowerShell コマンドを使用して、インストール可能なサーバーの役割です。 新しい Active Directory フォレストおよびドメインをインストールする場合に自動的に DNS がインストールされていると Active Directory フォレストおよびドメインのグローバル カタログ サーバーとして。 

- [Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx):このドキュメントでは、Active Directory 証明書サービス (AD CS) で Windows Server® 2012 の概要を示します。 AD CS は、公開キー基盤 (PKI) を構築し、公開キーの暗号化、デジタル証明書、およびデジタル署名機能を組織に提供するサーバーの役割です。

- [公開キー基盤設計ガイダンス](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx):この wiki は、公開キー基盤 (Pki) の設計ガイダンスを提供します。 PKI と証明機関 (CA) 階層を構成する前に、組織のセキュリティ ポリシーと証明書実施規定 (CPS) があります。

- [AD CS のステップ バイ ステップ ガイド:2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx):このステップ バイ ステップ ガイドでは、ラボ環境で Active Directory® 証明書サービス (AD CS) の基本的な構成を設定するために必要な手順について説明します。 Windows Server® 2008 R2 の AD CS では、作成および公開キー テクノロジを使用して、ソフトウェア セキュリティ システムで使用される公開キー証明書を管理するためのカスタマイズ可能なサービスを提供します。

- [ネットワーク ポリシー サーバー (NPS)](../../../../networking/technologies/nps/nps-top.md):このトピックでは、Windows Server 2016 でネットワーク ポリシー サーバーの概要を示します。 ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。 

---
