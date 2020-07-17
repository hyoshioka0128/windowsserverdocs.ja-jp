---
title: ネットワーク オフロードおよび最適化テクノロジ
description: このトピックでは、Windows Server 2016 のオフロードおよび最適化テクノロジの概要について説明し、これらのテクノロジに関するその他のガイダンスへのリンクを示します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: 04e924190170bbd3c841b452a27dc586bb69024e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316863"
---
# <a name="network-offload-and-optimization-technologies"></a>ネットワーク オフロードおよび最適化テクノロジ

このトピックでは、Windows Server 2016 で使用できるさまざまなネットワークオフロードおよび最適化機能の概要を説明し、ネットワークの効率を向上させる方法について説明します。 これらのテクノロジには、ソフトウェアのみ (そのため) の機能とテクノロジ、ソフトウェアとハードウェア (SH) の統合された機能とテクノロジ、ハードウェアのみ (ホー) の機能とテクノロジが含まれます。

Windows Server 2016 で使用可能なネットワーク機能には、次の3つのカテゴリがあります。 

1.  [ソフトウェアのみ (SO) の機能とテクノロジ](hpn-software-only-features.md): これらの機能は OS の一部として実装され、基になる NIC には依存しません。 場合によっては、最適な操作のために NIC のチューニングが必要になることがあります。 これらの例としては、vmQoS、Acl、NIC チーミングなどの Hyper-v 以外の機能などの Hyper-v 機能が挙げられます。   

2.  [ソフトウェアおよびハードウェア (SH) 統合された機能とテクノロジ](hpn-software-hardware-features.md): これらの機能には、ソフトウェアとハードウェアの両方のコンポーネントがあります。 このソフトウェアは、この機能が動作するために必要なハードウェア機能に深くされています。 これらの例には、VMMQ、VMQ、送信側 IPv4 チェックサムオフロード、RSS などがあります。   

3.  [ハードウェアのみ (ホー) の機能とテクノロジ](hpn-hardware-only-features.md): これらのハードウェアアクセラレータは、ソフトウェアと組み合わせてネットワークのパフォーマンスを向上させますが、ソフトウェア機能の一部では深くません。 これらの例としては、割り込みモデレーション、フロー制御、受信側 IPv4 チェックサムオフロードなどがあります。 

4. [Nic の詳細プロパティ](hpn-nic-advanced-properties.md): netadapter コマンドレットを使用して、Windows PowerShell を使用して nic とすべての機能を管理できます。  Nic およびすべての機能は、ネットワークコントロールパネル (ncpa.cpl」) を使用して管理することもできます。 

>[!TIP]
>- そのため、NIC 速度や NIC の機能に関係なく、すべてのハードウェアアーキテクチャで機能とテクノロジを利用できます。
>
>- SH およびホー機能は、ネットワークアダプターが機能またはテクノロジをサポートしている場合にのみ使用できます。

---