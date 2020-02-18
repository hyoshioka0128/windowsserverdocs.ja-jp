---
title: ネットワーク シェル (netsh)
description: このトピックでは、Windows Server 2016 の Network Shell (netsh) コマンドライン ユーティリティの概要について説明します。
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
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405544"
---
# <a name="network-shell-netsh"></a>Network Shell \(netsh\)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Network Shell (netsh) は、コマンドライン ユーティリティであり、Windows Server 2016 を実行中のコンピューターにインストールした後、さまざまなネットワーク通信サーバーの役割とコンポーネントを構成してそれらのステータスを表示できます。

動的ホスト構成プロトコル \(DHCP\) クライアントや BranchCache などの一部のクライアント テクノロジでも、Windows 10 を実行しているクライアント コンピューターを構成するための netsh コマンドが提供されています。

ほとんどの場合、netsh コマンドでは、各ネットワーク サーバーの役割またはネットワーク機能に対して Microsoft 管理コンソール \(MMC\) スナップインを使用する場合に利用できるのと同じ機能が提供されます。 たとえば、NPS MMC スナップインを使用するか、**netsh nps** コンテキストで netsh コマンドを使用することで、ネットワーク ポリシー サーバー \(NPS\) を構成できます。

さらに、Windows Server で MMC スナップインとして使用できない、IPv6、ネットワーク ブリッジ、リモート プロシージャ コール \(RPC\) などのネットワーク テクノロジ用の netsh コマンドがあります。

>[!IMPORTANT]
>[Windows Server 2016 と Windows 10](https://technet.microsoft.com/library/mt156917.aspx) でネットワーク テクノロジを管理するには、Network Shell ではなく Windows PowerShell を使用することをお勧めします。 ただし、Network Shell はスクリプトとの互換性のために提供されており、その使用はサポートされています。

## <a name="network-shell-netsh-technical-reference"></a>Network Shell (netsh) テクニカル リファレンス

Netsh テクニカル リファレンスでは、netsh コマンドの構文、パラメーター、例を含む包括的な netsh コマンド リファレンスが提供されています。 Netsh テクニカル リファレンスを使用して、Windows Server 2016 と Windows 10 を実行しているコンピューターで、ネットワーク テクノロジをローカルまたはリモートで管理するための netsh コマンドを使用して、スクリプトとバッチ ファイルを作成できます。  
  
### <a name="content-availability"></a>コンテンツの利用可能性  
  
Network Shell テクニカル リファレンスは、TechNet ギャラリーから Windows ヘルプの \(*.chm\) 形式でダウンロードできます。[Netsh テクニカル リファレンス](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
