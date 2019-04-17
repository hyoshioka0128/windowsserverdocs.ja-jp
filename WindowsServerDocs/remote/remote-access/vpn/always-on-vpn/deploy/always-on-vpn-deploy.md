---
title: Windows Server および Windows 10 のための Always On VPN 展開
description: この展開を使用すると、windows 10 クライアント コンピューターは Windows Server 2016 以降のリモート アクセスと Always On VPN プロファイルを使用してリモートの従業員に常に仮想プライベート ネットワーク (VPN) 接続を展開します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb60bdc6d6f3ff074f04827aa95c9e8e8abf35b
ms.sourcegitcommit: c435f91ef6f3ff5ffd2661291264b939d5ce4e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2018
ms.locfileid: "8981132"
---
# Windows Server および Windows 10 向けの always On VPN の展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** リモート アクセス](../../../Remote-Access.md)<br>
& #187 です。[ **[次へ]:** Always On VPN の機能や機能について説明します](../../vpn-map-da.md)


Always On VPN では、リモート アクセスおよびサポートしているドメインに参加している 1 つのまとまりのあるソリューション、ドメインに参加していない (ワークグループ)、または Azure AD に参加しているデバイスも個人所有のデバイスを提供します。  Always On VPN で接続の種類がユーザーまたはデバイスのみにする必要はありませんが、両方の組み合わせをすることができます。 たとえば、リモート デバイスの管理、デバイスの認証を有効にし、会社の内部サイトとサービスへの接続ユーザー認証を有効にする可能性があります。



## 前提条件

テクノロジがある可能性が最も高い Always On VPN の展開に使用できるを展開します。 Always On VPN 展開には、DC/DNS サーバー以外 NPS (RADIUS) サーバー、証明機関 (CA) サーバー、およびリモート アクセス (ルーティング/VPN) サーバーが必要です。 インフラストラクチャを設定するは、クライアントの登録し、オンプレミス ネットワークのいくつかの変更を安全にクライアントを接続する必要があります。

- Active Directory ドメインなどのインフラストラクチャに 1 つまたは複数のドメイン ネーム システム (DNS) サーバー。 内部および外部の両方のドメイン ネーム システム (DNS) ゾーンが必要な場合は、内部のゾーンされる委任された外部ゾーン (たとえば、corp.contoso.com、contoso.com) のサブドメインを想定しています。
- Active Directory に基づく公開キー基盤 (PKI) と Active Directory 証明書サービス (AD CS)。
- サーバー、仮想または物理、既存または新しい、ネットワーク ポリシー サーバー (NPS) をインストールします。 ネットワーク上の NPS サーバーを既にがある場合は、新しいサーバーを追加なくに、既存の NPS サーバー構成の変更します。
- IKEv2 VPN 接続および LAN ルーティングをサポートする機能の小さなサブセットを持つ RAS ゲートウェイの VPN サーバーとしてのリモート アクセスします。
- 2 つのファイアウォールを含む境界ネットワーク。  ファイアウォールが正常に機能する VPN と RADIUS の両方の通信に必要なトラフィックを許可することを確認します。 詳細については、 [Always On VPN テクノロジの概要](../always-on-vpn-technology-overview.md)を参照してください。
- 物理サーバーや境界ネットワーク上にリモート アクセス RAS ゲートウェイの VPN サーバーとしてインストールする物理イーサネット ネットワーク アダプターが 2 つの仮想マシン (VM)。 Vm では、ホストの仮想 LAN (VLAN) が必要です。 
- 管理者、またはそれと同等のメンバーシップは、最低限必要です。
- 展開を実行する前にこの展開する準備を確認するには、このガイドの計画のセクションをご覧ください。
- 各使用されるテクノロジの設計と展開ガイドを確認します。 これらのガイドは、展開シナリオが、サービスと、組織のネットワークに必要な構成を提供するかどうかを判断するのに役立ちます。 詳細については、 [Always On VPN テクノロジの概要](../always-on-vpn-technology-overview.md)を参照してください。
- CSP はベンダーに固有ではないために、Always On VPN の構成を展開するため、任意の管理プラットフォームです。


>[!IMPORTANT]
>この展開に必須ではありません Active Directory ドメイン サービス、Active Directory 証明書サービス、およびネットワーク ポリシー サーバーを実行しているコンピューターなど、インフラストラクチャ サーバーが Windows Server 2016 を実行していること。 インフラストラクチャ サーバーとリモート アクセスを実行しているサーバーの以前のバージョンの Windows Server 2012 R2 などの Windows Server を使用することができます。
>
>仮想マシンでのリモート アクセスの展開をしないで Microsoft Azure で \(VM\) します。 Microsoft Azure でのリモート アクセスの使用はサポートされていません、リモート アクセス VPN と DirectAccess の両方を含みます。 詳細については、 [Microsoft サーバー ソフトウェアが Microsoft Azure の仮想マシンに対するサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)を参照してください。


## <a name="bkmk_about"></a>この展開について

表示される指示には、1 つテナントとして VPN RAS ゲートウェイのサイト to\ 半の VPN 接続では、以下には、Windows 10 を実行しているリモート クライアント コンピューターに説明したシナリオのいずれかを使用してリモート アクセスの展開について説明します。 既存のインフラストラクチャの展開の一部を変更するための手順を見つけることもできます。 この展開全体では、VPN 接続のプロセス、サーバーを構成する、ProfileXML VPNv2 CSP ノード、および Always On VPN を展開するには、その他のテクノロジについて詳しく知るに役立つリンクを確認します。

**Always On VPN 展開シナリオの場合:**

1. Always On VPN の展開だけです。
2. Azure AD を使用して VPN 接続の条件付きアクセス Always On VPN を展開します。


詳細と提示されたシナリオのワークフローは、[展開 Always On VPN](always-on-vpn-deploy-deployment.md)を参照してください。


## <a name="bkmk_not"></a>この展開で何が指定されていません。

この展開はための手順を提供しません。

- Active Directory ドメイン サービス \(AD DS\) します。
- Active Directory 証明書サービスの \(AD CS\) と公開キー基盤 \(PKI\) します。
- 動的ホスト構成プロトコル \(DHCP\) します。 
- ネットワーク ケーブル、ファイアウォール、スイッチ、およびハブなどのハードウェア。
- Always On VPN 接続経由でリモート ユーザーがアクセスできるようにするアプリケーションとファイル サーバーなどの追加のネットワーク リソースです。
- インターネット接続や Azure AD を使用してインターネット接続の条件付きアクセスします。 詳細については、 [Azure Active Directory でアクセスする条件](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を参照してください。




## 次のステップ

- [Always On VPN の機能と機能について詳しく知る](../../vpn-map-da.md)

- [Always On VPN の機能強化について詳しく知る](../always-on-vpn-enhancements.md)

- [Always On VPN の高度な機能の一部について説明します](always-on-vpn-adv-options.md)

- [Always On VPN テクノロジの詳細の確認](../always-on-vpn-technology-overview.md)

- [Always On VPN 展開の計画を開始する](always-on-vpn-deploy-deployment.md)


---
