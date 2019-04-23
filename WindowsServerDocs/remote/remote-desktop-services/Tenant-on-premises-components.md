---
title: テナント オンプレミス コンポーネント
description: RDS デプロイで、オンプレミスのコンポーネントについて説明します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a01dbd12d76b1efa84e38f2ded38cfd613fb2ac4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857403"
---
# <a name="tenant-on-premises-components"></a>テナント オンプレミス コンポーネント

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

次の情報には、デスクトップ ホスティング展開を構成するオンプレミスのコンポーネントについて説明します。  
  
##  <a name="clients"></a>クライアント  
ホストされたデスクトップとアプリケーションにアクセスするには、ユーザーはリモート デスクトップ プロトコル (RDP) 7.1 以降をサポートしているリモート デスクトップ クライアントを使用する必要があります。 具体的には、クライアントでは、リモート デスクトップ ゲートウェイとリモート デスクトップ接続ブローカーをサポートする必要があります。 アプリケーションをローカルのデスクトップを配信するには、クライアントで、RemoteApp の機能もサポートする必要があります。 最上位のゲートウェイのスケールを実現するために、クライアントは RD ゲートウェイに純粋な HTTP トランスポート接続をサポートする必要があります。  
  
追加情報:  
[RemoteFX 対応デバイス](https://social.technet.microsoft.com/wiki/contents/articles/14534.remotefx-enabled-devices.aspx)  
[新機能については Windows Server 2012 R2 リモート デスクトップ ゲートウェイです。](https://blogs.technet.microsoft.com/enterprisemobility/2013/03/14/whats-new-in-windows-server-2012-remote-desktop-gateway/#transport)  
[Microsoft リモート デスクトップ クライアント](https://technet.microsoft.com/library/dn473009.aspx)  
[Microsoft Store での Windows リモート デスクトップ アプリ](https://apps.microsoft.com/windows/app/remote-desktop/051f560e-5e9b-4dad-8b2e-fa5e0b05a480)  
[Microsoft リモート デスクトップ-Google Play の Android アプリ](https://play.google.com/store/apps/details?id=com.microsoft.rdc.android)  
[Mac App Store の Microsoft リモート デスクトップ](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12)  
[App Store での Microsoft リモート デスクトップ](https://itunes.apple.com/us/app/microsoft-remote-desktop/id714464092?mt=8)  
  
##  <a name="active-directory-domain-services"></a>Active Directory Domain Services  
一部の大きいとより高度なテナントは、オンプレミスの Active Directory Domain Services (AD DS) サーバーをホストする選択できます。 この場合は、テナントの環境で AD DS サーバーは、テナントのオンプレミスでは、AD DS サーバーのレプリカを通常になります。 テナントの環境で仮想ネットワークを作成し、Azure VPN を使用して、テナントのオンプレミス ネットワークから Azure データ センターでテナントの仮想ネットワークにサイト対サイト接続を作成するには、これはサポートされています。  
  
追加情報:  
[Microsoft Azure Virtual Network の概要](https://azure.microsoft.com/documentation/articles/virtual-networks-overview/)  
[Azure Portal を使用してサイト対サイト VPN 接続を持つリソース マネージャー VNet を作成します。](https://azure.microsoft.com/documentation/articles/vpn-gateway-howto-site-to-site-resource-manager-portal/)  


