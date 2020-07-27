---
title: リモート デスクトップ サービス - 高可用性
description: 高可用性 RDS 展開の設定に関する計画情報。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 36996d7f69c33198587dbe5297650c16ffeb1da2
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959324"
---
# <a name="remote-desktop-services---high-availability"></a>リモート デスクトップ サービス - 高可用性

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

失敗と調整は、大規模なシステムでは避けられません。 高可用性をサポートし、エンド ユーザーがいつでもシームレスに接続できるようにするように、リモート デスクトップ インフラストラクチャのロールを簡単に設定できます。

リモート デスクトップ サービスでは、次の項目はリモート デスクトップ インフラストラクチャのロールを表し、高可用性を確立するためのそれぞれのガイダンスが付けられています。
- [リモート デスクトップ接続ブローカー](./rds-connection-broker-cluster.md)
- [リモート デスクトップ ゲートウェイ](./rds-rdweb-gateway-ha.md)
- リモート デスクトップ ライセンス
- [リモート デスクトップ Web アクセス](./rds-rdweb-gateway-ha.md)

高可用性を確立するには、それぞれのロール サービスの複製を 2 台目のコンピューター上に作成します。 Azure では、2 つの仮想マシンのセット (同じロールをホスト) を、可用性セットに配置することによって、保証された稼働時間が受けられます。

可用性セットと共に、Azure SQL データベースとその Azure 認定の SLA の効力を活用して、常に接続情報を確保し、ユーザーをデスクトップやアプリケーションにリダイレクトできるようになりました。

RDS 環境を作成するためのベスト プラクティスについては、[デスクトップ ホスティングのアーキテクチャ](desktop-hosting-reference-architecture.md)に関するページを参照してください。
