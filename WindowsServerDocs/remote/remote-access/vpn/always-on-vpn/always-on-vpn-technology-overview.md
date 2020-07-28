---
title: Always On VPN テクノロジの概要
description: 'このページでは、Always On VPN テクノロジの概要と詳細なドキュメントへのリンクを提供します。 '
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 12c80e7e266ac3a8c788781a4d98f0a856164084
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182018"
---
# <a name="always-on-vpn-technology-overview"></a>Always On VPN テクノロジの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** Always On VPN の機能強化について説明します。](always-on-vpn-enhancements.md)
- [**次のようになります。** Always On VPN の高度な機能について説明します。](deploy/always-on-vpn-adv-options.md)

この展開では、Windows Server 2016 を実行している新しいリモートアクセスサーバーをインストールし、展開のために既存のインフラストラクチャの一部を変更する必要があります。

次の図は Always On VPN の展開に必要なインフラストラクチャを示しています。

![Always On VPN インフラストラクチャ](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

この図に示されている接続プロセスは、次の手順で構成されています。

1. Windows 10 VPN クライアントは、パブリック DNS サーバーを使用して、VPN ゲートウェイの IP アドレスに対して名前解決のクエリを実行します。

2. VPN クライアントは、DNS によって返された IP アドレスを使用して、VPN ゲートウェイに接続要求を送信します。

3. VPN ゲートウェイは、リモート認証ダイヤルインユーザーサービス (RADIUS) クライアントとしても構成されます。VPN RADIUS クライアントは、接続要求の処理のために、組織または企業の NPS サーバーに接続要求を送信します。

4. NPS サーバーは、認証と認証の実行など、接続要求を処理し、接続要求を許可するか拒否するかを決定します。

5. NPS サーバーは、アクセス許可またはアクセス拒否応答を VPN ゲートウェイに転送します。

6. 接続は、NPS サーバーから VPN サーバーが受信した応答に基づいて開始または終了します。

上の図に示されている各インフラストラクチャコンポーネントの詳細については、次のセクションを参照してください。

>[!NOTE]
>これらのテクノロジの一部が既にネットワークに展開されている場合は、この展開のガイダンスに記載されている手順を使用して、この展開の目的でテクノロジの追加構成を行うことができます。

## <a name="domain-name-system-dns"></a>ドメイン ネーム システム (DNS)

内部ゾーンと外部ドメインネームシステム (DNS) ゾーンの両方が必要です。これは、内部ゾーンが外部ゾーンの委任されたサブドメインであることを前提としています (たとえば、corp.contoso.com と contoso.com)。

詳細については、 [「ドメインネームシステム (DNS)](../../../../networking/dns/dns-top.md) 」または「[コアネットワークガイド」](../../../../networking/core-network-guide/core-network-guide.md)を参照してください。

>[!NOTE]
>分割ブレイン DNS (別の DNS ゾーンで内部および外部で同じドメイン名を使用) または関連のない内部および外部ドメイン (たとえば、contoso. local と contoso.com) などの他の DNS 設計も可能です。 スプリットブレイン DNS の展開の詳細については、「[スプリットブレイン Dns 展開に Dns ポリシーを使用する](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)」を参照してください。

## <a name="firewalls"></a>ファイアウォール

VPN と RADIUS 通信の両方が正常に機能するために必要なトラフィックがファイアウォールによって許可されていることを確認します。

詳細については、「 [Configure firewall FOR RADIUS Traffic](../../../../networking/technologies/nps/nps-firewalls-configure.md)」を参照してください。

## <a name="remote-access-as-a-ras-gateway-vpn-server"></a>RAS ゲートウェイ VPN サーバーとしてのリモートアクセス

Windows Server 2016 では、リモートアクセスサーバーの役割は、ルーターとリモートアクセスサーバーの両方として正常に動作するように設計されています。そのため、さまざまな機能をサポートしています。 この展開のガイダンスでは、これらの機能のごく一部のみを必要とします。 IKEv2 VPN 接続と LAN ルーティングのサポートです。

IKEv2 は、「インターネット技術標準化委員会におけるコメント7296の要求」で説明されている VPN トンネリングプロトコルです。 IKEv2 の主な利点は、基になるネットワーク接続で許容が中断されることです。 たとえば、接続が一時的に失われた場合、またはユーザーがクライアントコンピューターをあるネットワークから別のネットワークに移動した場合、IKEv2 はネットワーク接続が再確立されたときに VPN 接続を自動的に復元します。ユーザーによる操作は必要ありません。

RAS ゲートウェイを使用すると、VPN 接続を展開して、エンドユーザーが組織のネットワークとリソースにリモートアクセスできるようにすることができます。 Always On VPN を展開すると、リモートコンピューターがインターネットに接続されている場合は常に、クライアントと組織のネットワークの間に永続的な接続が維持されます。 RAS ゲートウェイでは、プライマリオフィスとブランチオフィスの間など、異なる場所にある2つのサーバー間にサイト間 VPN 接続を作成し、ネットワーク内のユーザーがインターネットなどの外部リソースにアクセスできるようにネットワークアドレス変換 (NAT) を使用することもできます。 また、RAS ゲートウェイでは Border Gateway Protocol (BGP) がサポートされています。これは、リモートオフィスの場所に BGP をサポートするエッジゲートウェイもある場合に動的ルーティングサービスを提供します。

Windows PowerShell コマンドとリモートアクセス Microsoft 管理コンソール (MMC) を使用して、リモートアクセスサービス (RAS) ゲートウェイを管理できます。

## <a name="network-policy-server-nps"></a>ネットワーク ポリシー サーバー (NPS)

NPS では、接続要求の認証と承認を行うために、組織全体のネットワークアクセスポリシーを作成して適用することができます。 NPS をリモート認証ダイヤルインユーザーサービス (RADIUS) サーバーとして使用する場合は、VPN サーバーなどのネットワークアクセスサーバーを NPS の RADIUS クライアントとして構成します。

また、NPS が接続要求を承認するために使用するネットワーク ポリシーを構成して、NPS がアカウンティング情報をローカル ハード ディスク上のログ ファイルまたは Microsoft SQL Server データベースに記録するように RADIUS アカウンティングを構成できます。

詳細については、「[Network Policy Server (NPS) (ネットワーク ポリシー サーバー (NPS))](../../../../networking/technologies/nps/nps-top.md)」をご覧ください。

## <a name="active-directory-certificate-services"></a>Active Directory 証明書サービス

証明機関 (CA) サーバーは、Active Directory 証明書サービスを実行している証明機関です。 VPN 構成には、Active Directory ベースの公開キー基盤 (PKI) が必要です。

組織は、AD CS を使用して、個人、デバイス、またはサービスの id を対応する公開キーにバインドすることにより、セキュリティを強化することができます。 AD CS には、さまざまなスケーラブルな環境で証明書の登録と失効を管理できる機能も含まれています。 詳細については、「 [Active Directory 証明書サービスの概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11))」および「[公開キー基盤の設計ガイダンス](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/designing-and-implementing-a-pki-part-i-design-and-planning/ba-p/396953)」を参照してください。

展開が完了したら、CA で次の証明書テンプレートを構成します。

- ユーザー認証証明書テンプレート

- VPN サーバー認証証明書テンプレート

- NPS サーバー認証証明書テンプレート

### <a name="certificate-templates"></a>証明書テンプレート

証明書テンプレートを使用すると、選択したタスク用に事前に構成された証明書を発行できるようになるため、証明機関 (CA) の管理タスクを大幅に簡略化できます。 証明書テンプレート MMC スナップインを使用すると、次のタスクを実行できます。

- 各証明書テンプレートのプロパティの表示

- 証明書テンプレートのコピーと変更

- テンプレートを読み取って証明書を登録できるユーザーとコンピューターを制御します。

- 証明書テンプレートに関連するその他の管理タスクの実行

証明書テンプレートは、エンタープライズ証明機関 (CA) に不可欠な要素です。 証明書テンプレートは、特定の環境における証明書ポリシーの重要な要素であり、証明書の登録、使用、および管理に必要な規則と形式のセットです。

詳細については、「[証明書テンプレート](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc730705(v=ws.11))」を参照してください。

### <a name="digital-server-certificates"></a>デジタルサーバー証明書

この展開ガイドでは、Active Directory 証明書サービス (AD CS) を使用して、証明書を登録し、リモートアクセスと NPS インフラストラクチャサーバーに自動的に登録する方法について説明します。 AD CS を使用すると、公開キー基盤 (PKI) を構築し、公開キーの暗号化、デジタル証明書、およびデジタル署名機能を組織に提供できます。

ネットワーク上のコンピューター間の認証にデジタルサーバー証明書を使用すると、証明書によって次のことが実現されます。

1. 暗号化による機密性

2. デジタル署名による整合性。

3. コンピューターネットワーク上のコンピューター、ユーザー、またはデバイスアカウントに証明書キーを関連付けることによる認証。

詳細については、「 [Active Directory 証明書サービスの概要](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11))」を参照してください。

## <a name="active-directory-domain-services-ad-ds"></a>Active Directory Domain Services (AD DS)

AD DS では、分散データベースにより、ネットワーク リソース、およびディレクトリ対応アプリケーションに固有のデータが保存、管理されます。 管理者は、AD DS を使用して、ユーザー、コンピューター、その他のデバイスなどのネットワーク要素を、階層化された格納構造で管理できます。 階層化された格納構造は、Active Directory フォレスト、フォレスト内のドメイン、および各ドメイン内の組織単位 (OU) から構成されます。 AD DS を実行するサーバーは、ドメイン コントローラーと呼ばれます。

AD DS には、保護された拡張認証プロトコル (PEAP) がユーザーの資格情報を認証し、VPN 接続要求の承認を評価するために必要なユーザーアカウント、コンピューターアカウント、およびアカウントのプロパティが含まれています。 AD DS の展開の詳細については、「Windows Server 2016[コアネットワークガイド](../../../../networking/core-network-guide/Core-Network-Guide.md)」を参照してください。

この展開の手順を完了すると、ドメインコントローラーで次の項目が構成されます。

- コンピューターとユーザーのグループポリシーでの証明書の自動登録を有効にする

- VPN ユーザーグループを作成する

- VPN サーバーグループを作成する

- NPS サーバーグループを作成する

### <a name="active-directory-users-and-computers"></a>Active Directory ユーザーとコンピューティング

Active Directory ユーザーとコンピューターは AD DS のコンポーネントであり、コンピューター、個人、セキュリティグループなどの物理的なエンティティを表すアカウントが含まれています。 セキュリティグループは、管理者が1つの単位として管理できるユーザーアカウントまたはコンピューターアカウントのコレクションです。 特定のグループに属するユーザーとコンピューターのアカウントは、グループメンバーと呼ばれます。

Active Directory ユーザーとコンピューターのユーザーアカウントには、nps が承認プロセス中に評価するダイヤルインプロパティがあります。これは、ユーザーアカウントの **"ネットワークアクセス許可**" プロパティが**nps ネットワークポリシーを介したアクセスを制御**するように設定されている場合を除きます。 これは、すべてのユーザーアカウントの既定の設定です。 ただし、場合によっては、この設定によって、ユーザーが VPN を使用した接続をブロックする構成が異なる場合があります。 この可能性から保護するために、ユーザーアカウントのダイヤルインプロパティを無視するように NPS サーバーを構成することができます。

詳細については、「[ユーザーアカウントのダイヤルインプロパティを無視するように NPS を構成する](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)」を参照してください。

### <a name="group-policy-management"></a>グループ ポリシー管理

グループポリシー管理を使用すると、セキュリティやユーザー情報など、ユーザーとコンピューターの設定のディレクトリベースの変更と構成を管理できます。 グループポリシーを使用して、ユーザーとコンピューターのグループの構成を定義します。

グループポリシーでは、レジストリエントリ、セキュリティ、ソフトウェアのインストール、スクリプト、フォルダーリダイレクト、リモートインストールサービス、および Internet Explorer のメンテナンスの設定を指定できます。 作成したグループポリシー設定は、グループポリシーオブジェクト (GPO) に含まれています。 GPO を選択した Active Directory システムコンテナー (サイト、ドメイン、Ou) に関連付けることによって、GPO の設定を Active Directory コンテナー内のユーザーとコンピューターに適用できます。 企業全体でグループポリシーオブジェクトを管理するには、Microsoft 管理コンソール (MMC) のグループポリシー管理エディターを使用します。

## <a name="windows-10-vpn-clients"></a>Windows 10 VPN クライアント

サーバーコンポーネントに加えて、VPN を使用するように構成するクライアントコンピューターで、Windows 10 周年更新プログラム (バージョン 1607) が実行されていることを確認します。 Windows 10 VPN クライアントは、Active Directory ドメインに参加している必要があります。


Windows 10 VPN クライアントは、高度な構成が可能であり、多くのオプションが用意されています。 このシナリオで使用される具体的な機能をわかりやすく説明するために、表1は、この展開が参照する VPN 機能のカテゴリと特定の構成を示しています。 これらの機能の個々の設定を構成するには、この展開で後ほど説明する VPNv2 構成サービスプロバイダー (CSP) を使用します。

表 1 この展開で説明されている VPN の機能と構成

| VPN 機能     |     展開シナリオの構成         |
|-----------------|-----------------------------------------------|
| 接続の種類 |                 ネイティブ IKEv2                  |
|     ルーティング     |                分割トンネリング                |
| 名前解決 |  ドメイン名情報の一覧と DNS サフィックス  |
|   トリガ    |    Always On と信頼されたネットワーク検出    |
| 認証  | TPM を使用した PEAP-TLS-保護されたユーザー証明書 |

>[!NOTE]
>PEAP-TLS と TPM は、"トランスポート層セキュリティで保護された拡張認証プロトコル" と "トラステッドプラットフォームモジュール" です。

### <a name="vpnv2-csp-nodes"></a>VPNv2 CSP ノード

この展開では、ProfileXML VPNv2 CSP ノードを使用して、Windows 10 クライアントコンピューターに配布される VPN プロファイルを作成します。 構成サービスプロバイダー (Csp) は、Windows クライアント内のさまざまな管理機能を公開するインターフェイスです。概念的には、Csp はグループポリシーの動作と同様に機能します。 各 CSP には、個々の設定を表す構成ノードがあります。 グループポリシー設定と同様に、CSP 設定をレジストリキー、ファイル、アクセス許可などに関連付けることができます。 グループポリシー管理エディターを使用してグループポリシーオブジェクト (Gpo) を構成する方法と同様に、Microsoft Intune などのモバイルデバイス管理 (MDM) ソリューションを使用して CSP ノードを構成します。 Intune のような MDM 製品は、オペレーティングシステムで CSP を構成するユーザーフレンドリな構成オプションを提供します。

![モバイルデバイス管理から CSP への構成](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

ただし、Intune 管理コンソールのようなユーザーインターフェイス (UI) を使用して、一部の CSP ノードを直接構成することはできません。 このような場合は、Open Mobile アライアンス Uniform Resource Identifier (OMA-URI) 設定を手動で構成する必要があります。 Oma-uri は、最新の Apple、Android、および Windows デバイスでサポートされているユニバーサルデバイス管理仕様である oma-uri デバイス管理プロトコル (OMA-URI) を使用して構成します。 OMA-URI 仕様に準拠している限り、すべての MDM 製品は同じ方法でこれらのオペレーティングシステムと対話する必要があります。

Windows 10 には多くの Csp が用意されていますが、この展開では、VPNv2 CSP を使用して VPN クライアントを構成することに重点を置いています。 VPNv2 CSP を使用すると、一意の CSP ノードを介して、Windows 10 の各 VPN プロファイル設定を構成できます。 VPNv2 CSP には、 *ProfileXML*と呼ばれるノードも含まれています。このノードを使用すると、個別にではなく、すべての設定を1つのノードで構成できます。 ProfileXML の詳細については、後の「ProfileXML の概要」を参照してください。 各 VPNv2 CSP ノードの詳細については、 [VPNV2 csp](/windows/client-management/mdm/vpnv2-csp)を参照してください。

## <a name="next-steps"></a>次のステップ

- [いくつかの高度な Always On VPN 機能について説明します。](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 展開の計画を開始する](deploy/always-on-vpn-deploy-deployment.md)

## <a name="related-topics"></a>関連トピック

- [Microsoft Azure の仮想マシンに対する microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): この記事では、Microsoft Azure 仮想マシン環境 (サービスとしてのインフラストラクチャ) で microsoft サーバーソフトウェアを実行するためのサポートポリシーについて説明します。

- [リモートアクセス](../../Remote-Access.md): このトピックでは、Windows server 2016 のリモートアクセスサーバーの役割の概要について説明します。

- [Windows 10 VPN の技術ガイド](/windows/access-protection/vpn/vpn-guide): このガイドでは、エンタープライズ VPN ソリューションで windows 10 クライアントに対して行うことの決定と、展開を構成する方法について説明します。 このガイドでは、「VPNv2 Configuration Service Provider (CSP)」(VPNv2 構成サービス プロバイダー (CSP)) を参照しており、Microsoft Intune、および Windows 10 用の VPN プロファイル テンプレートを使用して、モバイル デバイス管理 (MDM) を構成する手順を示します。

- [コアネットワークガイド](../../../../networking/core-network-guide/Core-Network-Guide.md): このガイドでは、新しいフォレストで、完全に機能するネットワークと新しい Active Directory ドメインに必要なコアコンポーネントを計画および展開する方法について説明します。

- [ドメインネームシステム (dns)](../../../../networking/dns/dns-top.md): このトピックでは、ドメインネームシステム (dns) の概要について説明します。 Windows Server 2016 では、DNS はサーバーの役割であり、サーバーマネージャーまたは Windows PowerShell コマンドを使用してインストールできます。 新しい Active Directory フォレストとドメインをインストールする場合は、フォレストとドメインのグローバルカタログサーバーとして Active Directory と共に DNS が自動的にインストールされます。

- [Active Directory 証明書サービスの概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831740(v=ws.11)): このドキュメントでは、Windows Server 2012 の Active Directory 証明書サービス (AD CS) の概要について説明 &reg; します。 AD CS は、公開キー基盤 (PKI) を構築し、公開キーの暗号化、デジタル証明書、およびデジタル署名機能を組織に提供するサーバーの役割です。

- [公開キー基盤の設計ガイダンス](https://techcommunity.microsoft.com/t5/ask-the-directory-services-team/designing-and-implementing-a-pki-part-i-design-and-planning/ba-p/396953): このフォーラムでは、公開キー基盤 (pki) の設計に関するガイダンスを提供します。 PKI と証明機関 (CA) 階層を構成する前に、組織のセキュリティポリシーと証明書作成ステートメント (CPS) に注意する必要があります。

- [Active Directory 証明書サービスの概要](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831740(v=ws.11)): このステップバイステップガイドでは、 &reg; ラボ環境で Active Directory 証明書サービス (AD CS) の基本構成を設定するために必要な手順について説明します。 Windows Server 2008 R2 の AD CS &reg; は、公開キーテクノロジを採用しているソフトウェアセキュリティシステムで使用される公開キー証明書を作成および管理するためのカスタマイズ可能なサービスを提供します。

- [ネットワークポリシーサーバー (NPS)](../../../../networking/technologies/nps/nps-top.md): このトピックでは、Windows server 2016 のネットワークポリシーサーバーの概要について説明します。 ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。
