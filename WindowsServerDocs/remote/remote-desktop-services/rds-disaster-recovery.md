---
title: RDS の展開 - ディザスター リカバリーを保護します。
description: リモート デスクトップ サービスは、障害復旧オプションについて説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ff6a3b0-ea14-424e-9524-209252e9f1a8
author: lizap
ms.author: elizapo
ms.date: 06/12/2017
ms.openlocfilehash: a6eac3a50999633d15b1b6dc28608f60f6fef6c7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834083"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>リモート デスクトップ サービス用のディザスター リカバリーを構成します。

お客様の環境にリモート デスクトップ サービスを展開するときに特にアプリとユーザーと共有するリソース、インフラストラクチャの重要な部分になります。 RDS の展開がダウンしても何のため、ネットワーク障害から自然災害への場合は、これらのアプリとリソースにアクセスできないし、ビジネスに悪影響が。 これを回避するにはの展開 - フェールオーバーを許可するディザスター リカバリー ソリューションを構成するときに自動的に引き継ぎを使用可能なバックアップがある、RDS デプロイ利用できない場合、何らかの理由から、します。

場合は、1 つのコンポーネントまたは下方向にマシンを実行している RDS デプロイを維持するには、高可用性 RDS デプロイの構成をお勧めします。 設定することによってこれを行う、 [RDSH ファーム](rds-scale-rdsh-farm.md)ことを確認し、[の高可用性接続ブローカーがクラスター化された](rds-connection-broker-cluster.md)します。 

ここで推奨ディザスター リカバリー ソリューションでは、RDS デプロイ全体 (高可用性のために構成されている冗長のロールを含む) を受け取るもの - 致命的な障害から、デプロイを保護します。 このような災害が発生する場合、デプロイに組み込まれているディザスター リカバリー ソリューションを持つと、デプロイ全体フェールオーバー、し、すぐにアプリのリソースと、ユーザーの実行できます。

RDS でのディザスター リカバリー ソリューションをデプロイするのにには、次の情報を使用します。

- [1 つの Azure データ センターがダウン (地理的冗長性) した場合でも、ユーザーは、RDS デプロイにアクセスできることを確認する複数の Azure データ センターを活用します。](rds-multi-datacenter-deployment.md)
- [サイト対サイトまたはサイトから Azure へのフェールオーバーでの RDS のコンポーネントのフェールオーバーを提供する Azure Site Recovery のデプロイします。](rds-disaster-recovery-with-azure.md)


