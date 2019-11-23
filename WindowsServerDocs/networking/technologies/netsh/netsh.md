---
title: ネットワーク シェル (netsh)
description: このトピックでは、Windows Server 2016 のネットワークシェル (netsh) コマンドラインユーティリティの概要について説明します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: ac440c8187424733c0636cf2013342458f08d2f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405544"
---
# <a name="network-shell-netsh"></a>ネットワークシェル \(Netsh\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ネットワークシェル (netsh) は、Windows Server 2016 を実行しているコンピューターにインストールした後に、さまざまなネットワーク通信サーバーの役割およびコンポーネントの状態を構成して表示するためのコマンドラインユーティリティです。

動的ホスト構成プロトコル \(DHCP\) クライアントおよび BranchCache などの一部のクライアントテクノロジでは、Windows 10 を実行しているクライアントコンピューターを構成するための netsh コマンドも用意されています。

ほとんどの場合、netsh コマンドは、Microsoft 管理コンソール \(MMC\) スナップ\-を使用して、各ネットワークサーバーの役割またはネットワーク機能に対して使用する場合と同じ機能を提供します。 たとえば、nps MMC スナップインまたは**netsh nps**コンテキストの netsh コマンドのいずれかを使用して、nps\) \(ネットワークポリシーサーバーを構成できます。

さらに、Windows Server で MMC スナップインとして使用できない、IPv6、ネットワークブリッジ、リモートプロシージャコール \(RPC\)などのネットワークテクノロジ用の netsh コマンドもあります。

>[!IMPORTANT]
>Windows PowerShell を使用して、ネットワークシェルではなく windows [Server 2016 と windows 10](https://technet.microsoft.com/library/mt156917.aspx)のネットワークテクノロジを管理することをお勧めします。 ただし、ネットワークシェルはスクリプトとの互換性のために用意されており、その使用はサポートされています。

## <a name="network-shell-netsh-technical-reference"></a>ネットワークシェル (Netsh) テクニカルリファレンス

Netsh テクニカルリファレンスには、netsh コマンドの構文、パラメーター、例など、包括的な netsh コマンドリファレンスが用意されています。 Netsh テクニカルリファレンスを使用して、Windows Server 2016 と Windows 10 を実行しているコンピューターでネットワークテクノロジをローカルまたはリモートで管理するための netsh コマンドを使用して、スクリプトとバッチファイルを作成できます。  
  
### <a name="content-availability"></a>コンテンツの可用性  
  
ネットワークシェルのテクニカルリファレンスは、TechNet ギャラリーの Windows ヘルプ \(* .chm\) 形式でダウンロードできます。 [Netsh Technical reference](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
