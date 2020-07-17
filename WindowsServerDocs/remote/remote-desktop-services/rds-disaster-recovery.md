---
title: お使いの RDS 展開を保護する - ディザスター リカバリー
description: リモート デスクトップ サービス用のディザスター リカバリー オプションについて説明します
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: 9ff6a3b0-ea14-424e-9524-209252e9f1a8
author: lizap
ms.author: elizapo
ms.date: 06/12/2017
ms.openlocfilehash: 5c3257be5b3e9a53b8aa2400777f0519f8891843
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80861295"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>リモート デスクトップ サービス用のディザスター リカバリーを構成する

お使いの環境内にリモート デスクトップ サービスを展開すると、それはインフラストラクチャ、特にユーザーと共有しているアプリとリソースにとって重要な部分になります。 ネットワーク エラーや自然災害に至るまで、何らかの理由で RDS 展開がダウンした場合、ユーザーはこれらのアプリとリソースにアクセスできなくなり、ビジネスが打撃を受けることになります。 これを回避するために、展開のフェールオーバーを可能にするディザスター リカバリー ソリューションを構成でき、何らかの理由で RDS 展開が利用できなくなった場合に、自動的に引き継がれるバックアップを利用できます。

単一のコンポーネントまたはコンピューターがダウンした場合に RDS 展開の実行を保持するために、高可用性用に RDS を構成することをお勧めします。 これは、[RDSH ファーム](rds-scale-rdsh-farm.md)を設定し、[接続ブローカーを高可用性用にクラスター化する](rds-connection-broker-cluster.md)ことで実行できます。 

ここでお勧めするディザスター リカバリー ソリューションは、壊滅的な災害からお使いの展開を保護するためのものであり、RDS 展開全体を引き継ぐものです (高可用性のために構成された冗長ロールも含まれます)。 このような災害が発生した場合でも、展開に組み込まれたディザスター リカバリー ソリューションによって展開全体がフェールオーバーされ、ユーザーがアプリとリソースを短時間で利用できるようにすることができます。

次の情報を使用して、RDS 内にディザスター リカバリー ソリューションをデプロイします。

- [複数の Azure データ センターを活用して、1 か所の Azure データ センターがダウンした場合でもユーザーが確実に RDS 展開にアクセスできるようにする (地理的冗長性)](rds-multi-datacenter-deployment.md)
- [Azure Site Recovery をデプロイして、RDS コンポーネントのサイト対サイトまたはサイト対 Azure 間のフェールオーバーを提供する](rds-disaster-recovery-with-azure.md)


