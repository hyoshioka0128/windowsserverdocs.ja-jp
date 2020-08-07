---
title: 手順 2. クラスターサーバーを計画する
description: このトピックは、「Windows Server 2016 のクラスターにリモートアクセスを展開する」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 762093c1cd9c4a8782274e796b5b82fd24d94855
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963838"
---
# <a name="step-2-plan-cluster-servers"></a>手順 2. クラスターサーバーを計画する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

単一のリモートアクセスサーバーを展開した後、クラスターにサーバーを追加することを計画します。

|タスク|説明|
|----|--------|
|[2.1 役割と機能のインストール](#BKMK_Install)|クラスターに追加する各サーバーについて、リモートアクセスの役割と Windows NLB 機能 (必要な場合) のインストールを計画し、トポロジ、IP アドレス指定、ルーティング、および転送を計画します。|
|[2.2 サーバー設定を構成する](#BKMK_Config)|クラスターに追加する各サーバーの設定を構成します。 仮想マシンを使用して、負荷分散されたサーバーのクラスターを構成できることに注意してください。 ルーティングと接続が正しく機能するためには、MAC アドレスのスプーフィングを使用するようにバーチャルマシンを構成する必要があります。|

## <a name="21-installing-roles-and-features"></a><a name="BKMK_Install"></a>2.1 役割と機能のインストール
クラスターに参加する各サーバーについて、リモートアクセスの役割のインストールを計画します。 また、Windows NLB を使用してクラスターへのトラフィックを負荷分散する場合は、ネットワーク負荷分散 (NLB) 機能をインストールする計画を立てます。 詳細については、「[ネットワーク負荷分散](../../../../../networking/technologies/network-load-balancing.md)」を参照してください。

## <a name="22-configure-server-settings"></a><a name="BKMK_Config"></a>2.2 サーバー設定を構成する
クラスターに追加する各サーバーについて、IP アドレスとドメインの設定を計画します。 次のことを考慮してください。

1.  クラスター内のサーバーはすべて同じドメインに属している必要があります。

2.  クラスター内のサーバーは、同じサブネットに配置する必要があります。

3.  クラスター内の各サーバーには、DirectAccess 展開で使用されているネットワークアダプターの数と同じ数が含まれている必要があります。

Windows NLB を使用してクラスターの負荷を分散すると、次の Windows NLB 設定が適用されます。

1.  操作モード-ユニキャスト。 これは NLB マネージャーを使用してマルチキャストに変更できます。 この設定は、リモートアクセス管理コンソールでは変更できません。

2.  負荷の重み係数-すべてのクラスターサーバーが同じ負荷を持つ、等しいとして定義されます。

3.  フィルターモード-トラフィックは複数のホスト間で負荷分散されます。

4.  Affinity-単一アフィニティが定義されます。

5.  プロトコル-両方
