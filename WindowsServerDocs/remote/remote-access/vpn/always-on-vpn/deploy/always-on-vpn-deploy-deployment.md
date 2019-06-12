---
title: Always On VPN の展開
description: このトピックでは、Always On VPN では、Windows Server 2016 を展開するための詳細な手順を説明します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6849d8547885b10fb32a133f09a82b6f133a535e
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749656"
---
# <a name="deploy-always-on-vpn"></a>Always On VPN の展開

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** Always On VPN 機能の詳細について説明します](always-on-vpn-adv-options.md)
- [**次に：** 手順 1.Always On VPN 展開の計画を開始します。](always-on-vpn-deploy-planning.md)

このセクションでは、ドメインに参加している Windows 10 のクライアント コンピューターをリモートの Always On VPN 接続の展開のワークフローについて説明します。 たい場合**条件付きアクセスを構成する**VPN ユーザーがリソースにアクセスする方法を微調整するには、次を参照してください。 [Azure AD を使用して VPN 接続用の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)します。 Azure AD を使用して VPN 接続用の条件付きアクセスの詳細については、次を参照してください。 [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)します。 

Always On VPN をデプロイするときに、次の図は、さまざまなシナリオのワークフロー プロセスを示します。

![Always On VPN 展開のワークフローのフロー チャート](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)

>[!IMPORTANT]
>この展開では、Active Directory Domain Services、Active Directory 証明書サービス、およびネットワーク ポリシー サーバーを実行しているコンピューターなど、インフラストラクチャ サーバーが Windows Server 2016 を実行していることを要件が違います。 インフラストラクチャ サーバーとリモート アクセスを実行しているサーバーの以前のバージョンの Windows Server、Windows Server 2012 R2 などを使用することができます。

## <a name="step-1-plan-the-always-on-vpn-deploymentalways-on-vpn-deploy-planningmd"></a>[手順 1.Always On VPN 展開を計画する](always-on-vpn-deploy-planning.md)

この手順では、計画し、Always On VPN 展開の準備を開始します。 コンピューターのリモート アクセス サーバーの役割をインストールする前に、VPN サーバーとして使用する計画しています。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。

## <a name="step-2-configure-the-always-on-vpn-server-infrastructurevpn-deploy-server-infrastructuremd"></a>[手順 2.Always On VPN サーバー インフラストラクチャを構成する](vpn-deploy-server-infrastructure.md)

この手順では、インストールし、VPN をサポートするために必要なサーバー側コンポーネントを構成します。 サーバー側コンポーネントには、ユーザー、VPN サーバー、および NPS サーバーで使用される証明書を配布するための PKI の構成が含まれます。  またの IKEv2 接続と VPN 接続の承認を実行する NPS サーバーをサポートするように RRAS を構成します。

サーバー インフラストラクチャを構成するには、次のタスクを実行する必要があります。

- **Active Directory Domain Services で構成されているサーバー。** コンピューターとユーザーの両方のグループ ポリシーで証明書の自動登録を有効にする、VPN ユーザー グループ、VPN サーバーのグループ、および、NPS サーバーのグループを作成し、各グループにメンバーを追加します。
- **Active Directory 証明書サーバー CA の場合は。** ユーザー認証、VPN サーバーの認証、および NPS サーバー認証証明書テンプレートを作成します。
- **ドメインに参加している Windows 10 クライアント。** 登録して、ユーザー証明書を検証します。

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpnvpn-deploy-rasmd"></a>[手順 3.Always On VPN 用にリモート アクセス サーバーを構成する](vpn-deploy-ras.md)

この手順では、IKEv2 VPN 接続を許可する、その他の VPN プロトコルからの接続を拒否、および承認済みの VPN クライアントの接続を IP アドレスの発行のための静的 IP アドレス プールを割り当てのリモート アクセス VPN を構成します。

RAS で構成するには、次のタスクを実行する必要があります。

- 登録して、VPN サーバーの証明書の検証
- インストールし、リモート アクセス VPN の構成

## <a name="step-4-install-and-configure-the-nps-servervpn-deploy-npsmd"></a>[手順 4.NPS サーバーをインストールして構成する](vpn-deploy-nps.md)

この手順では、Windows PowerShell またはサーバー マネージャーの役割の追加と機能のウィザードのいずれかを使用してネットワーク ポリシー サーバー (NPS) をインストールします。 また、すべての認証、承認、およびアカウンティングの職務の VPN サーバーから受信した接続要求を処理するために NPS を構成します。

NPS を構成するには、次のタスクを実行する必要があります。

- Active Directory での NPS サーバーを登録します。
- RADIUS NPS サーバーのアカウンティングを構成します。
- VPN サーバーを NPS を RADIUS クライアントとして追加します。
- NPS でネットワーク ポリシーを構成します。
- NPS サーバー証明書を自動登録

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpnvpn-deploy-dns-firewallmd"></a>[手順 5.VPN で常に DNS とファイアウォール設定を構成します。](vpn-deploy-dns-firewall.md)

DNS とファイアウォールを構成するこの手順で設定します。 リモート VPN クライアントが、接続を使用、内部クライアントを使用して、同じ DNS サーバー名を内部のワークステーションの残りの部分と同じ方法で解決できます。 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connectionsvpn-deploy-client-vpn-connectionsmd"></a>[手順 6.Windows 10 クライアントの Always On VPN 接続を構成する](vpn-deploy-client-vpn-connections.md)

この手順では、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成します。 いくつかのテクノロジを使用して、Windows PowerShell、System Center Configuration Manager では、Intune などの Windows 10 の VPN クライアントを構成することができます。 3 つすべては、XML の VPN プロファイルを適切な VPN 設定を構成する必要があります。

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivityad-ca-vpn-connectivity-windows10md"></a>[手順 7.(省略可能)VPN 接続用の条件付きアクセスを構成します。](../../ad-ca-vpn-connectivity-windows10.md)

この省略可能な手順では、どの承認済みの VPN を微調整できますユーザー リソースにアクセスします。 VPN 接続用の Azure AD 条件付きアクセス、VPN 接続を保護できます。 条件付きアクセスは、任意の Azure AD のアクセス規則を作成することができます、評価のポリシー ベースのエンジンに接続しているアプリケーションです。 詳細については、次を参照してください。 [Azure Active Directory (Azure AD) の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)します。

## <a name="next-step"></a>次の手順

[手順 1.Always On VPN 展開の計画](always-on-vpn-deploy-planning.md):コンピューターのリモート アクセス サーバーの役割をインストールする前に、VPN サーバーとして使用する計画しています。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。  
