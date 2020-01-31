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
ms.openlocfilehash: fdd409dee5a7a957580daeeb05209336edfd86f6
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822615"
---
# <a name="virtual-private-networking-vpn"></a>仮想プライベート ネットワーク (VPN)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10

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
- [Vpn の機能の Always On](vpn-map-da.md): このトピックでは Always On vpn の機能について説明します。 

- [Windows 10 で Vpn デバイストンネルを構成](vpn-device-tunnel-config.md)する: Always On vpn では、デバイスまたはコンピューター用の専用 vpn プロファイルを作成できます。 Always On VPN 接続には、_デバイストンネル_と_ユーザートンネル_という2種類のトンネルがあります。 デバイストンネルは、ログオン前の接続シナリオとデバイス管理の目的で使用されます。 ユーザートンネルを使用すると、ユーザーは VPN サーバー経由で組織のリソースにアクセスできます。

- [Windows Server 2016 および windows 10 用の Vpn 展開の Always On](always-on-vpn/deploy/always-on-vpn-deploy.md): リモートアクセスを Always On vpn 接続を使用して組織のネットワークに接続できるようにするポイント対サイト vpn 接続用のシングルテナント Vpn RAS ゲートウェイとしてリモートアクセスを展開する手順について説明します。 この展開で使用される各テクノロジについて、設計と展開のガイドを確認することをお勧めします。

- [Windows 10 VPN の技術ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): エンタープライズ VPN ソリューションで windows 10 クライアントに対して行う決定事項と、展開を構成する方法について説明します。 VPNv2 構成サービスプロバイダー (CSP) への参照を検索し、Microsoft Intune と Windows 10 用の VPN プロファイルテンプレートを使用して、モバイルデバイス管理 (MDM) の構成手順を提供できます。

- [Configuration Manager で vpn プロファイルを作成する方法](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles): このトピックでは、CONFIGURATION MANAGER で vpn プロファイルを作成する方法について説明します。

- [Windows 10 クライアント ALWAYS ON VPN 接続を構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections)する: このトピックでは、ProfileXML のオプションとスキーマ、および ProfileXML VPN の作成方法について説明します。 サーバーインフラストラクチャを設定したら、VPN 接続を使用して、そのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成する必要があります。

- [Vpn プロファイルのオプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): このトピックでは、Windows 10 の vpn プロファイルの設定について説明し、Intune または Configuration Manager を使用して vpn プロファイルを構成する方法について説明します。 VPNv2 CSP の ProfileXML ノードを使用して、Windows 10 のすべての VPN 設定を構成できます。
