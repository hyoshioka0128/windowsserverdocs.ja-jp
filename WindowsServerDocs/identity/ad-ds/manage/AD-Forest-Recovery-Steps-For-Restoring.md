---
title: AD フォレストの回復 - フォレストを復元する手順
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 1712d3a636160f82495539afdd42ab2ee85ffae2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861473"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD フォレストの回復 - フォレストを復元する手順

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

このセクションでは、フォレストを回復するための推奨パスの概要を示します。 フォレストの回復手順については、後で詳しく説明します。  
  
次の一覧は、高レベルの回復手順をまとめたものです。  
  
1. [問題を特定します。](AD-Forest-Recovery-Identify-the-Problem.md)  

   扱う IT とマイクロソフト サポートの問題と考えられる原因は、スコープを決定して、すべてのビジネスの利害関係者と考えられる解決策を評価します。 多くの場合は、最後のオプションが合計のフォレストの回復にあります。  
  
2. [フォレストを回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)  

   フォレストの回復が必要であるが決定したら、完了の暫定版の準備手順: 現在のフォレスト構造を決定する、各 DC を実行する、どの DC を決定するドメインごとに復元する関数を識別およびすべての書き込み可能 Dc ことを確認しますオフラインになります。  

3. [最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  

   分離ドメインごとに 1 つの DC を回復し、それらをクリーンアップして、ドメインを再接続します。 特権のアカウントをリセットし、このフェーズでセキュリティ侵害によって引き起こされる問題を修正します。  
  
4. [残りの Dc を再デプロイします。](AD-Forest-Recovery-Restore-Additional-DCs.md)  

   障害発生前に、の状態に戻すためのフォレストを再デプロイします。 この手順は、特定のデザインと要件に合わせて調整する必要があります。 仮想化ドメイン コント ローラーの複製は、このプロセスを高速化に役立ちます。  

5. [クリーンアップ](AD-Forest-Recovery-Cleanup.md)  

   機能が復元された後、必要に応じて、名前解決を再構成し、LOB アプリケーションの動作を取得します。  

危険なデータを回復したフォレストに再挿入される可能性を最小限に抑えるには、このガイドの手順が設計されています。 次の手順などの要因のアカウントを変更する必要があります。  
  
- スケーラビリティ  
- リモート管理の容易性  
- 迅速な回復  
