---
title: ネットワーク インターフェイスの順序を構成します。
description: このトピックは、Windows Server 2016 のネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2edf9d312e50a0fd8485e0032dee8413675367cf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-order-of-network-interfaces"></a>ネットワーク インターフェイスの順序を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 および Windows 10 では、ネットワーク インターフェイスの順序を構成するのにインターフェイス メトリックを使用することができます。

これは、以前のバージョンの Windows および Windows Server は、ユーザー インターフェイスまたはコマンドのいずれかを使用してネットワーク アダプターのバインド順序を構成することができるとは異なる**INetCfgComponentBindings::MoveBefore**と**INetCfgComponentBindings::MoveAfter**します。 これらのネットワーク インターフェイスの順序の 2 つの方法では、Windows Server 2016 および Windows 10 で利用できません。

代わりに、各アダプターのインターフェイス メトリックを構成することによって、ネットワーク アダプターの列挙の順序を設定するため、新しいメソッドを使用することができます。 使用して、インターフェイス メトリックを構成することができます、[セット NetIPInterface](https://docs.microsoft.com/en-us/powershell/module/nettcpip/set-netipinterface)の Windows PowerShell コマンド。

ネットワーク トラフィック ルートを選択し、構成した場合、**インターフェイス メトリック**のパラメーター、**セット NetIPInterface**コマンドで、全体的なメトリック インターフェイス] 基本設定の決定に使用される、ルートのメトリックとインターフェイス メトリックの合計です。 通常、インターフェイス メトリックは、両方ワイヤード (有線) およびワイヤレスが利用可能な場合は、ワイヤード (有線) の使用など、特定のインターフェイスに基本設定を示します。

次の Windows PowerShell コマンド例では、このパラメーターの使用を示します。

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

アダプターが一覧に表示される順序は、IPv4 または IPv6 インターフェイス メトリックによって決定されます。  詳細については、次を参照してください。[GetAdaptersAddresses 関数](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)します。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。
