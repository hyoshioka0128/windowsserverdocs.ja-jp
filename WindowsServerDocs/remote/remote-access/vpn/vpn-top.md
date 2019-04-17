---
title: 仮想プライベート ネットワーク (VPN)
description: このトピックを使用すると、Windows Server 2016 および Windows 10 VPN の機能と機能について説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cd4908f0-0d6f-4c02-8f98-4dc88c3dcb65
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: bf38995f0a2b396044d1f45b45eff8c3c2de329d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067304"
---
# 仮想プライベート ネットワーク \(VPN\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## 1 つのテナント VPN サーバーとして RAS ゲートウェイ

Windows Server 2016 では、リモート アクセス サーバーの役割は、次の関連するネットワーク アクセス テクノロジの論理グループです。

- リモート アクセス サービス (RAS)
- ルーティング
- Web アプリケーション プロキシ

これらのテクノロジは、リモート アクセス サーバーの役割の役割サービスです。

役割の追加と機能の削除ウィザードまたは Windows PowerShell のリモート アクセス サーバーの役割をインストールするときは、これらの 3 つの役割サービスの 1 つ以上をインストールできます。

リモート アクセス サービス ゲートウェイを展開してインストールすると、 **DirectAccess と VPN (RAS)** の役割サービス、\ (**RAS ゲートウェイ**\)。 RAS ゲートウェイは、多数の拡張機能と拡張機能を提供する 1 つのテナント RAS ゲートウェイ仮想プライベート ネットワーク \(VPN\) サーバーとして展開できます。

>[!NOTE]
>\(SDN\)、ソフトウェア定義ネットワークで使用するためのマルチ テナント VPN サーバーまたは DirectAccess サーバーとして RAS ゲートウェイを展開することもできます。 詳細については、 [RAS ゲートウェイ](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway)、[ソフトウェア定義ネットワーク (SDN)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)、および[DirectAccess](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/directaccess)を参照してください。

## 関連トピック
- [Always On VPN の機能](vpn-map-da.md): このトピックでは、Always On VPN の機能についてについて説明します。 

- [Windows 10 での VPN デバイス トンネルの構成](vpn-device-tunnel-config.md): Always On VPN は、デバイスまたはコンピューターに専用の VPN プロファイルを作成する機能を提供します。 Always On VPN 接続には、2 種類のトンネル:_デバイス トンネル_と_ユーザー トンネル_します。 デバイス トンネルはログオン前の接続のシナリオとデバイス管理の目的で使われます。 ユーザー トンネルでは、VPN サーバーを介して組織のリソースにアクセスすることができます。

- [常に VPN 展開の Windows Server 2016 および Windows 10](always-on-vpn/deploy/always-on-vpn-deploy.md): については、1 つとして、リモート アクセスの展開、リモートの従業員、組織に接続することを許可するサイト to\ 半の VPN 接続用の VPN RAS ゲートウェイのテナントを提供します。Always On VPN の接続、ネットワーク。 この展開で使用されるテクノロジの設計と展開ガイドを確認することをお勧めします。

- [Windows 10 VPN テクニカル ガイド](https://docs.microsoft.com/windows/access-protection/vpn/vpn-guide): 向けに決定する Windows 10 クライアント、エンタープライズ VPN ソリューションと展開を構成する方法について説明します。 VPNv2 構成サービス プロバイダー (CSP) への参照を見つけることができ、モバイル デバイス管理 (MDM) 構成手順が Windows 10 向けの Microsoft Intune と、VPN プロファイル テンプレートを使用して機能を提供します。

- [System Center Configuration Manager での作成の VPN プロファイルをする方法](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles): このトピックでは、System Center Configuration Manager (SCCM) で VPN プロファイルを作成する方法について説明します。

- [Windows 10 クライアント常に VPN 接続の構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): このトピックで説明、ProfileXML オプションとスキーマと ProfileXML VPN を作成する方法。 サーバー インフラストラクチャをセットアップしたら、VPN 接続では、そのインフラストラクチャとの通信に windows 10 クライアント コンピューターを構成する必要があります。 

- [VPN プロファイル オプション](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options): このトピックでは、Windows 10 での VPN プロファイルの設定について説明し、Intune や SCCM を使用して、VPN プロファイルを構成する方法について説明します。 VPNv2 CSP で ProfileXML ノードを使用して Windows 10 では、すべての VPN 設定を構成できます。

---