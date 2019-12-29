---
title: 仮想プライベート ネットワーク (VPN)
description: このトピックでは、Windows Server 2016 と Windows 10 VPN の機能について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 6b647d8cbf9586408b49c1519b57d32e596fce10
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404222"
---
# <a name="virtual-private-networking-vpn"></a>仮想プライベート ネットワーク (VPN)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="ras-gateway-as-a-single-tenant-vpn-server"></a>シングルテナント VPN サーバーとしての RAS ゲートウェイ

Windows Server 2016 では、リモートアクセスサーバーの役割は、次の関連するネットワークアクセステクノロジを論理的にグループ化したものです。

- リモートアクセスサービス (RAS)
- ルーティング
- Web アプリケーション プロキシ

これらのテクノロジは、リモートアクセスサーバーの役割の役割サービスです。

役割と機能の追加ウィザードまたは Windows PowerShell を使用してリモートアクセスサーバーの役割をインストールする場合は、これら3つの役割サービスの1つまたは複数をインストールできます。

**DirectAccess および VPN (ras)** 役割サービスをインストールすると、リモートアクセスサービスゲートウェイ (**ras ゲートウェイ**) が展開されます。 RAS ゲートウェイは、多数の高度な機能と拡張機能を提供する単一のテナント RAS ゲートウェイ仮想プライベートネットワーク (VPN) サーバーとして展開できます。

>[!NOTE]
>ソフトウェア定義ネットワーク (SDN) で使用するマルチテナント VPN サーバーとして、または DirectAccess サーバーとして RAS ゲートウェイを展開することもできます。 詳細については、「 [RAS ゲートウェイ](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway)、[ソフトウェア定義ネットワーク (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)、および[DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)」を参照してください。

## <a name="related-topics"></a>関連トピック
- [VPN の機能を Always On し](vpn-map-da.md)ます。このトピックでは、Always On VPN の機能について説明します。 

- [Windows 10 で VPN デバイストンネルを構成する](vpn-device-tunnel-config.md):Always On VPN を使用すると、デバイスまたはコンピューター用の専用 VPN プロファイルを作成できます。 Always On VPN 接続には、_デバイストンネル_と_ユーザートンネル_という2種類のトンネルがあります。 デバイストンネルは、ログオン前の接続シナリオとデバイス管理の目的で使用されます。 ユーザートンネルを使用すると、ユーザーは VPN サーバー経由で組織のリソースにアクセスできます。

- [Windows Server 2016 および windows 10 用の VPN 展開の Always On](always-on-vpn/deploy/always-on-vpn-deploy.md):リモートの従業員が Always On VPN 接続を使用して組織のネットワークに接続できるようにする、ポイント対サイト VPN 接続用のシングルテナント VPN RAS ゲートウェイとしてリモートアクセスをデプロイする手順について説明します。 この展開で使用される各テクノロジについて、設計と展開のガイドを確認することをお勧めします。

- [Windows 10 VPN 技術ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide):エンタープライズ VPN ソリューションで Windows 10 クライアントに対して行う決定事項と、展開を構成する方法について説明します。 VPNv2 構成サービスプロバイダー (CSP) への参照を検索し、Microsoft Intune と Windows 10 用の VPN プロファイルテンプレートを使用して、モバイルデバイス管理 (MDM) の構成手順を提供できます。

- [System Center Configuration Manager で VPN プロファイルを作成する方法](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles):このトピックでは、System Center Configuration Manager (SCCM) で VPN プロファイルを作成する方法について説明します。

- [Windows 10 クライアント ALWAYS ON VPN 接続を構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections)します。このトピックでは、ProfileXML のオプションとスキーマ、および ProfileXML VPN の作成方法について説明します。 サーバーインフラストラクチャを設定したら、VPN 接続を使用して、そのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成する必要があります。

- [VPN プロファイルのオプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options):このトピックでは、Windows 10 の VPN プロファイル設定について説明し、Intune または SCCM を使用して VPN プロファイルを構成する方法について説明します。 VPNv2 CSP の ProfileXML ノードを使用して、Windows 10 のすべての VPN 設定を構成できます。
