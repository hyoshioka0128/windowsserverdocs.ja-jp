---
title: リモート デスクトップ サービスの高可用性
description: 高可用性 RDS デプロイの設定に関する情報を計画します。
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
ms.openlocfilehash: b5a2bd38c8831063d6fd2ba525b71a10403b8fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839263"
---
# <a name="remote-desktop-services---high-availability"></a>リモート デスクトップ サービスの高可用性

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

エラーやスロット リングでは、大規模なシステムでは避けられません。 簡単にシームレスに接続する高可用性をサポートし、エンドユーザーにリモート デスクトップのインフラストラクチャ ロールを設定するたびにします。

リモート デスクトップ サービスでは、次の項目は、高可用性を確立するために、それぞれのガイダンスを持つ、リモート デスクトップのインフラストラクチャ ロールを表します。
- [リモート デスクトップ接続ブローカー](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [リモート デスクトップ ゲートウェイ](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- リモート デスクトップ ライセンス
- [リモート デスクトップ Web アクセス](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

高可用性を確立するには、各 2 つ目のコンピューターの役割サービスを複製します。 Azure では、保証されたアップタイムを受信可用性内 (同じロールをホストしている) 2 つの仮想マシンのセットを配置することで設定します。

可用性セット、およびようになりましたことを確認して常に接続情報をデスクトップやアプリケーションにユーザーをリダイレクトすることができますを Azure SQL Database と Azure バックアップ SLA の電源を活用できます。

RDS 環境の作成のベスト プラクティスについてを参照してください、[デスクトップ ホスティング アーキテクチャ](desktop-hosting-reference-architecture.md)します。