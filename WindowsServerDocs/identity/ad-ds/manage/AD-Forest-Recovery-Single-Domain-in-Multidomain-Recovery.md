---
title: AD フォレストの回復 - マルチ ドメイン フォレストで 1 つのドメインを回復します。
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adds
ms.openlocfilehash: fae2cc40af0b43dd38d72c2622720a6bb17b0a66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863473"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD フォレストの回復 - マルチ ドメイン フォレストで 1 つのドメインを回復します。

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

完全なフォレストの回復ではなく、複数のドメインを持つフォレスト内で 1 つのドメインのみを回復するために必要な場合もあります。 このトピックでは、1 つのドメインと回復を実行できる方法の回復に関する考慮事項について説明します。  
  
1 つのドメインの回復は、グローバル カタログ (GC) サーバーを再構築のために独特の課題を表示します。 たとえば、ドメインの最初のドメイン コントローラ (DC) が、フォレスト内の他のすべての Gc 1 週間前に作成されたバックアップから復元した場合より、復元された DC をそのドメインの多くの最新の状態データがあります。 GC データの整合性を再確立するには、いくつかのオプションがあります。  
  
- Unhost し、し、同時に復旧のドメインを除く、フォレスト内のすべての Gc から回復したドメイン パーティションを再ホストします。  
- ドメインを回復するフォレストの回復プロセスに従うし他のドメイン内の Gc から残留オブジェクトを削除します。  
  
次のセクションでは、各オプションの一般的な考慮事項を提供します。 異なる Active Directory 環境での回復を実行する必要がある手順の完全なセットが異なります。  
  
## <a name="rehost-all-gcs"></a>すべての Gc をリホストします。  

> [!WARNING]
> すべてのドメインのドメイン管理者アカウントのパスワードは、問題を GC ログオンのアクセスを防止する場合に使用できる状態である必要があります。  

Gc がすべてのホスト変更を行うことができます repadmin を使用して/unhost とかかるコマンドの repadmin (repadmin/experthelp の一部)。 復旧されていない各ドメインでは、各 GC の repadmin コマンドを実行するとします。 必要なられないようにする Gc がすべて保持しない回復したドメインのコピーできなくなります。 これを実現するには、unhost ドメイン パーティション最初すべてのドメイン コント ローラーからなしに復旧のすべてのドメイン、フォレストの間で最初にします。 すべての Gc では、パーティションをもはや含まない後、は、再ホストすることができます。 、再ホストするときは、たとえば、フォレストのサイト構造とレプリケーション構造を検討してください、そのサイトの他の Dc を再ホストする前に、サイトごとの 1 つの DC の再ホストが終了されます。  
  
このオプションは、ドメインごとに、いくつかドメイン コントローラのみを含む小規模な組織にとって得策です。 金曜日の夜に Gc がすべて再構築する可能性があり、月曜日の朝の前に必要に応じて、すべて読み取り専用のドメインの完全なレプリケーションがパーティション分割します。 世界規模でサイトをカバーする大規模なドメインを回復する必要がある場合すべて Gc の読み取り専用のドメイン パーティションを再ホストの他のドメインを利用する操作の影響は大幅に、可能性のあるダウン タイムが必要です。  
  
## <a name="remove-lingering-objects"></a>残留オブジェクトを削除します。

フォレストの回復プロセスと同様の回復で、残りの Dc のメタデータのクリーンアップを実行し、ドメインを構築するための AD DS を再インストールする必要のあるドメイン内のバックアップから 1 つの DC を復元します。 その他のすべてのドメイン、フォレスト内の Gc では、回復したドメインの読み取り専用のパーティションの残留オブジェクトを削除します。  

残留オブジェクトのクリーンアップのソースには、回復したドメインの DC を指定する必要があります。 ソース DC に任意のドメイン パーティションの残留オブジェクトがないことは、GC があった場合は、グローバル カタログを削除できます。  

残留オブジェクトの削除は、ダウンタイムの他のオプションに関連するリスクを回避する大規模な組織と便利です。  

詳細については、次を参照してください。[残留オブジェクトを削除する使用 Repadmin](https://technet.microsoft.com/library/cc785298.aspx)します。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)  
- [AD フォレストの回復 - カスタム フォレスト回復の計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復の問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復に回復する方法を決定](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復 - 最初の回復を実行します。](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
- [AD フォレストの回復 - よく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
- [AD フォレストの回復 - Multidomain フォレスト内の 1 つのドメインを回復します。](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD フォレストの回復 - Windows Server 2003 ドメイン コント ローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)  
