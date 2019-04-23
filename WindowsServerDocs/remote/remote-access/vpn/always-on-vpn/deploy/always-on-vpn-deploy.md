---
title: Windows Server および Windows 10 のための Always On VPN 展開
description: この展開を使用して、Windows 10 クライアント コンピューターの Windows Server 2016 以降のリモート アクセスと Always On VPN プロファイルを使用してリモートの社員を常に仮想プライベート ネットワーク (VPN) 接続を展開することができます。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb60bdc6d6f3ff074f04827aa95c9e8e8abf35b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859623"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Windows Server および Windows 10 の always On VPN 展開

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

&#171;  [**先の：** リモート アクセス](../../../Remote-Access.md)<br>
&#187;[ **[次へ]。** Always On VPN 機能と機能について説明します](../../vpn-map-da.md)


Always On VPN リモート アクセスをサポートするドメインに参加している 1 つのまとまりのあるソリューション、非ドメインに参加している (ワークグループ)、または Azure AD に参加してデバイスも個人所有のデバイスを提供します。  Always On VPN、接続の種類がユーザーまたはデバイスのみにする必要はありませんが、両方の組み合わせを指定できます。 など、リモート デバイスの管理用のデバイス認証を有効にし、会社の内部サイトとサービスへの接続をユーザーの認証を有効に可能性があります。



## <a name="prerequisites"></a>前提条件

テクノロジがある可能性が最も高いデプロイ Always On VPN の展開を行えます。 NPS (RADIUS) サーバー、証明機関 (CA) サーバー、およびリモート アクセス (ルーティング VPN) サーバー、DC/DNS サーバー以外、Always On VPN 展開が必要です。 インフラストラクチャを設定すると、クライアントの登録し、経由でオンプレミスに安全にいくつかのネットワークの変更をクライアントを接続する必要があります。

- Active Directory ドメイン インフラストラクチャ、1 つまたは複数のドメイン ネーム システム (DNS) サーバーを含むです。 内部および外部の両方のドメイン ネーム システム (DNS) ゾーンが必要な場合は、内部のゾーン (たとえば、corp.contoso.com と contoso.com など) は、外部のゾーンの委任されたサブドメインであることを想定しています。
- Active Directory による公開キー基盤 (PKI) と Active Directory 証明書サービス (AD CS)。
- サーバー、仮想または物理、既存または新規、ネットワーク ポリシー サーバー (NPS) をインストールします。 ネットワーク上の NPS サーバーを既にがある場合は、新しいサーバーを追加なくに、既存の NPS サーバーの構成を変更します。
- IKEv2 VPN 接続と LAN ルーティングをサポートする機能の小さなサブセットを持つ RAS ゲートウェイの VPN サーバーとしてリモート アクセスします。
- 2 つのファイアウォールを含む境界ネットワーク。  ファイアウォールが適切に機能する VPN、RADIUS の両方の通信に必要なトラフィックを許可することを確認します。 詳細については、次を参照してください。 [VPN 技術概要で常に](../always-on-vpn-technology-overview.md)します。
- 物理サーバーまたはリモート アクセスを RAS ゲートウェイの VPN サーバーとしてインストールする物理イーサネット ネットワーク アダプターが 2 つ、境界ネットワーク上の仮想マシン (VM)。 Vm では、ホストの仮想 LAN (VLAN) が必要です。 
- 管理者、またはそれと同等のメンバーシップは、最低限必要です。
- 展開を実行する前にこの展開する準備は、このガイドの計画セクションを参照します。
- 使用されているテクノロジのそれぞれの設計と展開のガイドを確認します。 これらのガイドでは、展開シナリオが、サービスと、組織のネットワークに必要な構成を提供するかどうかを判断できます。 詳細については、次を参照してください。 [VPN 技術概要で常に](../always-on-vpn-technology-overview.md)します。
- CSP は、ベンダー固有ではないため、Always On VPN 構成をデプロイするため、任意の管理プラットフォームです。


>[!IMPORTANT]
>この展開では、Active Directory Domain Services、Active Directory 証明書サービス、およびネットワーク ポリシー サーバーを実行しているコンピューターなど、インフラストラクチャ サーバーが Windows Server 2016 を実行していることを要件が違います。 インフラストラクチャ サーバーとリモート アクセスを実行しているサーバーの以前のバージョンの Windows Server、Windows Server 2012 R2 などを使用することができます。
>
>仮想マシンにリモート アクセスの展開をしないで\(VM\) Microsoft Azure でします。 Microsoft Azure でのリモート アクセスの使用はサポートされていません、リモート アクセス VPN と DirectAccess の両方を含むです。 詳細については、次を参照してください。 [Microsoft Azure 仮想マシンのマイクロソフト サーバー ソフトウェア サポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)します。


## <a name="bkmk_about"></a>この展開について

指示のポイントの 1 つのテナント RAS ゲートウェイの VPN とリモート アクセスの展開手順\-に\-サイトの Windows を実行しているリモート クライアント コンピューターについて以下に説明したシナリオのいずれかを使用して、VPN 接続10。 既存のインフラストラクチャのデプロイの一部を変更する手順についても表示されます。 またこの展開では、全体に VPN 接続のプロセス、構成するサーバーをそれを ProfileXML VPNv2 CSP ノード、および Always On VPN を展開するには、その他のテクノロジの詳細について役立つリンクがあります。

**Always On VPN 展開シナリオ:**

1. 常を展開 VPN のみです。
2. Azure AD を使用して VPN 接続用の条件付きアクセスには、Always On VPN をデプロイします。


詳細と、シナリオのワークフローは、次を参照してください。[デプロイ Always On VPN](always-on-vpn-deploy-deployment.md)します。


## <a name="bkmk_not"></a>この展開で何が指定されていません。

このデプロイは、手順を提供しません。

- Active Directory Domain Services \(AD DS\)します。
- Active Directory 証明書サービス\(AD CS\)および公開キー基盤\(PKI\)します。
- 動的ホスト構成プロトコル\(DHCP\)します。 
- イーサネット ケーブルの接続、ファイアウォール、スイッチ、およびハブなどのハードウェアをネットワークします。
- Always On VPN 接続経由でリモート ユーザーがアクセスできるアプリケーションおよびファイル サーバーなどの追加のネットワーク リソース。
- インターネット接続または Azure AD を使用してインターネット接続の条件付きアクセス。 詳細については、次を参照してください。 [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)します。




## <a name="next-steps"></a>次のステップ

- [Always On VPN 機能と機能の詳細について説明します](../../vpn-map-da.md)

- [Always On VPN の機能強化についての詳細します。](../always-on-vpn-enhancements.md)

- [高度な Always On VPN 機能の一部について説明します](always-on-vpn-adv-options.md)

- [Always On VPN テクノロジについて詳しく説明します](../always-on-vpn-technology-overview.md)

- [Always On VPN 展開の計画を開始します。](always-on-vpn-deploy-deployment.md)


---
