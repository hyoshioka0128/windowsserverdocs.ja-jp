---
title: BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 288865f0237969e0bed7e105f8d539759984275e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834773"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>BranchCache トラフィックを許可するように非ドメイン メンバーのファイアウォール規則を構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックの情報を使用するには、サード パーティ製のファイアウォール製品を構成して、BranchCache 分散キャッシュ モードで実行を許可するファイアウォール規則を手動でクライアント コンピューターを構成します。  
  
> [!NOTE]  
> -   グループ ポリシーを使用して、BranchCache クライアント コンピューターを構成している場合、グループ ポリシー設定は、手動でクライアント コンピューターに適用されるポリシーの構成をオーバーライドします。  
> -   BranchCache と DirectAccess を展開している場合は、BranchCache トラフィックを許可する IPsec 規則を構成するには、このトピックで、設定を使用できます。  
  
メンバーシップ**管理者**、または同等が最低限の構成の変更に必要です。  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>MS-PCCRD:ピア コンテンツのキャッシュと探索プロトコルの取得  
分散キャッシュ クライアントは、Web Services Dynamic Discovery (Ws-discovery) プロトコルで実行されて受信と送信の MS PCCRD トラフィックを許可する必要があります。  
  
ファイアウォールの設定は、受信および送信トラフィックだけでなく、マルチキャスト トラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュ モードのファイアウォール例外を構成することができます。  
  
IPv4 マルチキャスト:239.255.255.250  
  
IPv6 マルチキャスト:FF02::C  
  
トラフィックを受信するには。ローカル ポート:3702、リモート ポート: 一時的な  
  
送信トラフィックは:ローカル ポート: 短期、リモートのポート。3702  
  
プログラム: %systemroot%\system32\svchost.exe (BranchCache サービス [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>MS-PCCRR:ピア コンテンツのキャッシュと検索機能:取得プロトコル  
分散キャッシュ クライアントは、要求のコメント (RFC) 2616 に記載されている HTTP 1.1 プロトコルでは実行受信と送信の MS PCCRR トラフィックを許可する必要があります。  
  
ファイアウォールの設定は、受信および送信トラフィックを許可する必要があります。 次の設定を使用して、分散キャッシュ モードのファイアウォール例外を構成することができます。  
  
トラフィックを受信するには。ローカル ポート:リモート ポートを 80、: 一時的な  
  
送信トラフィックは:ローカル ポート: 短期、リモートのポート。80  
  


