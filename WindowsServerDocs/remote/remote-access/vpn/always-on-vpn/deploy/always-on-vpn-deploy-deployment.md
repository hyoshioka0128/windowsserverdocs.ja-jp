---
title: Always On VPN の展開
description: このトピックでは、Always On VPN では、Windows Server 2016 の展開について詳しく説明します。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 15c60f2986d3837c5c6e03f9e0a25c7e0a4e0cc0
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067328"
---
# Always On VPN の展開

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #0171 です。[**前:** 、Always On VPN の機能の詳細について説明します](always-on-vpn-adv-options.md)<br>
& #0187 です。[ **[次へ]:** 手順 1 です。Always On VPN 展開の計画開始](always-on-vpn-deploy-planning.md)

このセクションでは、リモート Windows 10 クライアント コンピューターをドメインに参加しているため、Always On VPN の接続を展開するためのワークフローについて説明します。 VPN ユーザー リソースにアクセスする方法を微調整する**条件付きアクセス**を構成する場合は、 [Azure AD を使用して VPN 接続の条件付きアクセス](../../ad-ca-vpn-connectivity-windows10.md)を参照してください。 Azure AD を使用して VPN 接続の条件付きアクセスについて詳しくは、 [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を参照してください。 


次の図は、Always On VPN を展開する際のさまざまなシナリオのワークフロー プロセスを示しています。 

_クリックして拡大_します。

<a href="../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow.png" alt="Full-sized view of the Always On VPN deployment workflow" target="_blank">![thumbnail](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)
</a> 

>[!IMPORTANT]
>この展開が必須ではありません Active Directory Domain Services、Active Directory 証明書サービス、およびネットワーク ポリシー サーバーを実行しているコンピューターなど、インフラストラクチャ サーバーが Windows Server 2016 を実行していること。 インフラストラクチャ サーバーとリモート アクセスを実行しているサーバーなど、Windows Server 2012 R2、Windows Server の以前のバージョンを使用することができます。

## [手順 1.  Always On VPN 展開を計画する](always-on-vpn-deploy-planning.md)

この手順では、計画し、Always On VPN 展開の準備を開始します。 コンピューターのリモート アクセス サーバーの役割をインストールする前に、VPN サーバーとして使用を計画しています。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。

## [手順 2.  Always On VPN サーバー インフラストラクチャを構成する](vpn-deploy-server-infrastructure.md)

この手順では、インストールして、VPN をサポートするために必要なサーバー側のコンポーネントを構成します。 サーバー側のコンポーネントには、ユーザー、VPN サーバー、および NPS サーバーによって使用される証明書を配布するための PKI の構成が含まれます。  また、IKEv2 接続および VPN 接続の認証を実行する NPS サーバーをサポートするために RRAS を構成します。

サーバー インフラストラクチャを構成するには、次のタスクを行う必要があります。
- **Active Directory ドメイン サービスで構成されているサーバーで:** コンピューターとユーザーの両方のグループ ポリシーで証明書の自動登録を有効にする、VPN のユーザー グループ、VPN サーバー グループで、および、NPS サーバー グループを作成し、各グループにメンバーを追加します。
- **Active Directory 証明書サーバー CA で:** ユーザーの認証、VPN サーバー認証、および NPS サーバー認証証明書テンプレートを作成します。
- **ドメインに参加している Windows 10 クライアントで:** 登録し、ユーザーの証明書を検証します。

## [手順 3.  Always On VPN 用にリモート アクセス サーバーを構成する](vpn-deploy-ras.md)

この手順では、その他の VPN プロトコルからの接続を拒否、承認された VPN クライアントが接続している IP アドレスの発行の静的 IP アドレス プールを割り当てる IKEv2 VPN 接続を許可するリモート アクセス VPN を構成します。

RAS を構成するには、次のタスクを行う必要があります。
- 登録し、VPN サーバーの証明書の検証
- インストールし、リモート アクセス VPN の構成

## [手順 4.  サーバーに NPS サーバーをインストールして構成する](vpn-deploy-nps.md)

この手順では、Windows PowerShell またはサーバー マネージャーの役割の追加と機能の削除ウィザードのいずれかを使用してネットワーク ポリシー サーバー (NPS) をインストールします。 すべての認証、承認、および VPN サーバーから受信接続要求の会計職務を処理するように NPS を構成します。

NPS を構成するには、次のタスクを行う必要があります。
- Active Directory に NPS サーバーを登録します。
- RADIUS アカウンティング NPS サーバーを構成します。
- Nps を RADIUS クライアントとして、VPN サーバーを追加します。
- NPS でのネットワーク ポリシーを構成します。
- NPS サーバー証明書の自動登録

## [手順 5.  VPN で常に DNS およびのファイアウォール設定を構成します。](vpn-deploy-dns-firewall.md)

DNS とファイアウォールを構成する、この手順で設定します。 リモート VPN クライアントが接続を使用、内部のクライアントを使用して、同じの DNS サーバー、内部のワークステーションの残りの部分と同じ方法で名前を解決するようにします。 

## [手順 6.  Windows 10 クライアントの Always On VPN 接続を構成する](vpn-deploy-client-vpn-connections.md)

この手順では、VPN 接続を使用して、そのインフラストラクチャとの通信に windows 10 クライアント コンピューターを構成します。 Windows PowerShell、System Center Configuration Manager、Intune など、windows 10 VPN クライアントを構成するのには、いくつかのテクノロジを使用できます。 3 つすべてが適切な VPN 設定を構成する XML の VPN プロファイルが必要です。 

## [手順 7.  (省略可能)VPN 接続の条件付きアクセスを構成します。](../../ad-ca-vpn-connectivity-windows10.md) 
このオプションの手順では、VPN を承認する方法を微調整できますユーザー リソースにアクセスします。 VPN 接続の条件付きアクセスを Azure AD、VPN 接続を保護できます。 条件付きアクセスは、アプリケーションができるように、Azure AD のアクセス規則を作成するため、ポリシー ベースの評価エンジンに接続されています。 詳細については、 [Azure Active Directory (Azure AD) の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を参照してください。


## 次の手順
手順 1 を[します。Always On VPN 展開を計画する](always-on-vpn-deploy-planning.md): VPN サーバーとして使用を計画しているコンピューターで、リモート アクセス サーバーの役割をインストールする前にします。 適切な計画の後で、Always On VPN を展開し、必要に応じて Azure AD を使用して VPN 接続の条件付きアクセスを構成します。  



---