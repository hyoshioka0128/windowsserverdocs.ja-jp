---
title: RADIUS トラフィック用にファイアウォールを構成する
description: このトピックでは、Windows Server 2016 でネットワーク ポリシー サーバーの RADIUS トラフィックを許可するようにファイアウォールを構成する方法の概要を示します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 58cca2b2-4ef3-4a09-a614-8bdc08d24f15
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 94b03349f21a40f9bf42508d5a2878a5cf2946cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819453"
---
# <a name="configure-firewalls-for-radius-traffic"></a>RADIUS トラフィック用にファイアウォールを構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

許可またはブロックして、コンピューターまたはファイアウォールが実行されているデバイスからの IP トラフィックの種類には、ファイアウォールを構成することができます。 ファイアウォールが RADIUS クライアント間の RADIUS トラフィックを許可して正しく構成されていない場合、ユーザーがネットワーク リソースにアクセスできなく、RADIUS プロキシ、および RADIUS サーバー、ネットワーク アクセスの認証がフェールバックできます。 

2 つの種類の RADIUS トラフィックを許可するファイアウォールを構成する必要があります。

- ネットワーク ポリシー サーバー (NPS) を実行しているローカル サーバーのセキュリティが強化された Windows Defender ファイアウォール。
- 他のコンピューターまたはハードウェア デバイスで実行されているファイアウォールします。

## <a name="windows-firewall-on-the-local-nps"></a>ローカル NPS 上の Windows ファイアウォール

既定では、NPS が送信し、ユーザー データグラム プロトコルを使用して RADIUS トラフィックを受け取る\(UDP\)ポート 1812、1813、1645、および 1646 します。 NPS 上の Windows Defender ファイアウォールは、送受信をこの RADIUS トラフィックを許可する、NPS のインストール時に自動的に、例外で構成されます。

そのため、既定の UDP ポートを使用している場合と NPSs の間の RADIUS トラフィックを許可する Windows Defender ファイアウォールの構成を変更する必要はありません。

場合によっては、NPS が RADIUS トラフィックに使用するポートを変更する可能性があります。 既定値以外のポートで RADIUS トラフィックを送受信するには、NPS とネットワーク アクセス サーバーを構成する場合は、次の操作を行う必要があります。

- 既定のポートで RADIUS トラフィックを許可する例外を削除します。
- 新しいポートで RADIUS トラフィックを許可する例外を作成します。

詳細については、次を参照してください。 [NPS UDP ポート情報の構成](nps-udp-ports-configure.md)します。

## <a name="other-firewalls"></a>その他のファイアウォール

最も一般的な構成でファイアウォールがインターネットに接続されているし、NPS は、境界ネットワークに接続されているイントラネット リソース。

イントラネット内のドメイン コント ローラーに到達、NPS が必要があります。

- 境界ネットワークとイントラネット上のインターフェイスのインターフェイス (IP ルーティングが有効でない)。 
- 境界ネットワーク上の 1 つのインターフェイス。 この構成では、NPS は、イントラネット境界ネットワークに接続する別のファイアウォールを介したドメイン コント ローラーと通信します。

## <a name="configuring-the-internet-firewall"></a>インターネット ファイアウォールを構成します。

インターネット インターフェイスでの入力と出力のフィルターを使用して、インターネットに接続されているファイアウォールを構成する必要があります\(と、必要に応じて、ネットワーク境界インターフェイス\)NPS 間の RADIUS メッセージの転送を許可するにはRADIUS クライアントまたはインターネット上のプロキシ。 Web サーバー、VPN サーバー、およびその他の種類のサーバーを境界ネットワーク上のトラフィックの通過を許可する追加のフィルターを使用できます。

個別に入力と出力のパケット フィルターをインターネット インターフェイスと境界ネットワーク インターフェイスに構成できます。

### <a name="configure-input-filters-on-the-internet-interface"></a>インターネット インターフェイス上の入力フィルターを構成します。

次の種類のトラフィックを許可するファイアウォールのインターネット インターフェイス上には、次の入力パケット フィルターを構成します。

- UDP 宛先ポート 1812 (0x714)、NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。  このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS 認証トラフィックを許可します。 これは、RFC 2865 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1812 をそのポート番号に置き換えてください。
- UDP 宛先ポート 1813 (0x715)、NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS アカウンティング トラフィックを許可します。 これは、RFC 2866 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1813 をそのポート番号に置き換えてください。
- \(省略可能な\)UDP 宛先ポート 1645、境界領域ネットワーク インターフェイスの宛先 IP アドレス\(0x66D\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS 認証トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。
- \(省略可能な\)UDP 宛先ポート 1646、境界領域ネットワーク インターフェイスの宛先 IP アドレス\(0x66E\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS アカウンティング トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。

### <a name="configure-output-filters-on-the-internet-interface"></a>インターネット インターフェイス上の出力フィルターを構成します。

次の種類のトラフィックを許可するファイアウォールのインターネット インターフェイス上には、次の出力フィルターを構成します。

- 1812 (0x714)、NPS の UDP 発信元ポート、境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS 認証トラフィックを許可します。 これは、RFC 2865 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1812 をそのポート番号に置き換えてください。
- 1813 (0x715)、NPS の UDP 発信元ポート、境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS アカウンティング トラフィックを許可します。 これは、RFC 2866 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1813 をそのポート番号に置き換えてください。
- \(省略可能な\)UDP 発信元ポート 1645、境界領域ネットワーク インターフェイスの発信元 IP アドレス\(0x66D\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS 認証トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。
- \(省略可能な\)UDP 発信元ポート 1646、境界領域ネットワーク インターフェイスの発信元 IP アドレス\(0x66E\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS アカウンティング トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。

### <a name="configure-input-filters-on-the-perimeter-network-interface"></a>境界ネットワーク インターフェイス上の入力フィルターを構成します。

次の種類のトラフィックを許可するファイアウォールの境界ネットワーク インターフェイス上には、次の入力フィルターを構成します。

- 1812 (0x714)、NPS の UDP 発信元ポート、境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS 認証トラフィックを許可します。 これは、RFC 2865 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1812 をそのポート番号に置き換えてください。
- 1813 (0x715)、NPS の UDP 発信元ポート、境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS アカウンティング トラフィックを許可します。 これは、RFC 2866 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1813 をそのポート番号に置き換えてください。
- \(省略可能な\)UDP 発信元ポート 1645、境界領域ネットワーク インターフェイスの発信元 IP アドレス\(0x66D\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS 認証トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。
- \(省略可能な\)UDP 発信元ポート 1646、境界領域ネットワーク インターフェイスの発信元 IP アドレス\(0x66E\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントに、NPS から RADIUS アカウンティング トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。

### <a name="configure-output-filters-on-the-perimeter-network-interface"></a>境界ネットワーク インターフェイス上の出力フィルターを構成します。

次の種類のトラフィックを許可するファイアウォールの境界領域ネットワーク インターフェイスでは、次の出力パケット フィルターを構成します。

- UDP 宛先ポート 1812 (0x714)、NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS 認証トラフィックを許可します。 これは、RFC 2865 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1812 をそのポート番号に置き換えてください。
- UDP 宛先ポート 1813 (0x715)、NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS アカウンティング トラフィックを許可します。 これは、RFC 2866 で定義されている、NPS で使用される既定の UDP ポートです。 別のポートを使用している場合は、1813 をそのポート番号に置き換えてください。
- \(省略可能な\)UDP 宛先ポート 1645、境界領域ネットワーク インターフェイスの宛先 IP アドレス\(0x66D\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS 認証トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。
- \(省略可能な\)UDP 宛先ポート 1646、境界領域ネットワーク インターフェイスの宛先 IP アドレス\(0x66E\) NPS の。 このフィルターは、インターネット ベースの RADIUS クライアントから、NPS を RADIUS アカウンティング トラフィックを許可します。 これは、古い RADIUS クライアントで使用される UDP ポートです。

セキュリティ強化のためには、境界ネットワーク上のクライアントと NPS の IP アドレス間のトラフィック フィルターを定義する、ファイアウォールを介してパケットを送信する各 RADIUS クライアントの IP アドレスを使用することができます。

### <a name="filters-on-the-perimeter-network-interface"></a>境界ネットワーク インターフェイスに基づくフィルター

次の種類のトラフィックを許可するためのイントラネット ファイアウォールの境界ネットワーク インターフェイス上には、次の入力パケット フィルターを構成します。

- NPS の境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、境界ネットワーク上の NPS からのトラフィックを許可します。

次の種類のトラフィックを許可するためのイントラネット ファイアウォールの境界ネットワーク インターフェイス上には、次の出力フィルターを構成します。

- NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。 このフィルターは、境界ネットワーク上の NPS にトラフィックを許可します。

### <a name="filters-on-the-intranet-interface"></a>イントラネット インターフェイス上のフィルター

次の種類のトラフィックを許可するファイアウォールのイントラネット インターフェイス上には、次の入力フィルターを構成します。

- NPS の境界領域ネットワーク インターフェイスの宛先 IP アドレス。 このフィルターは、境界ネットワーク上の NPS にトラフィックを許可します。

次の種類のトラフィックを許可するファイアウォールのイントラネット インターフェイス上には、次の出力パケット フィルターを構成します。

- NPS の境界領域ネットワーク インターフェイスの発信元 IP アドレス。 このフィルターは、境界ネットワーク上の NPS からのトラフィックを許可します。


NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。




