---
title: 仮想プライベート ネットワーク (VPN)
description: このトピックを使用すると、Windows Server 2016 および Windows 10 VPN 機能と機能について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bfd00b7a13e9fad113da1191e7ccd33965223070
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749553"
---
# <a name="virtual-private-networking-vpn"></a>仮想プライベート ネットワーク (VPN)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>1 つのテナントの VPN サーバーとしての RAS ゲートウェイ

Windows Server 2016 でリモート アクセス サーバーの役割は、次の関連するネットワーク アクセス テクノロジの論理グループです。

- リモート アクセス サービス (RAS)
- ルーティング
- Web アプリケーション プロキシ

これらのテクノロジは、リモート アクセス サーバーの役割の役割サービスです。

追加の役割と機能のウィザードまたは Windows PowerShell のリモート アクセス サーバーの役割をインストールするときに、これらの 3 つの役割サービスの 1 つ以上をインストールできます。

インストールするときに、 **DirectAccess と VPN (RAS)** 役割サービス、リモート アクセス サービスのゲートウェイを展開する (**RAS ゲートウェイ**)。 RAS ゲートウェイは、拡張機能と拡張機能の多くを提供する 1 つのテナント RAS ゲートウェイの仮想プライベート ネットワーク (VPN) サーバーとしてデプロイできます。

>[!NOTE]
>ソフトウェア定義ネットワーク (SDN) を使用するマルチ テナント VPN サーバーとして、または DirectAccess サーバーとしては、RAS ゲートウェイをデプロイすることもできます。 詳細については、次を参照してください。 [RAS ゲートウェイ](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway)、[ソフトウェア定義ネットワーク (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)、および[DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)します。

## <a name="related-topics"></a>関連トピック
- [Always On VPN 機能と機能](vpn-map-da.md):このトピックでは、Always On VPN の機能について説明します。 

- [Windows 10 デバイスの VPN トンネルを構成する](vpn-device-tunnel-config.md):Always On VPN では、デバイスまたはコンピューターの専用の VPN プロファイルを作成する機能を提供します。 Always On VPN 接続には、トンネルの 2 つの種類:_デバイス トンネル_と_ユーザー トンネル_します。 デバイスのトンネルは、ログオン前の接続のシナリオとデバイス管理のために使用されます。 ユーザー トンネルでは、VPN サーバーを組織のリソースにアクセスすることができます。

- [Windows Server 2016 および Windows 10 の VPN の展開の always On](always-on-vpn/deploy/always-on-vpn-deploy.md):ポイント対サイト VPN 接続、リモートの従業員に Always On VPN 接続を持つ組織のネットワークに接続できるようにするための 1 つのテナント RAS ゲートウェイの VPN とリモート アクセスの展開について説明します。 この展開で使用されているテクノロジのそれぞれの設計と展開のガイドを確認することをお勧めします。

- [Windows 10 の VPN に関するテクニカル ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide):社内の VPN ソリューションでの Windows 10 クライアントと、展開を構成する方法が決定を示します。 VPNv2 構成サービス プロバイダー (CSP) への参照を見つけることができ、モバイル デバイス管理 (MDM) の構成手順が Windows 10 用 Microsoft Intune と VPN プロファイルのテンプレートを使用してを提供します。

- [System Center Configuration Manager での作成の VPN プロファイル方法](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles):このトピックでは、System Center Configuration Manager (SCCM) での VPN プロファイルを作成する方法について説明します。

- [VPN 接続で常に Windows 10 クライアントを構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):このトピックで説明、それを ProfileXML オプションとスキーマ、およびそれを ProfileXML VPN を作成する方法。 サーバー インフラストラクチャを設定した後は、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成する必要があります。

- [VPN プロファイルのオプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options):このトピックでは、Windows 10 で VPN プロファイルの設定について説明し、Intune、SCCM を使用して VPN プロファイルを構成する方法について説明します。 VPNv2 CSP でそれを ProfileXML ノードを使用して Windows 10 では、すべての VPN 設定を構成できます。
