---
title: AD フォレストの回復 - 問題の特定
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: cb3cf45f778ff305c8fe5aad5e23f0257650d6f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865523"
---
# <a name="identify-the-problem"></a>問題を特定します。

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2
  
フォレスト全体の障害の兆候が表示されたらなどのイベント ログまたは他の監視ソリューションでは、エラーの原因を特定する Microsoft サポートと協力し、任意の考えられる解決策を評価します。  

## <a name="examples-of-forest-wide-failures"></a>フォレスト全体の障害の例

- すべての Dc が論理的に破損またはビジネス継続性が可能であれば、ポイントに物理的に破損しているされました。たとえば、AD DS に依存するすべてのビジネス アプリケーションは機能しません。  
- 悪意のある管理者は、Active Directory 環境を侵害されました。  
- 攻撃者が意図的に- または管理者誤って: フォレスト間でデータの破損を分散するスクリプトを実行します。  
- 攻撃者が意図的に、または管理者誤って-悪意のある、または競合する変更を Active Directory スキーマを拡張します。  
- 攻撃者が Dc に悪意のあるソフトウェアをインストールする管理されているし、フォレストをバックアップから回復するは、Microsoft サポートから指摘されています。  
  
   > [!IMPORTANT]
   >  このホワイト ペーパーでは、ハッキングまたは侵害が済んでいるフォレストを回復する方法についてのセキュリティに関する推奨事項は含まれません。 一般に、お勧めに従って Pass the Hash 緩和方法を環境を強化します。 詳細については、次を参照してください。 [Mitigating-Pass-the-hash (PtH) 攻撃とその他の資格情報窃盗手法](https://www.microsoft.com/download/details.aspx?id=36036)します。
  
- レプリケーション パートナーと、Dc のいずれもレプリケートできます。  
- 任意のドメイン コント ローラーで AD DS に変更できません。  
- 任意のドメインに新しい Dc をインストールすることはできません。  
  
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
