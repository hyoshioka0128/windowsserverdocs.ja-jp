---
title: vRSS よく寄せられる質問
description: このトピックでは、いくつかよく寄せられる質問と回答 vRSS の使用についてを検索します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3fafe6c39285e65a9d39a76cc6b652dac5c3efbd
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133818"
---
# vRSS よく寄せられる質問

このトピックでは、いくつかよく寄せられる質問と回答 vRSS の使用についてを検索します。

## VRSS で使用する物理ネットワーク アダプターの要件を教えてください。

ネットワーク アダプターは、仮想マシンのキュー \(VMQ\) と互換性のあるである必要があり、10 gbps リンク速度以上必要があります。

詳細については、 [vRSS の使用を計画](vrss-plan.md)を参照してください。

## VRSS は hyper\ スレッド プロセッサ コアを搭載した動作しますか。

いいえ。 VRSS かつ VMQ hyper\ スレッド プロセッサ コアを無視します。

## VRSS はホスト仮想 Nic \(vNICs\) に動作しますか。

はい、できます。 **セット VMNetworkAdapter**の Windows PowerShell コマンドで仮想マシン \(VM\) 名とホスト vNIC を**有効にする NetAdapterRss**ではなく **、ManagementOS**パラメーターを使用します。

詳細については、 [RSS や vRSS 用の Windows PowerShell コマンド](vrss-wps.md)を参照してください。

## VM で vRSS を使用する必要があるの論理プロセッサの数かどうか。

Vm では、2 つまたは複数の論理プロセッサ \(LPs\) vRSS を使用できるようにする必要があります。

詳細については、 [vRSS の使用を計画](vrss-plan.md)を参照してください。

## NIC チーミングと互換性のある vRSS ですか。

はい、できます。 NIC チーミングを使用している場合は、NIC チーミングの設定を操作する VMQ を正しく構成することが重要です。 NIC チーミングの展開と管理の詳細については、 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)を参照してください。

## vRSS が有効になっているが、知るには機能しているかどうか。 

VRSS が動作している仮想マシンで、タスク マネージャーを開くと、仮想プロセッサ使用率を表示するかを確認することができます。 VM に確立された複数の接続がある場合は、使用率が 0% の上の 1 つ以上のコアを確認できます。

1 つの TCP セッションには、複数の論理プロセッサ コア全体に負荷分散をすることはできません、ため、VM する必要がありますを受信する複数の TCP vRSS が動作しているかどうかを確認する前に、セッション。

複数の TCP セッションを受信して、VM 使用率が 0% の上の 1 つ以上の LP コアが表示されない場合は、すべての[vRSS の使用を計画する](vrss-plan.md)トピックの準備完了したことを確認します。

## ホストで検索し、すべてのプロセッサが使用されています。 すべての他のいずれかをスキップしてようです。
  
ハイパースレッディングが有効になっているかどうかを確認します。 VMQ と vRSS の両方が hyper\ シングル スレッドのコアをスキップする設計されています。

## RSS や vRSS のさまざまな Windows PowerShell コマンドはありますか。

さあ何とも言えません。 ネイティブ ホストで RSS と仮想マシンで RSS の両方に同じコマンドを使用する vRSS も VMQ スイッチ ポートで有効にする物理 NIC - や VM と vRSS を有効にする必要があります。

詳細については、 [RSS や vRSS 用の Windows PowerShell コマンド](vrss-wps.md)を参照してください。

---
