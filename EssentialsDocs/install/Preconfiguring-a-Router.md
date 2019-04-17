---
title: "ルーターの事前構成"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 7dc66c8a439552c2087d0348b0115adba04027ee
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="preconfiguring-a-router"></a>ルーターの事前構成

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

通常、オペレーティング システムの新しいインストールは、インターネット対応のルーターとファイアウォールの顧客の内部ネットワークをインターネットに接続する必要があります。 事前に構成されたサーバーと付加価値としてルーターを提供する場合は、優れたユーザー エクスペリエンスを提供するようにルーターを事前に構成する追加の手順を実行できます。  
  
 ルーターで DHCP を有効になりますが必要です。 サーバーには、静的 IP アドレスを割り当てる必要があります。 これは、IP アドレスの DHCP 予約または DHCP アドレスの範囲外にある IP アドレスを割り当てることによって行うことができます。  
  
 ポート フォワーディングをルーターの外部インターフェイスから内部ネットワーク上のサーバーのアドレスに特定のポートを転送する、ルーター上で設定もあらかじめ構成する必要があります。 次の表は、推奨される構成を示します。  
  
|構成の設定|詳細|  
|---------------------------|-------------|  
|DHCP|[|  
|ポート フォワーディング|サーバーのアドレスには、次のポートを転送する必要があります。<br /><br /> -80 (ホスト型の構成、443 のみを使用)<br />-   443|  
|UPnP サポート|インストール中に、お客様とお客様の最適なエクスペリエンスの最も簡単なルーターの構成を提供する、UPnP™ サポートを有効にする必要があります。<br /><br /> **警告:** UPnP アーキテクチャできるセキュリティ リスクが左に有効な場合です。|  
  
 基本的なルーターの事前構成設定に加えて、ルーターを管理するためのより統合されたユーザー エクスペリエンスを提供する、次のタスクを完了できます。  
  
-   ユーザーがカスタム ユーザー インターフェイスからルーターを管理できるサーバーで、アドインを提供することで、ダッシュ ボードを拡張します。  
  
-   正常性アラートを拡張できるように、ルーターからのアラートをアラート ビューアーに表示されることができます。  
  
-   ルーターでは、複数のサブネットをサポートする場合、サーバーの IP アドレス、必要がありますとして配る DHCP を介して 1 つの DNS サーバー。  
  
-   ルーターは、アクティブな DirectoryÂ® ドメイン サービスの統合されたアクセス制御機能には、サーバーの初期構成中に Active Directory 統合を自動化することができます。 ルーター管理アドインをダッシュ ボードを使用してこの機能を公開することも必要があります。  
  
> [!NOTE]
>  ワイヤレス接続の構成の詳細については、次を参照してください。[ワイヤレス ネットワークのサポートの構成](Configure-Support-for-a-Wireless-Network.md)します。  
  
## <a name="see-also"></a>参照してください。  
 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)