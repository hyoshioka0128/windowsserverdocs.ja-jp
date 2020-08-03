---
title: ネットワーク インターフェイスの順序を構成する
description: このトピックは、Windows Server 2016 のネットワークサブシステムのパフォーマンスチューニングガイドに含まれています。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: dcscontentpm
ms.author: v-tea
author: Teresa-Motiv
ms.openlocfilehash: 176fa80cd82fdaa3ac76a8661d189b16aa9631ff
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87517897"
---
# <a name="configure-the-order-of-network-interfaces"></a>ネットワーク インターフェイスの順序を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 と Windows 10 では、インターフェイスメトリックを使用してネットワークインターフェイスの順序を構成できます。

これは、以前のバージョンの Windows および Windows Server とは異なります。これにより、ユーザーインターフェイスを使用するか、 **Inetcfgcomponentbindings:: MoveBefore**コマンドと**Inetcfgcomponentbindings:: movebefore**コマンドを使用して、ネットワークアダプターのバインド順序を構成できます。 ネットワークインターフェイスの順序付けの2つの方法は、Windows Server 2016 と Windows 10 では使用できません。

代わりに、新しい方法を使用して、各アダプターのインターフェイスメトリックを構成することによって、ネットワークアダプターの列挙順序を設定できます。 インターフェイスメトリックを構成するには、Windows PowerShell コマンドの[Set ne?](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface)を使用します。

ネットワークトラフィックルートを選択し、 **InterfaceMetric** **インターフェイス**コマンドのパラメーターを構成した場合、インターフェイス設定を決定するために使用される全体的なメトリックは、ルートメトリックとインターフェイスメトリックの合計になります。 通常、インターフェイスメトリックは、ワイヤードとワイヤレスの両方が使用可能な場合に、ワイヤードを使用するなど、特定のインターフェイスを優先します。

次の Windows PowerShell コマンドの例は、このパラメーターの使用方法を示しています。

```powershell
Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15
```

アダプターが一覧に表示される順序は、IPv4 または IPv6 のインターフェイスメトリックによって決まります。  詳細については、「 [Getadaptersaddresses 関数](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)」を参照してください。

このガイドのすべてのトピックへのリンクについては、「[ネットワークサブシステムのパフォーマンスチューニング](net-sub-performance-top.md)」を参照してください。
