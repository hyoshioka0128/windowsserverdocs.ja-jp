---
title: ネットワーク オフロードおよび最適化テクノロジ
description: このトピックでは、オフロードと Windows Server 2016 での最適化テクノロジの概要を示し、詳細なガイダンスについては、これらのテクノロジへのリンクが含まれています。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: 9cd63ae557eab6e8e4f69fedd20619d4e7af9184
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847853"
---
# <a name="network-offload-and-optimization-technologies"></a>ネットワーク オフロードおよび最適化テクノロジ

このトピックで Windows Server 2016 で使用できる別のネットワーク オフロードと最適化機能の概要を説明してより効率的なネットワークを作成できる方法について説明します。 これらのテクノロジは、ソフトウェアのみ (SO) 機能およびテクノロジ、ソフトウェアとハードウェア (SH) の機能とテクノロジ、およびハードウェアのみ (ホー) 機能およびテクノロジの統合します。

Windows Server 2016 で使用可能なネットワーク機能の 3 つのカテゴリは次のとおりです。 

1.  [ソフトウェアのみ (SO) 機能およびテクノロジ](hpn-software-only-features.md):これらの機能は、OS の一部としては実装されは基になるレベルに依存しません。 場合によってこれらの機能では、いくつかの操作を最適化の NIC のチューニングが必要です。 これらの例には、vmQoS、Acl、NIC チーミングなどの非 HYPER-V 機能など、hyper-v の機能が含まれます。   

2.  [統合された機能とテクノロジのソフトウェアおよびハードウェア (SH)](hpn-software-hardware-features.md):これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 ソフトウェアは密接機能を使用するために必要なハードウェア機能に関連付けられています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサム オフロード、および RSS が含まれます。   

3.  [ハードウェア (ホスト) のみの機能およびテクノロジ](hpn-hardware-only-features.md):これらのハードウェア アクセラレーションは、ソフトウェアと組み合わせて、ネットワーク パフォーマンスを向上させるが、密接ソフトウェア機能の一部ではありません。 これらの例には、割り込み節度、フロー制御、および受信側 IPv4 チェックサム オフロードが含まれます。 

4. [プロパティを高度な NIC](hpn-nic-advanced-properties.md):Nic と NetAdapter コマンドレットを使用して Windows PowerShell を使用してすべての機能を管理することができます。  Nic とネットワーク コントロール パネル (ncpa.cpl) を使用してすべての機能を管理することもできます。 

>[!TIP]
>- その機能とテクノロジで利用できる速度の NIC または NIC 機能に関係なく、すべてのハードウェア アーキテクチャ。
>
>- SH とホー機能は、ネットワーク アダプターの機能やテクノロジをサポートする場合にのみ使用します。

---