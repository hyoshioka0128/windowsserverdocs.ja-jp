---
title: AD フォレストの回復 - 考案、AD フォレストの回復計画
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adds
ms.openlocfilehash: edfc874fe030c6394bc8bda95c49e61951e78f43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881783"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>AD フォレストの回復 - 考案、AD フォレストの回復計画

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

環境やビジネス要件によっては、可能性があります。 または成功したフォレストの回復を実行するには、このガイドで説明されているすべての手順を実行する必要はありません。 このガイドでは、フォレストの回復用のテンプレートとしてのみ、ある環境に適したをビジネス ニーズを満たすカスタム フォレスト回復の計画を考案する必要があります。  
  
たとえば、フォレスト回復計画で、フォレストの詳細なトポロジ マップが必要です。 マップには、名前、そのロールとバックアップの状態間の信頼関係など、Dc の情報がすべてが一覧表示します。 トポロジ マップの作成に使用できるツールを参照してください。 [Microsoft Active Directory トポロジ Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380)します。  
  
1 年間に少なくとも 1 回フォレスト復旧計画を練習する必要があります。 または、Enterprise Admins または Domain Admins グループにメンバーシップの変更がある場合に、フォレストの回復ドリルを実行することをお勧めします。 これにより、情報技術 (IT) スタッフがフォレストの復旧計画を完全に理解していることを確認できます。

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
