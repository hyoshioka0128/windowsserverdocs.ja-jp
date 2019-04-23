---
title: vRSS よく寄せられる質問
description: このトピックでは、いくつかについてよく寄せられる質問と回答 vRSS を使用してを紹介します。
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840243"
---
# <a name="vrss-frequently-asked-questions"></a>vRSS よく寄せられる質問

このトピックでは、いくつかについてよく寄せられる質問と回答 vRSS を使用してを紹介します。

## <a name="what-are-the-requirements-for-the-physical-network-adapters-that-i-use-with-vrss"></a>VRSS で使用する物理ネットワーク アダプターの要件とは

ネットワーク アダプターを仮想マシン キューとの互換性にする必要があります\(VMQ\)リンクの速度は 10 Gbps 以上が必要とします。

詳細については、次を参照してください。 [vRSS の使用を計画](vrss-plan.md)します。

## <a name="does-vrss-work-with-hyper-threaded-processor-cores"></a>ハイパーと連携します vRSS\-プロセッサ コアをスレッドですか?

いいえ。 VRSS および VMQ の両方を無視ハイパー\-プロセッサ コアをスレッドです。

## <a name="does-vrss-work-for-host-virtual-nics-vnics"></a>使用 vRSS ホスト仮想 Nic \(Vnic\)でしょうか。

[はい]。 使用して、 **- ManagementOS**仮想マシンではなくパラメーター \(VM\)名を**Set-vmnetworkadapter** Windows PowerShell のコマンドと**有効にする NetAdapterRss**ホスト vNIC の。

詳細については、次を参照してください。 [RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)します。

## <a name="how-many-logical-processors-does-a-vm-need-to-use-vrss"></a>VM で vRSS を使用する必要があるの論理プロセッサの数。

Vm には、2 つ以上の論理プロセッサが必要があります\(LPs\) vRSS を使用できるようにします。

詳細については、次を参照してください。 [vRSS の使用を計画](vrss-plan.md)します。

## <a name="is-vrss-compatible-with-nic-teaming"></a>VRSS は NIC チーミングと互換性のあるですか。

[はい]。 NIC チーミングを使用している場合は、NIC チーミングの設定を使用するために VMQ を正しく構成することが重要です。 NIC チーミングの展開と管理の詳細については、次を参照してください。 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)します。

## <a name="vrss-is-enabled-but-how-do-i-know-if-it-is-working"></a>vRSS を有効にするが動作しているかどうかを知る方法でしょうか。 

VRSS は VM では、タスク マネージャーを開き、仮想プロセッサ使用率を表示して操作を指示することができます。 VM に確立されている複数の接続がある場合は、0% 使用率の上の 1 つ以上のコアを確認できます。

1 つの TCP セッションでは、複数の論理プロセッサ コア間で負荷分散をすることはできません、ため、VM する必要がありますを受信する複数の TCP vRSS が動作しているかどうかを確認するにはセッション。

VM が複数の TCP セッションを受信して 1 つ以上の LP コア使用率 0% の上に表示されない場合は、すべてのトピックの準備手順を完了したことを確認します[vRSS の使用を計画](vrss-plan.md)します。

## <a name="im-looking-at-the-host-and-not-all-of-the-processors-are-being-used-it-looks-like-every-other-one-is-being-skipped"></a>ホストを監視していますが、使用されていないプロセッサがあります 1 つおきにスキップされていると思われます。
  
ハイパー スレッディングが有効であるかどうかをチェックします。 VMQ と vRSS の両方がスキップするように設計\-ハイパー スレッディング コア。

## <a name="are-there-different-windows-powershell-commands-for-rss-and-vrss"></a>RSS および vRSS を別の Windows PowerShell コマンドはありますか。

さあ何とも言えません。 ネイティブ ホストで RSS と Vm で RSS の両方に同じコマンドを使用して、スイッチ ポートで有効にする - 物理 NIC で、および VM と vRSS を有効にするために VMQ は vRSS も必要です。

詳細については、次を参照してください。 [RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)します。

---
