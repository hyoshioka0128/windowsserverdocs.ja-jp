---
title: "AD フォレストの回復 - フォレストを復元するための手順"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 29988c262897649173e039cc052bb64f38a1a0ca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
#<a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD フォレストの回復 - フォレストを復元するための手順 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

このセクションでは、フォレストを回復するための推奨パスの概要を示します。 フォレストの回復の手順については、後で詳しく説明します。  
  
 次の一覧は、大まかに言えば、回復の手順をまとめたものです。  
  
1.  [問題を特定します。](AD-Forest-Recovery-Identify-the-Problem.md)  
  
     連携 IT およびマイクロソフト サポートの問題と考えられる原因は、スコープを決定して、すべてのビジネス利害関係者と考えられる解決策を評価します。 合計フォレストの回復は多くの場合、最後のオプションをする必要があります。  
  
2.  [フォレストを回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)  
  
     手順完全な暫定版を準備することを決定したらフォレストの回復が必要である、:、現在のフォレストの構造を判断し、各ドメイン コントローラーを実行する、どの DC を決定するドメインごとに復元し、書き込み可能なすべての Dc がオフラインにすることを確認する関数を指定します。  
  
3.  [初期の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
  
     、個別に、ドメインごとに 1 つの DC の回復、クリーンアップ、およびドメインを再接続します。 特権のアカウントをリセットし、このフェーズでは、セキュリティ侵害によって発生する問題を修正します。  
  
4.  [残りの Dc を再展開します。](AD-Forest-Recovery-Restore-Additional-DCs.md)  
  
     障害発生前に、の状態に戻りますフォレストを再展開します。 この手順は、特定の設計や要件に合わせて調整する必要があります。 仮想化ドメイン コントローラーの複製には、このプロセスを迅速化できます。  
  
5.  [クリーンアップ](AD-Forest-Recovery-Cleanup.md)  
  
     機能を復元した後、必要に応じて名前解決を再構成し、LOB アプリケーションの動作を取得します。  

  
 このガイドの手順は、危険なデータを回復したフォレストに再挿入される可能性を最小限に設計されています。 などの要因を考慮する手順を変更する必要があります。  
  
-   スケーラビリティ  
-   リモート管理の容易性  
-   回復の速度  

