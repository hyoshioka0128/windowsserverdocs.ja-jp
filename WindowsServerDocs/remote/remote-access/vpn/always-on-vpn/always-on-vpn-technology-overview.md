---
title: Always On VPN テクノロジの概要
description: 'このページでは、詳細なドキュメントへのリンクを使って、Always On VPN テクノロジの簡単な概要です。 '
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: fd3f7c6ca8555e270aabf04bbee6800ed284080c
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031326"
---
# Always On VPN テクノロジの概要
>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** Always On VPN の機能強化について説明します](always-on-vpn-enhancements.md)<br>
& #187 です。 [ **[次へ]:** Always On VPN の高度な機能について説明します](deploy/always-on-vpn-adv-options.md)

この展開にする必要があります Windows Server 2016 を実行している新しいリモート アクセス サーバーをインストールしたりする、既存のインフラストラクチャの展開の一部を変更します。

次の図は、Always On VPN を展開するために必要なインフラストラクチャを示します。

![Always On VPN インフラストラクチャ](../../../media/Always-On-Vpn/Ao-Vpn-Overview.jpg)

次の図に示されている接続のプロセスは、次の手順で構成されます。

1. パブリック DNS サーバーを使用して、Windows 10 VPN クライアントは、VPN ゲートウェイの IP アドレスの名前解決クエリを実行します。

2. DNS によって返される IP アドレスを使用して、VPN クライアントは、VPN ゲートウェイへの接続要求を送信します。

3. VPN ゲートウェイがリモート認証ダイヤルイン ユーザー サービス \(RADIUS\) としても構成されているクライアントです。VPN クライアントは、接続要求の処理の組織や企業の NPS サーバーに接続要求を送信します。

4. NPS サーバーは、承認、および認証の実行を含む、接続要求を処理し、許可または接続要求を拒否するかどうかを決定します。

5. NPS サーバーは、VPN ゲートウェイへのアクセス許可や、アクセス拒否応答を転送します。

6. 接続を開始または終了される NPS サーバーから受信した VPN サーバーの応答に基づいています。

上の図に示されている各インフラストラクチャ コンポーネントについて詳しくは、次のセクションを参照してください。

>[!NOTE]
>これらのテクノロジを展開して、ネットワーク上のいくつか既にがある場合は、この展開の目的のためのテクノロジの追加の構成を実行するこの展開ガイドで」の手順を使用できます。

## ドメイン ネーム システム (DNS)

内部および外部の両方のドメイン ネーム システム (DNS) ゾーンが必要な場合は、内部のゾーンされる委任された外部ゾーン (たとえば、corp.contoso.com、contoso.com) のサブドメインを想定しています。

[ドメイン ネーム システム (DNS)](../../../../networking/dns/dns-top.md)または[コア ネットワーク ガイド](../../../../networking/core-network-guide/core-network-guide.md)の詳細について説明します。




>[!NOTE] 
>他の DNS (同じドメイン名を使用内部と外部の別の DNS ゾーンで) ブレイン DNS などの設計, または無関係内部と外部ドメイン (contoso.local および contoso.com など) も可能。 ブレイン DNS の展開について詳しくは、[分割/ブレイン DNS の展開に DNS ポリシーを使用して](../../../../networking/dns/deploy/split-brain-DNS-deployment.md)を参照してください。

## ファイアウォール

ファイアウォールが正常に機能する VPN と RADIUS の両方の通信に必要なトラフィックを許可することを確認します。

詳細については、 [RADIUS トラフィック用にファイアウォールを構成する](../../../../networking/technologies/nps/nps-firewalls-configure.md)を参照してください。

## RAS ゲートウェイの VPN サーバーとしてのリモート アクセス

In Windows Server 2016, the Remote Access server role is designed to perform well as both a router and a remote access server; therefore, it supports a wide array of features. この展開ガイダンスについては、これらの機能の小さなサブセットのみが必要な: IKEv2 VPN 接続および LAN ルーティングのサポート。

IKEv2 は、VPN トンネリング プロトコルのコメント 7296 インターネット技術標準化委員会要求で説明します。 IKEv2 の主な利点は、基になるネットワーク接続の中断を許容できることができます。 たとえば、接続が一時的に失われた場合、または、ユーザーでは、1 つのネットワークからクライアント コンピューターを移動する場合は、IKEv2 自動的に接続が復元される VPN ネットワーク接続を再び-ユーザーの介入なしすべてします。

RAS ゲートウェイを使用すると、ユーザーに提供終了、組織のネットワークとリソースへのリモート アクセス VPN 接続を展開することができます。 リモート コンピューターがインターネットに接続されているときに、クライアントと組織のネットワーク間で永続的な接続を維持 Always On VPN を展開します。 RAS ゲートウェイ、また、プライマリのオフィスと、ブランチ オフィスの間など、さまざまな場所にある 2 つのサーバー間でサイト間 VPN 接続を作成して使うネットワーク アドレス変換 \(NAT\) 外部ネットワーク内のユーザーがアクセスできるようにインターネットなどのリソースです。 また、RAS ゲートウェイは、遠隔地のオフィスも BGP をサポートする edge ゲートウェイが動的なルーティング サービスを提供するボーダー ゲートウェイ プロトコル (BGP) をサポートしています。

リモート アクセス サービス (RAS) ゲートウェイは、Windows PowerShell コマンドとリモート アクセス Microsoft 管理コンソール (MMC) を使用して管理できます。



## ネットワーク ポリシー サーバー (NPS)

NPS を作成し、接続要求の認証と承認の組織全体のネットワーク アクセス ポリシーを適用できます。 NPS をリモート認証ダイヤルイン ユーザー サービス (RADIUS) サーバーとして使用する場合は、NPS の RADIUS クライアントとして、VPN サーバーなどのネットワーク アクセス サーバーを構成します。

構成することも、接続要求を承認する NPS を使用するネットワーク ポリシーと NPS アカウンティング情報をローカルのハード ディスクや Microsoft SQL Server データベース内のファイルをログに記録をログに記録するように、RADIUS アカウンティングを構成することができます。

詳細については、[ネットワーク ポリシー サーバー (NPS)](../../../../networking/technologies/nps/nps-top.md)を参照してください。


## Active Directory 証明書サービス

証明機関 (CA) サーバーでは、Active Directory 証明書サービスを実行している証明機関です。 VPN 構成には、Active Directory ベースの公開キー基盤 (PKI) が必要です。

組織では、ユーザー、デバイス、またはサービスの id を対応する公開キーにバインドすることによって、セキュリティを強化するために、AD CS を使用できます。 AD CS には、証明書の登録と、さまざまなスケーラブルな環境で失効を管理することを許可する機能も含まれています。 詳細については、 [Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx)と[公開キー インフラストラクチャの設計ガイダンス](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx)を参照してください。

展開の完了時に、CA で次の証明書テンプレートを構成します。

-   ユーザーの認証証明書テンプレート

-   VPN サーバー認証証明書テンプレート

-   NPS サーバー認証証明書テンプレート

### 証明書テンプレート

大幅に証明書テンプレートは、証明機関 (CA) の管理タスクを簡素化、選択したタスクの事前に構成された証明書を発行することを許可することができます。 証明書テンプレート MMC スナップインを次のタスクを実行できます。

-   各証明書テンプレートのプロパティを表示します。

-   コピーし、証明書テンプレートを変更します。

-   ユーザーを制御し、コンピューターが読み取るテンプレートと証明書を登録します。

-   証明書テンプレートに関連するその他の管理タスクを実行します。

証明書テンプレートは、エンタープライズ証明機関 (CA) の重要な一部です。 これらは、一連の規則と証明書の登録、使用、および管理の形式は、特定の環境の証明書ポリシーの重要な要素です。

詳細については、[証明書テンプレート](https://technet.microsoft.com/library/cc730705.aspx)を参照してください。

### サーバーのデジタル証明書

この展開ガイドは、Active Directory 証明書サービス (AD CS) を使用して登録して、リモート アクセスとインフラストラクチャの NPS サーバーに証明書を自動的に登録するための手順を提供します。 AD CS を使用すると、公開キー基盤 (PKI) をビルドして、組織の公開キーの暗号化、デジタル証明書とデジタル署名の機能を提供できます。

ネットワーク上のコンピューターの間の認証のデジタル サーバー証明書を使用する場合、証明書を提供します。

1.  機密性暗号化を使用します。

2.  整合性を通じてデジタル署名します。

3.  証明書のキーがコンピューター ネットワーク上のコンピューター、ユーザー、またはデバイスのアカウントに関連付けることによって認証します。

詳細については、次を参照してください。 [AD CS ステップ バイ ステップ ガイド: 2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)します。

## Active Directory ドメイン サービス (AD DS)

AD DS を格納およびディレクトリが有効なアプリケーションからのネットワーク リソースおよびアプリケーションに固有のデータに関する情報を管理する分散データベースを提供します。 管理者は、ユーザー、コンピューター、およびその他のデバイスなど、ネットワークの要素を階層的な包含構造に整理を AD DS を使用できます。 階層的な包含構造体が含まれています、Active Directory フォレストにはドメイン、フォレスト、組織単位 (Ou) でドメインごとにします。 AD DS を実行しているサーバーは、ドメイン コント ローラーと呼ばれます。

AD DS には、ユーザー アカウント、コンピューター アカウント、およびユーザーの資格情報を認証し、VPN 接続要求の承認を評価するによって保護されている拡張認証プロトコル (PEAP) 必要なアカウントのプロパティが含まれています。 AD DS の展開について詳しくは、Windows Server 2016 の[コア ネットワーク ガイド](../../../../networking/core-network-guide/Core-Network-Guide.md)を参照してください。



この展開の手順の完了時に、ドメイン コント ローラーで、次の項目を構成します。

-   コンピューターとユーザーのグループ ポリシーで証明書の自動登録を有効にします。

-   VPN のユーザー グループを作成します。

-   VPN サーバー グループを作成します。

-   NPS サーバー グループを作成します。

### Active Directory ユーザーとコンピューター

Active Directory ユーザーとコンピューターは、コンピューター、ユーザーまたはセキュリティ グループなどの物理エンティティを表すアカウントを含む AD DS のコンポーネントです。 セキュリティ グループは、管理者は、1 つの単位として管理できるユーザーまたはコンピューター アカウントのコレクションです。 特定のグループに参加しているユーザーとコンピューターのアカウントは、グループ メンバーと呼ばれます。

**NPS ネットワーク ポリシーでアクセスを制御するユーザー アカウントの**ネットワーク アクセス許可**のプロパティが設定されていない限り、Active Directory ユーザーとコンピューターでのユーザー アカウントが承認プロセスの中に NPS を評価するダイヤルイン プロパティを持つ**. これは、すべてのユーザー アカウントの既定の設定です。 場合によっては、ただし、この設定があります、ユーザーが VPN を使用して接続をブロックしている別の構成。 この可能性を防ぐには、ユーザー アカウントのダイヤルでプロパティを無視するように NPS サーバーを構成できます。

詳細については、[ユーザー アカウントを無視してダイヤルイン プロパティに NPS を構成する](../../../../networking/technologies/nps/nps-np-configure.md#configure-nps-to-ignore-user-account-dial-in-properties)を参照してください。



### グループ ポリシーの管理

グループ ポリシーの管理では、セキュリティとユーザーの情報を含む、ユーザーとコンピューターの設定の変更と構成をディレクトリ ベースで管理できるようにします。 ユーザーとコンピューターのグループの構成を定義するのにには、グループ ポリシーを使用します。

グループ ポリシーとレジストリ エントリ、セキュリティ、ソフトウェアのインストール、スクリプト、フォルダー リダイレクト、リモート インストール サービス、および Internet Explorer のメンテナンスの設定を指定できます。 グループ ポリシー オブジェクト (GPO) では、作成したグループ ポリシー設定が含まれています。 Active Directory システムのコンテナーを選択した GPO を関連付けることによって、サイト、ドメイン、および Ou-ユーザーとそれらの Active Directory コンテナー内のコンピューターに GPO の設定を適用することができます。 企業内でのグループ ポリシー オブジェクトを管理するには、グループ ポリシー管理エディター Microsoft 管理コンソール (MMC) を使用できます。


## Windows 10 VPN クライアント

サーバーのコンポーネントだけでなく、VPN を使用して構成するクライアント コンピューターが windows 10 Anniversary Update (version1607) を実行していることを確認します。 Active Directory ドメインにドメインに参加している Windows 10 VPN クライアントがある必要があります。


Windows 10 VPN クライアントは、高度に構成可能な多くのオプションを提供します。 このシナリオで使用する特定の機能をより適切に示すためには、表 1 は、この展開を参照して、VPN 機能カテゴリと特定の構成を識別します。 この展開で後で説明されている VPNv2 構成サービス プロバイダー (CSP) を使用して、これらの機能の個々 の設定が構成されます。 

表 1. VPN の機能と、この展開で説明されている構成

| **VPN の機能** | **展開シナリオの構成**         |
|-----------------|-----------------------------------------------|
| 接続の種類 | ネイティブ IKEv2                                  |
| ルーティング         | 分割トンネリング                               |
| 名前解決 | ドメイン名情報の一覧と DNS サフィックス   |
| トリガー      | Always On と信頼されたネットワークの検出       |
| Authentication  | TPM で保護されたユーザーの証明書を使って PEAP-TLS |
---

>[!NOTE] 
>PEAP-TLS と TPM は、「保護されている拡張認証プロトコルのトランスポート層セキュリティ」と「トラステッド プラットフォーム モジュール、」それぞれします。

### VPNv2 CSP ノード

この展開では、windows 10 クライアント コンピューターに配信される VPN プロファイルを作成するのに ProfileXML VPNv2 CSP のノードを使用します。 構成サービス プロバイダー (Csp) は、Windows クライアント内のさまざまな管理機能を公開するインターフェイスです。概念的には、Csp の動作と同様に、グループ ポリシーのしくみです。 各 CSP では、個々 の設定を表す構成の各ノードがあります。 グループ ポリシー設定のような CSP の設定のレジストリ キー、ファイル、アクセス許可を関連付けることができます。 グループ ポリシー オブジェクト (Gpo) を構成するグループ ポリシー管理エディターを使用する方法と同様の Microsoft Intune などのモバイル デバイス管理 (MDM) ソリューションを使用して、CSP のノードを構成します。 Intune などの MDM 製品は、オペレーティング システムで、CSP を構成するユーザーにわかりやすい構成オプションを提供します。

![CSP の構成をモバイル デバイス管理](../../../media/Always-On-Vpn/Vpn-Mdm.jpg)

ただし、いくつか Intune 管理コンソールのようなユーザー インターフェイス (UI) を通じて直接 CSP のノードを構成することはできません。 このような場合は、Open Mobile Alliance Uniform Resource Identifier (OMA-URI) 設定を構成する必要があります手動でします。 ユニバーサル デバイス管理の仕様 Apple、Android、および Windows の最新のデバイスをサポートする OMA デバイスの管理プロトコル (OMA-DM) を使用して、OMA Uri を構成します。 OMA DM 仕様に従って、限りと同じ方法で、MDM のすべての製品がこれらのオペレーティング システムと対話する必要があります。

Windows 10 には、多くの Csp が提供していますが、VPNv2 CSP を使用して、VPN クライアントを構成するこの展開に焦点を当てています。 VPNv2 CSP は、windows 10 の各 VPN プロファイル設定の構成を一意の CSP ノードを使用できます。 *ProfileXML*、すべての設定を構成することをという名前のノードは、VPNv2 CSP にも含まれている 1 つのノードではなく、個別にします。 ProfileXML について詳しくは、後でこの展開で「ProfileXML の概要」セクションを参照してください。 VPNv2 CSP の各ノードについて詳しくは、 [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp)を参照してください。



## 次のステップ

- [Always On VPN の高度な機能の一部について説明します](deploy/always-on-vpn-adv-options.md)

- [Always On VPN 展開の計画を開始する](deploy/always-on-vpn-deploy-deployment.md)


---

## 関連トピック
- [Microsoft サーバー ソフトウェアが Microsoft Azure の仮想マシンのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines): この記事では、Microsoft Azure の仮想マシン環境 (インフラストラクチャとして-サービス) で Microsoft サーバー ソフトウェアを実行するためのサポート ポリシーを説明します。

- [リモート アクセス](../../Remote-Access.md): このトピックでは、Windows Server 2016 では、リモート アクセス サーバーの役割の概要を説明します。

- [Windows 10 VPN テクニカル ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): このガイドによって、向けに決定する Windows 10 クライアント、エンタープライズ VPN ソリューションと展開を構成する方法について説明します。 このガイドでは、「VPNv2 Configuration Service Provider (CSP)」(VPNv2 構成サービス プロバイダー (CSP)) を参照しており、Microsoft Intune、および Windows 10 用の VPN プロファイル テンプレートを使用して、モバイル デバイス管理 (MDM) を構成する手順を示します。

- [コア ネットワーク ガイド](../../../../networking/core-network-guide/Core-Network-Guide.md): このガイドは、計画し、完全に機能しているネットワークと新しいフォレスト内の新しい Active Directory ドメインに必要な主要なコンポーネントを展開する方法について説明します。

- [ドメイン ネーム システム (DNS)](../../../../networking/dns/dns-top.md): このトピックでは、ドメイン ネーム システム (DNS) の概要を説明します。 Windows Server 2016 では、DNS とは、サーバー マネージャーまたは Windows PowerShell コマンドを使用してインストールできるサーバーの役割です。 新しい Active Directory フォレストとドメインをインストールする場合は DNS は Active Directory と共に、フォレストとドメインのグローバル カタログ サーバーとして自動的にインストールされます。 

- [Active Directory 証明書サービスの概要](https://technet.microsoft.com/library/hh831740.aspx): このドキュメントは、Active Directory 証明書サービス (AD CS) Windows Server® 2012 での概要を説明します。 AD CS は、公開キー基盤 (PKI) をビルドして、組織の公開キーの暗号化、デジタル証明書とデジタル署名の機能を提供することができるサーバーの役割です。

- [公開キー インフラストラクチャの設計ガイダンス](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx): この wiki 公開キー基盤 (Pki) の設計ガイダンスを紹介します。 PKI および証明機関 (CA) の階層を構成する前に、組織のセキュリティ ポリシーと証明書ことをお勧め書) があります。

- [AD CS ステップ バイ ステップ ガイド: 2 層 PKI 階層の展開](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx): このステップ バイ ステップ ガイドは、ラボ環境での Active Directory® 証明書サービス (AD CS) の基本的な構成を設定するために必要な手順を説明します。 Windows Server® 2008 R2 で AD CS では、公開キー テクノロジを用いるソフトウェア セキュリティ システムで使われる公開キー証明書を作成してカスタマイズ可能なサービスを提供します。

- [ネットワーク ポリシー サーバー (NPS)](../../../../networking/technologies/nps/nps-top.md): このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの概要を説明します。 ネットワーク ポリシー サーバー (NPS) を使用すると、接続要求の認証と承認を行うための組織全体のネットワーク アクセス ポリシーを作成して適用できます。 

---
