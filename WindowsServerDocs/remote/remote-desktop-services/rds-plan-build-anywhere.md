---
title: リモート デスクトップ サービスの任意の場所のビルド
description: RDS の展開をホストする場所の判断に役立つ計画情報。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c803a383-0eea-4e11-bca5-d204ab758048
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 4563108d2efa9cd864fbe75fa82349d21659a941
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712335"
---
# <a name="remote-desktop-services---build-anywhere"></a>リモート デスクトップ サービスの任意の場所のビルド

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

オンプレミス、クラウド、またはその両方のハイブリッドを展開します。 お客様のビジネス ニーズの変化に応じて、展開を変更します。

あるか、基になるに関係なく [アーキテクチャ](desktop-hosting-logical-architecture.md) リモート デスクトップ サービスの環境は変わりません。
- 外部ユーザーの RD Web アクセス、RD ゲートウェイを使用するインターネットに接続するサーバーをある必要があります。
- Active Directory を持つ必要があります家のユーザーとリモート デスクトップのプロパティに、SQL データベースを高可用性環境におけるのとは-
- まだ必要 RD インフラストラクチャの役割 (RD 接続ブローカー、RD ゲートウェイ、RD ライセンス、および RD Web アクセス) と終了 RDSH 間の通信のアクセスまたはエンドユーザーを自分のデスクトップまたはアプリケーションに接続できる RDVH ホストです。

このような柔軟性では、両方の長所を活用することができます。
- 簡潔さと従量課金制のメソッドをクラウドとオンラインの世界に関連付けられています。
- よく知っている手間のかからない方法で、オンプレミスに既に存在する大量のリソースを活用。

詳細については、する方法を紹介 [の構築し、デプロイのリモート デスクトップ サービス展開](rds-build-and-deploy.md)します。