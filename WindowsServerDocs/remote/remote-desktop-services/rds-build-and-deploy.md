---
title: RDS での構築し、デプロイ
description: リモート デスクトップ展開の構築手順
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9c3962a830d9544e915a96f061e32bb9e037949b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404032"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>構築し、デプロイのリモート デスクトップ サービス展開

リモート デスクトップ サービスの展開は、アプリとリソースをユーザーと共有するために使用するインフラストラクチャです。 提供するエクスペリエンスに応じて、必要な規模と複雑さにすることができます。 リモート デスクトップの展開が容易に拡張します。 大きくと、リモート デスクトップ Web アクセスを減らす、ゲートウェイ、接続ブローカー サーバーとセッション ホスト サーバーでは、です。 リモート デスクトップ接続ブローカーを使用して、作業負荷を分散できます。 Active Directory ベースの認証は、高度なセキュリティ環境を提供します。 

[リモート デスクトップ クライアント](clients/remote-desktop-clients.md)は、任意の Windows、Apple、Android のコンピューター、タブレット、またはスマートフォンからアクセスできます。

リモート デスクトップ サービスの展開を構成するさまざまなコンポーネントの詳しい説明については、「[リモート デスクトップ サービスのアーキテクチャ](desktop-hosting-logical-architecture.md)」をご覧ください。

以前のバージョンの Windows Server 上に構築された既存のリモート デスクトップ展開をお持ちの場合は、 Windows Server 2016 に移行すると、パフォーマンスとスケール関連の新機能や機能向上を利用できます。次の移行オプションをご確認ください。

- [RDS の展開を Windows Server 2016 に移行する](migrate-rds-role-services.md)
- [RDS の展開を Windows Server 2016 にアップグレードする](upgrade-to-rds-2016.md)

新しいリモート デスクトップ展開を作成する場合は、 次の情報を使用して、Windows Server 2016 にリモート デスクトップを展開します。

- [リモート デスクトップ サービス インフラストラクチャを展開する](rds-deploy-infrastructure.md)
- [共有するアプリとリソースを保持するセッション コレクションを作成する](rds-create-collection.md)
- [RDS 展開のライセンス](rds-client-access-license.md)
- ユーザーがアプリとリソースにアクセスできるように、[リモート デスクトップ クライアント](clients/remote-desktop-clients.md)をインストールしてもらいます。 
- 接続ブローカーとセッション ホストをさらに追加することで、高可用性を実現します。
   - [RD セッション ホスト ファームを使用して既存の RDS コレクションをスケールアウトする](rds-scale-rdsh-farm.md)
   - [RD 接続ブローカー インフラストラクチャに高可用性を追加する](rds-connection-broker-cluster.md)
   - [RD Web および RD ゲートウェイ Web フロントに高可用性を追加する](rds-rdweb-gateway-ha.md)
   - [UPD 記憶域用に 2 ノードの記憶域スペース ダイレクト ファイル システムを展開する](rds-storage-spaces-direct-deployment.md)


リモート デスクトップを使用して顧客にアプリとリソースを提供したいホスティング パートナーのお客様、またはアプリのホスト先をお探しのお客様は、「[リモート デスクトップ サービスのホスティング パートナー](rds-hosting-partners.md)」で、Azure で RDS をホスティング環境として使用する方法に関する試験についての情報、およびその試験に合格したパートナーの一覧をご覧ください。
