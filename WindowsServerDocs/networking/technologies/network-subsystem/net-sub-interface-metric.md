---
title: ネットワーク インターフェイスの順序を構成する
description: このトピックでは、Windows Server 2016 は、ネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 18bc9a268b4e69e4b87b6b1e310f1162473adb10
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821773"
---
# <a name="configure-the-order-of-network-interfaces"></a>ネットワーク インターフェイスの順序を構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 および Windows 10 では、ネットワーク インターフェイスの順序を構成するのにインターフェイス メトリックを使用できます。

これは以前のバージョンの Windows と Windows Server は、ユーザー インターフェイスまたはコマンドを使用してネットワーク アダプターのバインドの順序を構成することを許可されている異なる**INetCfgComponentBindings::MoveBefore**と**INetCfgComponentBindings::MoveAfter**します。 ネットワーク インターフェイスを順序付けの 2 つのメソッドでは、Windows Server 2016 および Windows 10 で使用できません。

代わりに、各アダプターのインターフェイス メトリックを構成することでネットワーク アダプターの列挙の順序を設定するため、新しいメソッドを使用することができます。 使用して、インターフェイス メトリックを構成することができます、[セット NetIPInterface](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface) Windows PowerShell コマンド。

ネットワーク トラフィック ルートを選択し、構成した場合、**インターフェイス メトリック**のパラメーター、**セット NetIPInterface**コマンドをインターフェイスを決定するために使用する全体的なメトリック基本設定は、ルートのメトリックと、インターフェイス メトリックの合計です。 通常、インターフェイス メトリックは、どちらもワイヤード (有線) ワイヤレスが利用可能な場合にワイヤード (有線) を使用してなどの特定のインターフェイスの基本設定を示します。

次の Windows PowerShell コマンドの例では、このパラメーターの使用を示します。

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

アダプターが一覧に表示される順序については、IPv4 または IPv6 インターフェイス メトリックによって決まります。  詳細については、次を参照してください。 [GetAdaptersAddresses 関数](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)します。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。
