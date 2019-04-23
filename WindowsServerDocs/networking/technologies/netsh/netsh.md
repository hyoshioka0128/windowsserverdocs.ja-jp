---
title: ネットワーク シェル (netsh)
description: このトピックでは、Windows Server 2016 でのネットワーク シェル (netsh) コマンド ライン ユーティリティの概要を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: 038b21783ef1d27619657ec3f9a472cf3caba68e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849363"
---
# <a name="network-shell-netsh"></a>ネットワーク シェル\(Netsh\)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ネットワーク シェル (netsh) を構成した後、Windows Server 2016 を実行しているコンピューターにインストールされているさまざまなネットワーク通信サーバーの役割およびコンポーネントのステータスを表示できるようにするコマンド ライン ユーティリティです。

動的ホスト構成プロトコルなど、いくつかのクライアント テクノロジ\(DHCP\)クライアントと BranchCache、Windows 10 を実行しているクライアント コンピューターを構成するための netsh コマンドが用意されています。

ほとんどの場合での netsh コマンドは、Microsoft 管理コンソールを使用するときに使用できる同じ機能を提供\(MMC\)スナップ\-で各ネットワークのサーバー ロールまたはネットワーク機能。 たとえば、ネットワーク ポリシー サーバーを構成できる\(NPS\) NPS MMC スナップインまたは netsh コマンドを使用して、 **netsh nps**コンテキスト。

さらに、ネットワーク テクノロジ用の netsh コマンドなどが IPv6 をネットワーク ブリッジ、およびリモート プロシージャ コールの\(RPC\)は、MMC スナップインとして Windows Server では使用できません。

>[!IMPORTANT]
>ネットワーク テクノロジを管理する Windows PowerShell を使用することをお勧め[Windows Server 2016 および Windows 10](https://technet.microsoft.com/library/mt156917.aspx)ネットワーク シェルではなく。 ネットワーク シェルは、スクリプトとの互換性ただしとその使用はサポートされています。

## <a name="network-shell-netsh-technical-reference"></a>ネットワーク シェル (Netsh) テクニカル リファレンス

Netsh テクニカル リファレンスでは、構文、パラメーター、および netsh コマンドの例を含む、包括的な netsh コマンド リファレンスを提供します。 Netsh テクニカル リファレンスを使用すると、Windows Server 2016 および Windows 10 を実行しているコンピューターでのネットワーク テクノロジのローカルまたはリモート管理用の netsh コマンドを使用して、スクリプトやバッチ ファイルをビルドします。  
  
### <a name="content-availability"></a>コンテンツの可用性  
  
ネットワーク シェル テクニカル リファレンスは、Windows のヘルプのダウンロード可能な\(*.chm\) TechNet ギャラリーからの形式。[Netsh テクニカル リファレンス](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
