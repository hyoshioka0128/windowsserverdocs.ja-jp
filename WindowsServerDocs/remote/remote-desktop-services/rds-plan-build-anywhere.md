---
title: リモート デスクトップ サービスの任意の場所のビルド
description: RDS デプロイをホストする場所を判断するのに役立つ計画情報。
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
ms.openlocfilehash: cbb8e73d753b1fe4f0293cf4427c634020a23a42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869513"
---
# <a name="remote-desktop-services---build-anywhere"></a>リモート デスクトップ サービスの任意の場所のビルド

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

オンプレミス、クラウド、またはその両方のハイブリッドを展開します。 お客様のビジネス ニーズの変化に応じて、展開を変更します。

あるか、基になるに関係なく [アーキテクチャ](desktop-hosting-logical-architecture.md) リモート デスクトップ サービスの環境は変わりません。
- 外部ユーザーの RD Web アクセス、RD ゲートウェイを使用するインターネットに接続するサーバーをある必要があります。
- Active Directory を持つ必要があります家のユーザーとリモート デスクトップのプロパティに、SQL データベースを高可用性環境におけるのとは-
- まだ必要 RD インフラストラクチャの役割 (RD 接続ブローカー、RD ゲートウェイ、RD ライセンス、および RD Web アクセス) と終了 RDSH 間の通信のアクセスまたはエンドユーザーを自分のデスクトップまたはアプリケーションに接続できる RDVH ホストです。

このような柔軟性では、両方の長所を活用することができます。
- 簡潔さと従量課金制のメソッドをクラウドとオンラインの世界に関連付けられています。
- 使いやすさと大量のリソースを既に活用の手間のかからない方法は、オンプレミスに存在します。

詳細については、する方法を紹介 [の構築し、デプロイのリモート デスクトップ サービス展開](rds-build-and-deploy.md)します。