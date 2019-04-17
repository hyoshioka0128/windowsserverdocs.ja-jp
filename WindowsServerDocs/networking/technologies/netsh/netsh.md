---
title: ネットワーク シェル (Netsh)
description: このトピックでは、Windows Server 2016 でのネットワーク シェル (netsh) コマンド ライン ユーティリティの概要を説明します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0a23d60bc3f181fee62ade105e546bbb7161c133
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh"></a>ネットワーク シェル \(Netsh\)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ネットワーク シェル (netsh) は、コマンド ライン ユーティリティを構成し、Windows Server 2016 を実行しているコンピューターにインストールされている後に、さまざまなネットワーク通信サーバーの役割およびコンポーネントのステータスを表示することができます。

>[!NOTE]
>このトピックに加え、次のネットワーク シェル コンテンツは使用できます。
>
> - [Netsh コマンドの構文、コンテキスト、および書式設定](netsh-contexts.md)
> - [ネットワーク シェル (Netsh) バッチ ファイルの例](netsh-wins.md)
> - [Netsh テクニカル リファレンス](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc) 

動的ホスト構成プロトコル \(DHCP\) クライアントと、BranchCache など、一部のクライアント テクノロジには、Windows 10 を実行しているクライアント コンピューターを構成するための netsh コマンドも提供します。

Netsh コマンドが Microsoft 管理コンソール \(MMC\) snap\ を使用する場合に使用できる同じ機能を提供するほとんどの場合、-の各ネットワークのサーバーの役割またはネットワーク機能します。 たとえば、NPS MMC スナップインまたはの netsh コマンドを使用してネットワーク ポリシー サーバー \(NPS\) を構成することができます、**netsh nps**コンテキスト。

さらは、ネットワーク テクノロジ用の netsh コマンドなど、IPv6、ネットワーク ブリッジ、およびリモート プロシージャ コール \(RPC\)、されない MMC スナップインとしての Windows Server で使用できます。

>[!IMPORTANT]
>ネットワーク テクノロジを管理する Windows PowerShell を使用することをお勧め[Windows Server 2016 および Windows 10](https://technet.microsoft.com/library/mt156917.aspx)ネットワーク シェルのではなく。 ネットワーク シェルは、スクリプトとの互換性ただし、およびその使用がサポートされています。

## <a name="network-shell-netsh-technical-reference"></a>ネットワーク シェル (Netsh) のテクニカル リファレンス

Netsh テクニカル リファレンスでは、構文、パラメーター、および用の netsh コマンドの例を含む包括的な netsh コマンドのリファレンスを提供します。 Netsh テクニカル リファレンスを使用して、ネットワーク テクノロジと Windows 10 の Windows Server 2016 を実行しているコンピューター上のローカルまたはリモート管理用の netsh コマンドを使用して、スクリプトやバッチ ファイルを作成することができます。  
  
### <a name="content-availability"></a>コンテンツの可用性  
  
ネットワーク シェル テクニカル リファレンスは、TechNet ギャラリーから Windows ヘルプ \(*.chm\) 形式でダウンロード可能な: [Netsh テクニカル リファレンス](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  

