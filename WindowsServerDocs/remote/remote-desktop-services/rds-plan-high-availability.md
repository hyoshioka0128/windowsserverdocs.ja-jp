---
title: リモート デスクトップ サービス - 高可用性
description: 高可用性 RDS 展開の設定に関する計画情報。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 79fd05458d0d838e34402bf28ef83b9327bfcceb
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743457"
---
# <a name="remote-desktop-services---high-availability"></a>リモート デスクトップ サービス - 高可用性

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

失敗と調整は、大規模なシステムでは避けられません。 高可用性をサポートし、エンド ユーザーがいつでもシームレスに接続できるようにするように、リモート デスクトップ インフラストラクチャのロールを設定することは単純です。

リモート デスクトップ サービスでは、次の項目はリモート デスクトップ インフラストラクチャのロールを表し、高可用性を確立するためのそれぞれのガイダンスが付けられています。
- [リモート デスクトップ接続ブローカー](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [リモート デスクトップ ゲートウェイ](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- リモート デスクトップ ライセンス
- [リモート デスクトップ Web アクセス](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

高可用性を確立するには、それぞれのロール サービスの複製を 2 台目のコンピューター上に作成します。 Azure では、2 つの仮想マシンのセット (同じロールをホスト) を、可用性セットに配置することによって、保証された稼働時間が受けられます。

可用性セットと共に、Azure SQL データベースとその Azure 認定の SLA の効力を活用して、常に接続情報を確保し、ユーザーをデスクトップやアプリケーションにリダイレクトできるようになりました。

RDS 環境を作成するためのベスト プラクティスについては、[デスクトップ ホスティングのアーキテクチャ](desktop-hosting-reference-architecture.md)に関するページを参照してください。