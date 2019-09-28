---
title: テナント オンプレミス コンポーネント
description: RDS 展開内のオンプレミス コンポーネントについて説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3eebb38-a835-4fa6-9e41-1966014bf2cb
author: lizap
manager: dongill
ms.openlocfilehash: a9ff1382d2a2e7e2acf0247fa2ba4ae8e9642162
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387843"
---
# <a name="tenant-on-premises-components"></a>テナント オンプレミス コンポーネント

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

以下では、デスクトップ ホスティングの展開を構成するオンプレミス コンポーネントについて説明します。  
  
##  <a name="clients"></a>クライアント  
ホストされたデスクトップとアプリケーションにアクセスするには、ユーザーはリモート デスクトップ プロトコル (RDP) 7.1 以降をサポートするリモート デスクトップ クライアントを使用する必要があります。 具体的には、クライアントでリモート デスクトップ ゲートウェイとリモート デスクトップ接続ブローカーがサポートされている必要があります。 アプリケーションをローカル デスクトップに配信するには、クライアントで RemoteApp 機能がサポートされている必要もあります。 ゲートウェイのスケールを最大化するには、クライアントで RD ゲートウェイへの純粋な HTTP トランスポート接続がサポートされている必要があります。  
  
追加情報:  
[RemoteFX 対応デバイス](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx)  
[Windows Server 2012 R2 のリモート デスクトップ ゲートウェイの新機能](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport)  
[Microsoft リモート デスクトップ クライアント](https://technet.microsoft.com/library/dn473009.aspx)  
[Microsoft Store の Windows 用リモート デスクトップ アプリ](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft リモート デスクトップ - Google Play の Android アプリ](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store - Microsoft リモート デスクトップ](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417?mt=12)  
[App Store の Microsoft リモート デスクトップ](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory Domain Services  
一部の大規模かつ高度なテナントでは、オンプレミスで Active Directory Domain Services (AD DS) サーバーをホストするという選択もできます。 この場合、テナントの環境の AD DS サーバーは、テナントのオンプレミスの AD DS サーバーのレプリカになることが一般的です。 これをサポートするには、テナントの環境に仮想ネットワークを作成し、Azure VPN を使用して、テナントのオンプレミス ネットワークから Azure データ センター内のテナントの仮想ネットワークへのサイト間接続を作成します。  
  
追加情報:  
[Microsoft Azure Virtual Network の概要](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Azure Portal を使用してリソース マネージャー VNet とサイト間 VPN 接続を作成する](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


