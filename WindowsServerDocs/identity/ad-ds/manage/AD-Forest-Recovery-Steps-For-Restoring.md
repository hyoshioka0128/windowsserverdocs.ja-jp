---
title: AD フォレストの回復-フォレストを復元する手順
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 07a043c4361f8eaae30b1dea665c604c0df42333
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390290"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD フォレストの回復-フォレストを復元する手順

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

このセクションでは、フォレストを回復するために推奨されるパスの概要について説明します。 フォレストの回復手順については、後で詳しく説明します。  
  
次の一覧は、高レベルでの回復手順をまとめたものです。  
  
1. [問題を特定する](AD-Forest-Recovery-Identify-the-Problem.md)  

   それを使用 Microsoft サポートして問題と考えられる原因の範囲を特定し、ビジネス上のすべての関係者との考えられる救済策を評価します。 多くの場合、フォレスト全体の回復は最後のオプションである必要があります。  
  
2. [フォレストを回復する方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)  

   フォレストの回復が必要であると判断したら、準備するための準備手順を完了します。現在のフォレストの構造を確認し、各 DC が実行する機能を特定し、各ドメインについて復元する DC を決定し、書き込み可能なすべての Dc があることを確認します。オフラインになります。  

3. [初期回復の実行](AD-Forest-Recovery-Perform-initial-recovery.md)  

   [分離] で、ドメインごとに1つの DC を回復し、クリーンアップして、ドメインを再接続します。 このフェーズでは、特権アカウントをリセットし、セキュリティ違反によって発生する問題を修正します。  
  
4. [残りの Dc の再デプロイ](AD-Forest-Recovery-Restore-Additional-DCs.md)  

   フォレストを再展開して、エラーが発生する前の状態に戻します。 この手順は、特定の設計と要件に適合させる必要があります。 仮想化ドメインコントローラーの複製は、このプロセスを迅速化するのに役立ちます。  

5. [清掃](AD-Forest-Recovery-Cleanup.md)  

   機能が復元されたら、必要に応じて名前解決を再構成し、LOB アプリケーションを動作させることができます。  

このガイドの手順は、回復したフォレストに危険なデータを再導入可能性を最小限に抑えるように設計されています。 次のような要因を考慮して、これらの手順を変更しなければならない場合があります。  
  
- スケーラビリティ  
- リモート管理性  
- 回復速度  
