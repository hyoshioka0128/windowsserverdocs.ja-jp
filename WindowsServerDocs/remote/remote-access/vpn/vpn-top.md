---
title: 仮想プライベート ネットワーク (VPN)
description: このトピックでは、Windows Server 2016 と Windows 10 VPN の機能について説明します。
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 30f08f02bf7a06619b9a32206863a9ddefc0fc2d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968919"
---
# <a name="virtual-private-networking-vpn"></a>仮想プライベート ネットワーク (VPN)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>シングルテナント VPN サーバーとしての RAS ゲートウェイ

Windows Server 2016 では、リモートアクセスサーバーの役割は、次の関連するネットワークアクセステクノロジを論理的にグループ化したものです。

- リモートアクセスサービス (RAS)
- ルーティング
- Web アプリケーション プロキシ

これらのテクノロジは、リモート アクセス サーバーの役割の役割サービスです。

役割と機能の追加ウィザードまたは Windows PowerShell を使用してリモートアクセスサーバーの役割をインストールする場合は、これら3つの役割サービスの1つまたは複数をインストールできます。

**DirectAccess および VPN (ras)** 役割サービスをインストールすると、リモートアクセスサービスゲートウェイ (**ras ゲートウェイ**) が展開されます。 RAS ゲートウェイは、多数の高度な機能と拡張機能を提供する単一のテナント RAS ゲートウェイ仮想プライベートネットワーク (VPN) サーバーとして展開できます。

>[!NOTE]
>ソフトウェア定義ネットワーク (SDN) で使用するマルチテナント VPN サーバーとして、または DirectAccess サーバーとして RAS ゲートウェイを展開することもできます。 詳細については、「 [RAS ゲートウェイ](../ras-gateway/ras-gateway.md)、[ソフトウェア定義ネットワーク (SDN)](../../../networking/sdn/software-defined-networking.md)、および[DirectAccess](../directaccess/directaccess.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
- [Vpn の機能の Always On](vpn-map-da.md): このトピックでは Always On vpn の機能について説明します。

- [Windows 10 で Vpn デバイストンネルを構成](vpn-device-tunnel-config.md)する: Always On vpn では、デバイスまたはコンピューター用の専用 vpn プロファイルを作成できます。 Always On VPN 接続には、_デバイストンネル_と_ユーザートンネル_という2種類のトンネルがあります。 デバイストンネルは、ログオン前の接続シナリオとデバイス管理の目的で使用されます。 ユーザー トンネルを使用すると、ユーザーが VPN サーバーを通じて組織のリソースにアクセスすることができます。

- [Windows Server 2016 および windows 10 用の Vpn 展開の Always On](always-on-vpn/deploy/always-on-vpn-deploy.md): リモートアクセスを Always On vpn 接続を使用して組織のネットワークに接続できるようにするポイント対サイト vpn 接続用のシングルテナント Vpn RAS ゲートウェイとしてリモートアクセスを展開する手順について説明します。 この展開で使用される各テクノロジについて、設計と展開のガイドを確認することをお勧めします。

- [Windows 10 VPN の技術ガイド](/windows/access-protection/vpn/vpn-guide): エンタープライズ VPN ソリューションで windows 10 クライアントに対して行う決定事項と、展開を構成する方法について説明します。 VPNv2 構成サービスプロバイダー (CSP) への参照を検索し、Microsoft Intune と Windows 10 用の VPN プロファイルテンプレートを使用して、モバイルデバイス管理 (MDM) の構成手順を提供できます。

- [Configuration Manager で vpn プロファイルを作成する方法](/configmgr/protect/deploy-use/create-vpn-profiles): このトピックでは、CONFIGURATION MANAGER で vpn プロファイルを作成する方法について説明します。

- [Windows 10 クライアント ALWAYS ON VPN 接続を構成](./always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)する: このトピックでは、ProfileXML のオプションとスキーマ、および ProfileXML VPN の作成方法について説明します。 サーバーインフラストラクチャを設定したら、VPN 接続を使用して、そのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成する必要があります。

- [Vpn プロファイルのオプション](/windows/access-protection/vpn/vpn-profile-options): このトピックでは、Windows 10 の vpn プロファイルの設定について説明し、Intune または Configuration Manager を使用して vpn プロファイルを構成する方法について説明します。 VPNv2 CSP の ProfileXML ノードを使用して、Windows 10 のすべての VPN 設定を構成できます。
