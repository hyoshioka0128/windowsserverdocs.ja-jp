---
title: RDS での構築し、デプロイ
description: リモート デスクトップの展開を作成する手順
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: 309ea068488d005eabfe22f8ea055f85dd098452
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453071"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>構築し、デプロイのリモート デスクトップ サービス展開

リモート デスクトップ サービス展開は、ユーザーとアプリとリソースを共有するためのインフラストラクチャです。 によって、エクスペリエンスを提供する、行うことができます、小さくまたは複雑にする必要があります。 リモート デスクトップの展開が容易に拡張します。 大きくと、リモート デスクトップ Web アクセスを減らす、ゲートウェイ、接続ブローカー サーバーとセッション ホスト サーバーでは、です。 リモート デスクトップ接続ブローカーを使用して、作業負荷を分散できます。 Active Directory ベースの認証は、高度なセキュリティ環境を提供します。 

[リモート デスクトップ クライアント](clients/remote-desktop-clients.md)電話の任意の Windows、Apple または Android コンピューター、タブレットからのアクセスを有効にします。

参照してください[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md)詳細については、異なる部分が連携して、リモート デスクトップ サービス展開を構成します。

以前のバージョンの Windows Server 上に構築された既存のリモート デスクトップの展開があるか。 パフォーマンスとスケールの周囲の新しい機能を利用を行う、WIndows Server 2016 に移るためのオプションをご覧ください。

- [Windows Server 2016 に RDS デプロイを移行します。](migrate-rds-role-services.md)
- [Windows Server 2016 に RDS デプロイをアップグレードします。](upgrade-to-rds-2016.md)

新しいリモート デスクトップの展開を作成しますか。 Windows Server 2016 でのリモート デスクトップを展開するのにには、次の情報を使用します。

- [リモート デスクトップ サービスのインフラストラクチャをデプロイします。](rds-deploy-infrastructure.md)
- [アプリと共有するリソースを保持するために、セッション コレクションを作成します。](rds-create-collection.md)
- [RDS デプロイをライセンスします。](rds-client-access-license.md)
- インストール、ユーザー、[リモート デスクトップ クライアント](clients/remote-desktop-clients.md)アプリとリソースにアクセスできるようにします。 
- 追加の接続ブローカーとセッション ホストを追加することで、高可用性を有効にします。
   - [RD セッション ホスト ファームを使用して既存の RDS コレクションをスケールアウトする](rds-scale-rdsh-farm.md)
   - [RD 接続ブローカー インフラストラクチャに高可用性を追加する](rds-connection-broker-cluster.md)
   - [RD Web および RD ゲートウェイ Web フロントに高可用性を追加する](rds-rdweb-gateway-ha.md)
   - [UPD 記憶域用に 2 ノードの記憶域スペース ダイレクト ファイル システムを展開する](rds-storage-spaces-direct-deployment.md)


ホスティング パートナーの顧客やユーザー、アプリをホストするをお探しのお客様にアプリとリソースを提供するリモート デスクトップを使用する場合は、チェック アウト[パートナーをホストしている、リモート デスクトップ サービス](rds-hosting-partners.md)については、評価に渡されたパートナーの一覧だけでなく、ホスティング環境として Azure で RDS を使用する方法を実行できます。
