---
title: ルーターの事前構成
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9153ac90-bb0c-4b8d-93b2-e2121ed13636
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bdfa3215b7a2426bcde807119971d99ccc229716
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311573"
---
# <a name="preconfiguring-a-router"></a>ルーターの事前構成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

通常、新しくオペレーティング システムをインストールする場合、顧客の内部ネットワークをインターネットに接続するために、インターネット対応のルーターおよびファイアウォールが必要です。 あらかじめ構成されたサーバーに付加価値としてルーターを提供する場合、より良いユーザー エクスペリエンスを提供するため、追加の手順を実行してあらかじめルーターを構成できます。  
  
 ルーターで DHCP が有効になっている必要があります。 サーバーには静的 IP アドレスを割り当てる必要があります。 これは、IP アドレスの DHCP 予約、または DHCP アドレス範囲の外にある IP アドレスの割り当てによって行います。  
  
 ルーターの外部インターフェイスから内部ネットワーク上のサーバーのアドレスに特定のポートを転送するため、ポート フォワーディング設定もあらかじめ構成する必要があります。 次の表は、推奨される構成の一覧を示します。  
  
|構成設定|詳細|  
|---------------------------|-------------|  
|DHCP|オン|  
|ポート フォワーディング|以下のポートをサーバーのアドレスに転送する必要があります。<br /><br /> -80 (ホストされる構成の場合、443のみを使用します)<br />-443|  
|UPnP サポート|UPnP サポートを有効にして、お客様のための最も簡単なルーター構成と、インストール時の最良のカスタマーエクスペリエンスを提供する必要があります。<br /><br /> **警告:** UPnP アーキテクチャが有効のままになっていると、セキュリティ上のリスクが生じる可能性があります。|  
  
 基本的なルーターの事前構成設定に加えて、ルーターを管理するためのより統合されたユーザー エクスペリエンスを提供するために、次のタスクを完了できます。  
  
-   ダッシュボードを拡張するには、サーバー上にアドインを提供して、ユーザーがカスタム ユーザー インターフェイスからルーターを管理できるようにします。  
  
-   正常性アラートを拡張して、ルーターからのアラートをアラート ビューアーで表示できるようにします。  
  
-   ルーターが複数のサブネットをサポートする場合、サーバーの IP アドレスを DHCP 経由で 1 つの DNS サーバーとして配る必要があります。  
  
-   ルーターに Active Directory®ドメインサービスのアクセス制御機能が統合されている場合は、サーバーの初期構成中に Active Directory 統合を自動化できます。 この機能を、ダッシュボードのルーター管理アドインを介して公開することも必要です。  
  
> [!NOTE]
>  ワイヤレス接続の構成の詳細については、「[ワイヤレス ネットワークのサポートの構成](Configure-Support-for-a-Wireless-Network.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)