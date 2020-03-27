---
title: Windows Server および Windows 10 のための Always On VPN 展開
description: この展開を使用して、Windows Server 2016 以降のリモートアクセスを使用してリモート従業員用の仮想プライベートネットワーク (VPN) 接続 Always On を展開し、Windows 10 クライアントコンピューターの VPN プロファイルを Always On できます。
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 5ae1a40b-4f10-4ace-8aaf-13f7ab581f4f
ms.localizationpriority: medium
ms.date: 12/20/2018
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ca064f887a524c5f41b29837e8f8fec586a8d928
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313263"
---
# <a name="always-on-vpn-deployment-for-windows-server-and-windows-10"></a>Windows Server および Windows 10 用の VPN 展開の Always On

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** リモートアクセス](../../../Remote-Access.md)<br>
- [**次のようになります。** Always On VPN の機能について説明します。](../../vpn-map-da.md)

Always On VPN は、リモートアクセスのための単一の統合されたソリューションを提供し、ドメインに参加している、ドメインに参加していない (ワークグループ)、または Azure AD 参加しているデバイス (個人所有のデバイスも含む) をサポートします。 Always On VPN では、接続の種類がユーザーまたはデバイス専用である必要はなく、両方の組み合わせにすることができます。 たとえば、リモート デバイス管理用のデバイス認証を有効にし、会社の内部サイトとサービスへの接続に対するユーザー認証を有効にすることができます。

## <a name="prerequisites"></a>前提条件

多くの場合、Always On VPN の展開に使用できるテクノロジが展開されています。 DC/DNS サーバー以外の Always On VPN の展開には、NPS (RADIUS) サーバー、証明機関 (CA) サーバー、およびリモートアクセス (ルーティングと VPN) サーバーが必要です。 インフラストラクチャがセットアップされたら、クライアントを登録し、いくつかのネットワーク変更によってクライアントをオンプレミスに安全に接続する必要があります。

- Active Directory ドメインインフラストラクチャ (1 つ以上のドメインネームシステム (DNS) サーバーを含む)。 内部ゾーンと外部ドメインネームシステム (DNS) ゾーンの両方が必要です。これは、内部ゾーンが外部ゾーンの委任されたサブドメインであることを前提としています (たとえば、corp.contoso.com と contoso.com)。
- Active Directory ベースの公開キー基盤 (PKI) と Active Directory 証明書サービス (AD CS)。
- ネットワークポリシーサーバー (NPS) をインストールするサーバー (仮想または物理、既存または新規)。 ネットワーク上に既に NPS サーバーがある場合は、新しいサーバーを追加するのではなく、既存の NPS サーバー構成を変更することができます。
- IKEv2 VPN 接続と LAN ルーティングをサポートする機能の小さなサブセットを使用した RAS ゲートウェイ VPN サーバーとしてのリモートアクセス。
- 2つのファイアウォールを含む境界ネットワーク。  VPN と RADIUS 通信の両方が正常に機能するために必要なトラフィックがファイアウォールによって許可されていることを確認します。 詳細については、「 [ALWAYS ON VPN テクノロジの概要](../always-on-vpn-technology-overview.md)」を参照してください。
- 2つの物理イーサネットネットワークアダプターを使用する境界ネットワーク上の物理サーバーまたは仮想マシン (VM)。 RAS ゲートウェイ VPN サーバーとしてリモートアクセスをインストールします。 Vm には、ホストの仮想 LAN (VLAN) が必要です。 
- Administrators のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。
- 展開を実行する前に、このガイドの「計画」セクションを読んで、この展開の準備ができていることを確認してください。
- 使用する各テクノロジの設計と展開に関するガイドを確認します。 これらのガイドは、組織のネットワークに必要なサービスと構成が展開シナリオによって提供されるかどうかを判断するのに役立ちます。 詳細については、「 [ALWAYS ON VPN テクノロジの概要](../always-on-vpn-technology-overview.md)」を参照してください。
- CSP はベンダー固有ではないため、Always On VPN 構成を展開するために選択した管理プラットフォーム。

>[!IMPORTANT]
>この展開では、Active Directory Domain Services、Active Directory 証明書サービス、およびネットワークポリシーサーバーを実行しているコンピューターなどのインフラストラクチャサーバーが Windows Server 2016 を実行している必要はありません。 Windows server 2012 R2 など、以前のバージョンの Windows Server を、インフラストラクチャサーバーおよびリモートアクセスを実行しているサーバーに使用できます。
>
>Microsoft Azure の仮想マシン (VM) にリモートアクセスを展開しないでください。 リモートアクセス VPN と DirectAccess の両方を含め、Microsoft Azure でのリモートアクセスの使用はサポートされていません。 詳細については、「 [Microsoft Azure の仮想マシンに対する Microsoft サーバーソフトウェアのサポート](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines)」を参照してください。

## <a name="about-this-deployment"></a>この展開について

ここでは、Windows 10 を実行しているリモートクライアントコンピューター用に、次に示すシナリオのいずれかを使用して、ポイント対サイト VPN RAS ゲートウェイとしてリモートアクセスを展開する手順について説明します。 また、展開用の既存のインフラストラクチャの一部を変更するための手順も紹介します。 また、この展開全体で、VPN 接続プロセス、構成するサーバー、ProfileXML VPNv2 CSP ノード、および Always On VPN を展開するためのその他のテクノロジについての詳細情報を確認するためのリンクがあります。

**Always On VPN 展開シナリオ:**

1. VPN のみ Always On デプロイします。
2. Azure AD を使用して VPN 接続の条件付きアクセスを使用して Always On VPN をデプロイします。

表示されるシナリオの詳細とワークフローについては、「 [Deploy ALWAYS ON VPN](always-on-vpn-deploy-deployment.md)」を参照してください。

## <a name="what-isnt-provided-in-this-deployment"></a>この展開で提供されていないもの

この展開では、次の手順は使用できません。

- Active Directory Domain Services (AD DS)。
- Active Directory 証明書サービス (AD CS) と公開キー基盤 (PKI)。
- 動的ホスト構成プロトコル (DHCP)。
- イーサネットケーブル、ファイアウォール、スイッチ、ハブなどのネットワークハードウェア。
- リモートユーザーが Always On VPN 接続を介してアクセスできる、アプリケーションやファイルサーバーなどの追加のネットワークリソース。
- インターネット接続、または Azure AD を使用したインターネット接続のための条件付きアクセス。 詳細については、「 [Azure Active Directory での条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)」を参照してください。

## <a name="next-steps"></a>次のステップ:

- [Always On VPN の機能についての詳細情報](../../vpn-map-da.md)

- [Always On VPN の機能強化についての詳細情報](../always-on-vpn-enhancements.md)

- [いくつかの高度な Always On VPN 機能について説明します。](always-on-vpn-adv-options.md)

- [Always On VPN テクノロジについての詳細情報](../always-on-vpn-technology-overview.md)

- [Always On VPN 展開の計画を開始する](always-on-vpn-deploy-deployment.md)