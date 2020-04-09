---
title: '手順 8: DirectAccess クラスターのスナップショット構成'
description: このトピックは、「windows Server 2016 用 Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション」のテストラボガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 99804fb7746e0e45f586f7eaea307d8aac47d0ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818996"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>手順 8: DirectAccess クラスターのスナップショット構成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

これで、DirectAccess のテストラボが完成します。 この構成を保存して、NLB クラスター構成を使用して作業中の DirectAccess にすばやく戻ることができるようにします。これにより、他の DirectAccess モジュールテストラボガイド、テストラボガイド拡張機能、または独自の実験と学習を行うことができます。示し  
  
1.  テスト ラボ内の物理コンピューターまたは仮想マシンのすべてのウィンドウを閉じ、正常にシャットダウンします。  
  
2.  ラボが仮想マシンに基づいている場合は、各仮想マシンのスナップショットを保存し、スナップショットに DirectAccess クラスターと NLB という名前を付けます。 ラボで物理コンピューターを使用している場合は、ディスクイメージを作成して、DirectAccess のテストラボ構成を保存します。  
