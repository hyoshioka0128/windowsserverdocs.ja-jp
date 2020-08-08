---
title: Always On VPN の展開
description: このトピックでは、Windows Server 2016 で Always On VPN を展開するための詳細な手順について説明します。
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.openlocfilehash: 1ba1e31c743d986e777af26f9acee5ed8820515a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958270"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN の展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** Always On VPN の高度な機能について説明します。](always-on-vpn-adv-options.md)
- [**次のようになります。** 手順 1.Always On VPN 展開の計画を開始する](always-on-vpn-deploy-planning.md)

このセクションでは、リモートドメインに参加している Windows 10 クライアントコンピューターに対して Always On VPN 接続を展開するためのワークフローについて説明します。 VPN ユーザーがリソースにアクセスする方法を微調整するために**条件付きアクセスを構成**する場合は、「 [Azure AD を使用した Vpn 接続の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)」を参照してください。 Azure AD を使用した VPN 接続の条件付きアクセスの詳細については、 [Azure Active Directory での条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)に関するページを参照してください。

次の図は Always On VPN をデプロイする場合のさまざまなシナリオのワークフロープロセスを示しています。

[![Always On VPN 展開ワークフローのフローチャート](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png)

> [!IMPORTANT]
> この展開では、Active Directory Domain Services、Active Directory 証明書サービス、およびネットワークポリシーサーバーを実行しているコンピューターなどのインフラストラクチャサーバーが Windows Server 2016 を実行している必要はありません。 Windows server 2012 R2 など、以前のバージョンの Windows Server を、インフラストラクチャサーバーおよびリモートアクセスを実行しているサーバーに使用できます。

## <a name="step-1-plan-the-always-on-vpn-deployment"></a>[手順 1.Always On VPN 展開を計画する](always-on-vpn-deploy-planning.md)

この手順では、Always On VPN 展開の計画と準備を開始します。 を VPN サーバーとして使用する予定のコンピューターにリモートアクセスサーバーの役割をインストールする前に、 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。

## <a name="step-2-configure-the-always-on-vpn-server-infrastructure"></a>[手順 2.Always On VPN サーバー インフラストラクチャを構成する](vpn-deploy-server-infrastructure.md)

この手順では、VPN をサポートするために必要なサーバー側コンポーネントをインストールして構成します。 サーバー側のコンポーネントには、ユーザー、VPN サーバー、および NPS サーバーによって使用される証明書を配布するように PKI を構成することが含まれます。  また、IKEv2 接続をサポートするように RRAS を構成し、VPN 接続の承認を実行するために NPS サーバーを構成します。

サーバーインフラストラクチャを構成するには、次のタスクを実行する必要があります。

- **Active Directory Domain Services で構成されたサーバーの場合:** コンピューターとユーザーの両方についてグループポリシーで証明書の自動登録を有効にし、VPN ユーザーグループ、VPN サーバーグループ、および NPS サーバーグループを作成して、各グループにメンバーを追加します。
- **Active Directory 証明書サーバーの CA:** ユーザー認証、VPN サーバー認証、および NPS サーバー認証証明書テンプレートを作成します。
- **ドメインに参加している Windows 10 クライアントの場合:** ユーザー証明書を登録および検証します。

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>[手順 3.Always On VPN 用にリモート アクセス サーバーを構成する](vpn-deploy-ras.md)

この手順では、IKEv2 VPN 接続を許可するようにリモートアクセス VPN を構成し、他の VPN プロトコルからの接続を拒否して、承認された VPN クライアントに接続するために IP アドレスを発行するための静的 IP アドレスプールを割り当てます。

RAS を構成するには、次のタスクを実行する必要があります。

- VPN サーバー証明書の登録と検証
- リモートアクセス VPN のインストールと構成

## <a name="step-4-install-and-configure-the-nps-server"></a>[手順 4.NPS サーバーをインストールして構成する](vpn-deploy-nps.md)

この手順では、Windows PowerShell またはサーバーマネージャーの役割と機能の追加ウィザードを使用して、ネットワークポリシーサーバー (NPS) をインストールします。 また、NPS が VPN サーバーから受信する接続要求のすべての認証、承認、およびアカウンティングの各作業を処理するように構成します。

NPS を構成するには、次のタスクを実行する必要があります。

- Active Directory に NPS サーバーを登録する
- NPS サーバーの RADIUS アカウンティングを構成する
- NPS で VPN サーバーを RADIUS クライアントとして追加する
- NPS でネットワークポリシーを構成する
- NPS サーバー証明書を自動登録する

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpn"></a>[手順 5.Always On VPN の DNS とファイアウォールの設定を構成する](vpn-deploy-dns-firewall.md)

この手順では、DNS とファイアウォールの設定を構成します。 リモート VPN クライアントは、接続するときに、内部のクライアントが使用しているのと同じ DNS サーバーを使用します。これにより、内部ワークステーションの他の部分と同じ方法で名前を解決できます。

## <a name="step-6-configure-windows-10-client-always-on-vpn-connections"></a>[手順 6.Windows 10 クライアントの Always On VPN 接続を構成する](vpn-deploy-client-vpn-connections.md)

この手順では、VPN 接続を使用して、そのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成します。 Windows PowerShell、Microsoft Endpoint Configuration Manager、Intune などの Windows 10 VPN クライアントを構成するには、いくつかのテクノロジを使用できます。 3つすべてに、適切な VPN 設定を構成するための XML VPN プロファイルが必要です。

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivity"></a>[手順 7.OptionalVPN 接続の条件付きアクセスの構成](../../ad-ca-vpn-connectivity-windows10.md)

この省略可能な手順では、承認された VPN ユーザーがリソースにアクセスする方法を微調整できます。 VPN 接続に Azure AD 条件付きアクセスを使用すると、VPN 接続を保護することができます。 条件付きアクセスは、ポリシーベースの評価エンジンであり、Azure AD 接続されたアプリケーションに対するアクセス規則を作成できます。 詳細については、「 [Azure Active Directory (Azure AD) 条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)」を参照してください。

## <a name="next-step"></a>次のステップ

[手順 1.Vpn 展開の Always On を計画](always-on-vpn-deploy-planning.md)する: vpn サーバーとして使用する予定のコンピューターにリモートアクセスサーバーの役割をインストールする前に、次のようにします。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。
