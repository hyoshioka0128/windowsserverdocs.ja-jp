---
title: '手順 8: DirectAccess クラスターのスナップショット構成'
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c2f458570f4e584be1f73f9825d39d396546edf3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951007"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>手順 8: DirectAccess クラスターのスナップショット構成

>適用先:Windows Server (半期チャネル)、Windows Server 2016

これで、DirectAccess のテストラボが完成します。 この構成を保存して、NLB クラスター構成を使用して作業中の DirectAccess にすばやく戻ることができるようにします。これにより、他の DirectAccess モジュールテストラボガイド、テストラボガイド拡張機能をテストしたり、独自の実験や学習を行ったりすることができます。

1.  テスト ラボ内の物理コンピューターまたは仮想マシンのすべてのウィンドウを閉じ、正常にシャットダウンします。

2.  ラボが仮想マシンに基づいている場合は、各仮想マシンのスナップショットを保存し、スナップショットに DirectAccess クラスターと NLB という名前を付けます。 ラボで物理コンピューターを使用している場合は、ディスクイメージを作成して、DirectAccess のテストラボ構成を保存します。
