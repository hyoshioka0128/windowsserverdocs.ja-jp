---
title: "AD フォレストの回復 - 立てる、AD フォレストの回復の計画"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adfs
ms.openlocfilehash: 6754509ccac352895b9370e63adf1b69548953bf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>AD フォレストの回復 - 立てる、AD フォレストの回復の計画

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

お客様の環境とビジネス要件によっては、可能性があります。または成功したフォレストの回復を実行するには、このガイドで説明されているすべての手順を実行する必要はありません。 このガイドは、フォレストの回復用のテンプレートとしてのみ機能、その環境に適したし、ビジネス ニーズを満たすをカスタム フォレスト回復計画を立てることが重要です。  
  
 たとえば、フォレスト回復計画では、フォレストの詳細なトポロジ マップが必要です。 マップする必要があります、名前、それぞれの役割とバックアップ ステータス、およびそれらの間で信頼関係など、Dc の情報がすべて一覧表示されます。 トポロジ マップの作成に使用できるツールを参照してください。[Microsoft Active Directory トポロジ Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380)します。  
  
 フォレスト回復計画 1 年間に少なくとも 1 回を練習する必要があります。 またを Enterprise Admins グループまたは Domain Admins グループのメンバーシップの変更がある場合は、フォレスト回復ドリルを実行することをお勧めします。 これにより、お客様の情報技術 (IT) スタッフは、フォレストの回復計画を十分に理解することを確認します。

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
