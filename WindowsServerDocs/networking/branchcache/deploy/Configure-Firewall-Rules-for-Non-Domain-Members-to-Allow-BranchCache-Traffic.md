---
title: BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e5f744141efc35bb493bcd95fad53eafbbc3f78d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックの情報を使用するには、サード パーティ製のファイアウォール製品を構成して、BranchCache 分散キャッシュ モードで実行を許可するファイアウォール規則をクライアント コンピューターを手動で構成します。  
  
> [!NOTE]  
> -   グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、ポリシーが適用されるクライアント コンピューターが手動で構成をオーバーライドします。  
> -   DirectAccess で BranchCache を展開している場合このトピックの「BranchCache トラフィックを許可する IPsec 規則を構成する設定を使用することができます。  
  
メンバーシップ**管理者**、またはそれと同等がこれらの構成変更のために必要な最小値。  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS PCCRD]: ピアのコンテンツのキャッシングと取得検出プロトコル  
分散キャッシュ クライアントでは、Web Services Dynamic Discovery (Ws-discovery) プロトコルでは実行受信と送信の MS PCCRD トラフィックを許可する必要があります。  
  
ファイアウォールの設定は、受信と送信トラフィックに加えて、マルチキャスト トラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュ モードのファイアウォールの例外を構成することができます。  
  
IPv4 マルチキャスト: 239.255.255.250  
  
IPv6 マルチキャスト: FF02::C  
  
トラフィックを受信しますローカル ポート: 3702、リモート ポート: 短期。  
  
送信トラフィック: ローカル ポート: 一時的なリモート ポート: 3702  
  
プログラム: %systemroot%\system32\svchost.exe (BranchCache サービス [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS PCCRR]: ピアのコンテンツのキャッシングと取得: 取得プロトコル  
分散キャッシュ クライアントでは、コメント (RFC) 2616 の要求に記述されている HTTP 1.1 プロトコルでは実行受信と送信の MS PCCRR トラフィックを許可する必要があります。  
  
ファイアウォールの設定は、受信と送信トラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュ モードのファイアウォールの例外を構成することができます。  
  
トラフィックを受信しますローカル ポート: 80、リモート ポート: 短期。  
  
送信トラフィック: ローカル ポート: 一時的なリモート ポート: 80  
  


