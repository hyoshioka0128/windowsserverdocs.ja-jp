---
title: BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 414f28c72817e91c56c91b6fd6acbb48e786cbd8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971929"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックの情報を使用して、サードパーティ製のファイアウォール製品を構成し、BranchCache を分散キャッシュモードで実行できるようにするファイアウォール規則を使用してクライアントコンピューターを手動で構成することができます。

> [!NOTE]
> -   グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、手動でクライアント コンピューターに適用されるポリシーの構成をオーバーライドします。
> -   DirectAccess を使用して BranchCache を展開した場合は、このトピックの設定を使用して、BranchCache トラフィックを許可する IPsec 規則を構成できます。

これらの構成を変更するには、 **Administrators**のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS PCCRD]: ピアコンテンツのキャッシュと取得の検出プロトコル
分散キャッシュクライアントは、受信および送信の MS PCCRD トラフィックを許可する必要があります。これは、Web サービスの動的検出 (WS-ATOMICTRANSACTION) プロトコルで実行されます。

ファイアウォール設定では、受信トラフィックと送信トラフィックに加えて、マルチキャストトラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュモードのファイアウォール例外を構成できます。

IPv4 マルチキャスト: 239.255.255.250

IPv6 マルチキャスト: FF02:: C

受信トラフィック: ローカルポート: 3702、リモートポート: 短期

送信トラフィック: ローカルポート: 短期、リモートポート: 3702

プログラム:% systemroot% \system32\svchost.exe (BranchCache サービス [PeerDistSvc])

## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS PCCRR]: ピアコンテンツのキャッシュと取得: 取得プロトコル
分散キャッシュクライアントは、RFC (request for comments) 2616 に記載されているように、HTTP 1.1 プロトコルで伝送される、受信と送信の両方の MS PCCRR トラフィックを許可する必要があります。

ファイアウォール設定では、受信トラフィックと送信トラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュモードのファイアウォール例外を構成できます。

受信トラフィック: ローカルポート:80、リモートポート: 短期

送信トラフィック: ローカルポート: 短期、リモートポート:80



