---
title: "AD フォレストの回復 - 問題の識別"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 1e9ede12dade0b5f1149eae784620520a8866e30
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="identify-the-problem"></a>問題を特定します。

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:
  
 フォレスト全体の障害の兆候が表示されたらなど、イベント ログまたはその他の監視ソリューションでは、エラーの原因を特定の Microsoft サポートを操作し、任意の考えられる救済策を評価します。  
 
## <a name="examples-of-forest-wide-failures"></a>フォレスト全体の障害の例 
  
-   すべての Dc を論理的に破損またはポイント ビジネス継続性が可能なではないことに物理的に損傷されています。たとえば、AD DS に依存しているすべてのビジネス アプリケーションが機能しません。  
  
-   悪意のある管理者には、Active Directory 環境が侵害されます。  
  
-   攻撃者は、意図的に、または管理者誤って — フォレスト全体でデータの破損を分散するスクリプトを実行します。  
  
-   攻撃者は、意図的に — または管理者誤って — 競合している、または悪意のある変更を Active Directory スキーマを拡張します。  
  
-   Dc 上の悪意のあるソフトウェアをインストールする攻撃者が管理対象し、するが知らされていた Microsoft サポートによって、フォレストをバックアップから復元します。  
  
    > [!IMPORTANT]
    >  このホワイト ペーパーでは、セキュリティの推奨事項をハッキングまたはセキュリティが侵害されたフォレストを回復する方法については説明しません。 一般に、することが推奨フォロー-Pass-the-hash 軽減手法環境を強化するためにします。 詳細については、次を参照してください。[Mitigating-Pass-the-hash (PtH) 攻撃とその他の資格情報窃盗手法](https://www.microsoft.com/download/details.aspx?id=36036)します。  
  
-   レプリケーション パートナーと none Dc の複製できます。  
  
-   任意のドメイン コントローラーでの AD DS に変更することはできません。  
  
-   任意のドメインに新しい Dc をインストールすることはできません。  
  
## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
