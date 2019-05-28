---
title: ルーターの事前構成
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6c4f471b6042fb22d74c10663cc38db995a16eb5
ms.sourcegitcommit: 2977c707a299929c6ab0d1e0adab2e1c644b8306
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2019
ms.locfileid: "63720808"
---
# <a name="preconfiguring-a-router"></a>ルーターの事前構成

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

通常、新しくオペレーティング システムをインストールする場合、顧客の内部ネットワークをインターネットに接続するために、インターネット対応のルーターおよびファイアウォールが必要です。 あらかじめ構成されたサーバーに付加価値としてルーターを提供する場合、より良いユーザー エクスペリエンスを提供するため、追加の手順を実行してあらかじめルーターを構成できます。  
  
 ルーターで DHCP が有効になっている必要があります。 サーバーには静的 IP アドレスを割り当てる必要があります。 これは、IP アドレスの DHCP 予約、または DHCP アドレス範囲の外にある IP アドレスの割り当てによって行います。  
  
 ルーターの外部インターフェイスから内部ネットワーク上のサーバーのアドレスに特定のポートを転送するため、ポート フォワーディング設定もあらかじめ構成する必要があります。 次の表は、推奨される構成の一覧を示します。  
  
|構成設定|詳細|  
|---------------------------|-------------|  
|DHCP|オン|  
|ポート フォワーディング|以下のポートをサーバーのアドレスに転送する必要があります。<br /><br /> -80 (ホストされている構成では、443 のみを使用)<br />-   443|  
|UPnP サポート|インストール中に、顧客および最善のカスタマー エクスペリエンスの最も簡単なルーターの構成を提供する、UPnP™ サポートを有効にする必要があります。<br /><br /> **警告:** UPnP アーキテクチャを有効のままにしておくと、セキュリティ上のリスクを引き起こすことがあります。|  
  
 基本的なルーターの事前構成設定に加えて、ルーターを管理するためのより統合されたユーザー エクスペリエンスを提供するために、次のタスクを完了できます。  
  
-   ダッシュボードを拡張するには、サーバー上にアドインを提供して、ユーザーがカスタム ユーザー インターフェイスからルーターを管理できるようにします。  
  
-   正常性アラートを拡張して、ルーターからのアラートをアラート ビューアーで表示できるようにします。  
  
-   ルーターが複数のサブネットをサポートする場合、サーバーの IP アドレスを DHCP 経由で 1 つの DNS サーバーとして配る必要があります。  
  
-   Active DirectoryÂ® Domain Services の統合アクセス制御機能にルーターがある場合は、サーバーの初期構成中に Active Directory の統合を自動化できます。 この機能を、ダッシュボードのルーター管理アドインを介して公開することも必要です。  
  
> [!NOTE]
>  ワイヤレス接続の構成の詳細については、「[ワイヤレス ネットワークのサポートの構成](Configure-Support-for-a-Wireless-Network.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)