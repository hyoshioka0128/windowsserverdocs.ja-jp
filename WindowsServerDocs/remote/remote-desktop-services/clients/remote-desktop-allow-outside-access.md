---
title: リモート デスクトップでのネットワークの外部からコンピューターへのアクセスを許可します。
description: PC のネットワークの外部から PC をリモートでアクセスするためのオプションについてください。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: haley-rowland
manager: dongill
ms.author: elizapo
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: d77c362d9d06b70ad0747002ed8853a39e05b7ff
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1708660"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>リモート デスクトップに、PC のネットワークの外部からコンピューターへのアクセスを許可します。

>Windows 10、Windows Server 2016 に適用されます。

PC に接続するには、「リモート デスクトップ クライアントを使用して、とピア ツー ピア接続を作成します。 これは、場合、(「ホスト」とも呼ばれます) の PC に直接アクセスする必要があります。 PC がで実行されているネットワークの外部でから PC に接続する必要がある場合は、そのアクセスを有効にする必要があります。 いくつかのオプションがある: ポート転送を使用するか、vpn 接続を設定します。

## <a name="enable-port-forwarding-on-your-router"></a>ルーターのポート転送を有効にします。

ポート転送ポート、およびアクセスする PC の IP アドレスをルーターの IP アドレス (自分のパブリック IP) のポートを割り当てます。 

ポート転送を有効にする手順は、手順については、ルーターのオンライン検索する必要がありますのでを使っているルーターとは異なります。 手順の概要については、確認[のポート転送の設定をルーターに wikiHow](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)してください。

ポートをマップする前に、次の必要があります。

- PC の内部 IP アドレス: ファイルの場所**設定 > ネットワークとインターネット > 状態 >、ネットワークのプロパティを表示する**します。 「運用」状態で、ネットワークの構成を見つけて、[ **IPv4 アドレス**を取得します。

   ![運用ネットワークの構成](../media/rdclient-operational-network.png)

- パブリック IP アドレス (ルーターの IP)。 検索対象のさまざまな方法があります: (Bing や Google) で"IP 自分"を検索する (Windows 10) の[Wi-fi ネットワークのプロパティ](https://binged.it/2Gwob34)を表示します。
- ポート番号が割り当てられます。 ほとんどの場合、これは 3389 - リモート デスクトップ接続で使用される既定のポートです。
- ルーターへのアクセスを管理します。  

   >[!WARNING]
   > インターネットに PC を開こうとしている - 強力なパスワード PC の設定があるかどうかを確認します。

ポートを割り当てた後は、ルーター (上で 2 番目の箇条書き) のパブリック IP アドレスに接続して、ホスト PC からローカル ネットワークの外部に接続することができます。

ルーターの IP アドレスを変更することができます:、インターネット サービス プロバイダー (ISP) 割り当てることができますが、新しい IP いつでもします。 この問題を回避する動的な DNS の使用を検討してください:、覚えやすい IP アドレスではなく、ドメイン名を使用して PC に接続できます。 ルーター自動的に更新 DDNS サービスと新しい IP アドレスを変更する必要があります。

ほとんどのルーターことができますが、ポートのマッピングに使用する送信元 ip アドレスまたはネットワークのソースを定義できます。 勤務先から接続しようとしているのみがわかっている場合は、作業ネットワークでの IP アドレスを追加できるように、できる全体のパブリック インターネットへのポートを開かないでください。 ホストを使用して接続するには、動的 IP アドレスが使用されている場合は、ISP 特定の範囲全体からのアクセスを許可するソースの制限を設定します。

検討する[静的 IP アドレス](/windows-hardware/customize/mobile/mcsf/enable-static-ip)を設定 PC の内部の IP アドレスを変更しないようにします。 [ルーターの操作を行う場合、正しい IP アドレスにポート転送いちます。


## <a name="use-a-vpn"></a>VPN を使用します。

仮想プライベート ネットワーク (VPN) を使用して、[ローカル エリア ネットワークに接続する場合は、パブリック インターネットに PC を開く必要はありません。 代わりに、VPN に接続するとき、RD クライアントは、同じネットワークの一部である、PC にアクセスできるように機能します。 いくつか VPN サービスの利用可能な - を検索し、自分に最適方を使用できます。