---
title: AD フォレストの回復 - マルチ ドメイン フォレストで 1 つのドメインの回復
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adfs
ms.openlocfilehash: 3a1c9d0671a732eee83aa707e061afdbbf106fa5
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2018
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD フォレストの回復 - マルチ ドメイン フォレストで 1 つのドメインの回復

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

フォレストのフル回復ではなく、複数のドメインがあるフォレスト内で 1 つのドメインだけを回復するために必要な場合もあります。 このトピックでは、1 つのドメインとの回復可能な戦略の回復に関する考慮事項について説明します。  
  
 1 つのドメインの回復は、グローバル カタログ (GC) サーバーを再構築できる一意のチャレンジを表示します。 たとえば、最初のドメイン コントローラー (DC)、ドメインがフォレストの他のすべての Gc が、1 週間前に、作成したバックアップから復元された場合は、復元されたドメイン コントローラーよりもそのドメインの多くの最新の状態データがあります。 GC データの整合性を再確立するには、いくつかのオプションがあります。  
  
-   Unhost し、同時に復元されたドメインで、ものを除き、フォレスト内のすべての Gc から復元されたドメイン パーティションを再ホストします。  
  
-   ドメインを回復するフォレストの回復プロセスに従い、他のドメイン内の Gc から残留オブジェクトを削除します。  
  
 次のセクションでは、各オプションの一般的な考慮事項を提供します。 異なる Active Directory 環境での回復を実行する必要がある手順の完全なセットが異なります。  
  
## <a name="rehost-all-gcs"></a>すべての Gc の再ホストします。  

> [!WARNING]
>  すべてのドメインのドメイン管理者アカウントのパスワードは、問題を GC ログオンのアクセスを防止する場合に使用できる状態である必要があります。  

 すべての Gc の再ホストを行う repadmin/unhost と repadmin/rehost コマンドを使用して (repadmin の一部 /experthelp)。 Repadmin コマンドを実行する各ドメインは復元されませんに毎回の GC でします。 必要があることを確認する、すべて Gc 保持しない、復元されたドメインのコピーされなくなります。 これを実現するには、unhost ドメイン パーティション最初にすべてのドメイン コントローラーからなしに復旧のすべてのドメイン、フォレストの間で最初にします。 すべての Gc にはパーティションが含まれて、もはや後、は、再ホストすることができます。 再ホスト、たとえば、フォレストのサイト構造とレプリケーション構造を検討してください、完了前に、そのサイトの他の Dc を再ホスト サイトあたり 1 つの DC の再ホストされます。  
  
 このオプションは利用をドメインごとに、いくつかドメイン コントローラのみを持つ小規模な組織の効率的です。 Gc がすべて金曜日の夜に再構築されます。また、すべて読み取り専用のドメインの完全なレプリケーションがパーティション月曜日の午前中の前に、必要に応じて。 世界各地のサイトをカバーする大規模なドメインを回復する場合は、すべて Gc の読み取り専用ドメイン パーティションを再ホスト他のドメインのことが大幅にへの影響の操作可能性のあるダウンタイムが必要です。  
  
## <a name="remove-lingering-objects"></a>残留オブジェクトを削除します。  
 フォレストの回復プロセスと同様に、1 つの DC バックアップから復元する回復、残りの Dc のメタデータ クリーンアップを実行し、ドメインを構築するための AD DS を再インストールする必要のあるドメインにします。 その他のすべてのドメイン、フォレスト内の Gc では、復元されたドメインの読み取り専用のパーティションの残留オブジェクトを削除します。  
  
 残留オブジェクトのクリーンアップのソースは、復元されたドメインの DC である必要があります。 ソース DC の任意のドメイン パーティションの残留オブジェクトがないことを特定するには、GC れていた場合、グローバル カタログを削除することができます。  
  
 残留オブジェクトの削除は、大規模な組織の停止時間の他のオプションに関連するリスクを回避便利です。  
  
 詳細については、次を参照してください。[残留オブジェクトを削除する使用 Repadmin](https://technet.microsoft.com/library/cc785298.aspx)します。

## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
-   [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)  
