---
title: テナント オンプレミス コンポーネント
description: RDS 展開内のオンプレミス コンポーネントについて説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: 3c29eb20c4cf39c868bab07fdfddc50aec5c4b85
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86953495"
---
# <a name="tenant-on-premises-components"></a>テナント オンプレミス コンポーネント

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

以下では、デスクトップ ホスティングの展開を構成するオンプレミス コンポーネントについて説明します。  
  
##  <a name="clients"></a>クライアント  
ホストされたデスクトップとアプリケーションにアクセスするには、ユーザーはリモート デスクトップ プロトコル (RDP) 7.1 以降をサポートするリモート デスクトップ クライアントを使用する必要があります。 具体的には、クライアントでリモート デスクトップ ゲートウェイとリモート デスクトップ接続ブローカーがサポートされている必要があります。 アプリケーションをローカル デスクトップに配信するには、クライアントで RemoteApp 機能がサポートされている必要もあります。 ゲートウェイのスケールを最大化するには、クライアントで RD ゲートウェイへの純粋な HTTP トランスポート接続がサポートされている必要があります。  
  
追加情報:  
[Windows Server 2012 R2 のリモート デスクトップ ゲートウェイの新機能](https://techcommunity.microsoft.com/t5/microsoft-security-and/what-8217-s-new-in-windows-server-2012-remote-desktop-gateway/ba-p/247611)  
[Microsoft リモート デスクトップ クライアント](./clients/remote-desktop-clients.md)  
[Microsoft Store の Windows 用リモート デスクトップ アプリ](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft リモート デスクトップ - Google Play の Android アプリ](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store - Microsoft リモート デスクトップ](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)  
[App Store の Microsoft リモート デスクトップ](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>[Active Directory Domain Services]  
一部の大規模かつ高度なテナントでは、オンプレミスで Active Directory Domain Services (AD DS) サーバーをホストするという選択もできます。 この場合、テナントの環境の AD DS サーバーは、テナントのオンプレミスの AD DS サーバーのレプリカになることが一般的です。 これをサポートするには、テナントの環境に仮想ネットワークを作成し、Azure VPN を使用して、テナントのオンプレミス ネットワークから Azure データ センター内のテナントの仮想ネットワークへのサイト間接続を作成します。  
  
追加情報:  
[Microsoft Azure Virtual Network の概要](/azure/virtual-network/virtual-networks-overview)  
[Azure Portal を使用してリソース マネージャー VNet とサイト間 VPN 接続を作成する](/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)  
