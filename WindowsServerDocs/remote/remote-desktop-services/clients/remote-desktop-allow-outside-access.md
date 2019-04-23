---
title: リモート デスクトップ - ネットワークの外部から PC へのアクセスを許可します。
description: PC のネットワークの外部から PC へのリモート アクセスするためのオプションについて説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888153"
---
# <a name="remote-desktop---allow-access-to-your-pc-from-outside-your-pcs-network"></a>リモート デスクトップ - お客様の PC のネットワークの外部から PC へのアクセスを許可します。

>適用先:Windows 10、Windows Server 2016

リモート デスクトップ クライアントを使用して、PC に接続するときは、ピア ツー ピア接続を作成しています。 これは、("host"とも呼ばれます)、PC に直接アクセスする必要があることを意味します。 お使いの PC がで実行されているネットワークの外部から PC に接続する必要がある場合は、そのアクセスを有効にする必要があります。 いくつかの選択肢がある: ポート フォワーディングを使用して、または VPN を設定します。

## <a name="enable-port-forwarding-on-your-router"></a>ルーターでポート フォワーディングを有効にします。

ポート フォワーディングは単に、ポートと IP アドレスにアクセスする PC のルーターの IP アドレス (パブリック IP) のポートをマップします。 

手順については、ルーターのオンラインで検索する必要がありますので、ポート フォワーディングを有効にするための特定の手順は、ルーターを使用するいるとは異なります。 手順の概要については、チェック アウト[をポート転送の設定、ルーター上に wikiHow](https://www.wikihow.com/Set-Up-Port-Forwarding-on-a-Router)します。

ポートをマップする前に、次のとおりです。

- PC の内部 IP アドレス:検索対象**設定 > ネットワークとインターネット > ステータス >、ネットワークのプロパティを表示**します。 「操作」状態でネットワーク構成を検索し、取得、 **IPv4 アドレス**します。

   ![運用ネットワークの構成](../media/rdclient-operational-network.png)

- パブリック IP アドレス (ルーターの IP)。 これを特定する方法はたくさんあります - (Bing や Google) で"my IP"を検索できますしたり表示したり、 [Wi-fi ネットワークのプロパティ](https://binged.it/2Gwob34)(用 Windows 10)。
- マップされているポート番号。 ほとんどの場合、これは 3389 - リモート デスクトップ接続で使用される既定のポートです。
- ルーターへのアクセスを管理します。  

   >[!WARNING]
   > インターネットまで、PC を開いています - 強力なパスワードをお使いの PC の設定があるかどうかを確認します。

ポートをマップした後、ルーター (上記で 2 番目の箇条書き) のパブリック IP アドレスに接続することで、ローカル ネットワークの外部からホスト PC に接続することができます。

ルーターの IP アドレスを変更することができます -、インターネット サービス プロバイダー (ISP) が、いつでも新しい IP を割り当てます。 この問題を回避する動的 DNS の使用を検討 - に IP アドレスの代わりに、ドメイン名を覚えやすいを使用して、PC に接続できます。 ルーターを自動的に更新 DDNS サービス、新しい IP アドレスを変更する必要があります。

ほとんどのルーターでは、ポートのマッピングを使用できるはどの送信元 ip アドレスまたはソース ネットワークを定義できます。 ように、職場のネットワークでの IP アドレスを追加するには職場から接続しようとしているだけがわかっている場合を可能にする全体のパブリック インターネットにポートを開かないでください。 接続を使用しているホストが動的 IP アドレスを使用する場合は、その特定の ISP の範囲全体からアクセスを許可するソースの制限を設定します。

設定することも検討できます、[静的 IP アドレス](/windows-hardware/customize/mobile/mcsf/enable-static-ip)内部 IP アドレスが変更されないように、PC にします。 ルーターの後、操作を行う場合ポート フォワーディングが常に正しい IP アドレスをポイントします。


## <a name="use-a-vpn"></a>VPN を使用します。

仮想プライベート ネットワーク (VPN) を使用して、ローカル エリア ネットワークに接続する場合は、パブリック インターネットに PC を開く必要はありません。 代わりに、VPN に接続するときに、RD クライアントは、同じネットワークの一部と、PC にアクセスできるように機能します。 複数の VPN サービスがある使用可能な - を検索して使用する方に最適です。