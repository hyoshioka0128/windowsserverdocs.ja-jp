---
title: AD フォレストの回復 - 問題の特定
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.openlocfilehash: 33a1febbdbe564873f8f7c0a4df474e933f09b92
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969899"
---
# <a name="identify-the-problem"></a>問題を特定する

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

イベントログやその他の監視ソリューションなど、フォレスト全体の障害の兆候が表示された場合は、Microsoft サポートを操作してエラーの原因を特定し、考えられる解決策を評価します。

## <a name="examples-of-forest-wide-failures"></a>フォレスト全体の障害の例

- すべての Dc が論理的に破損しているか、物理的に破損しているため、ビジネス継続性が不可能です。たとえば、AD DS に依存するすべてのビジネスアプリケーションは機能しません。
- 偽の管理者によって Active Directory 環境が侵害されました。
- 意図的に、または管理者が誤って、フォレスト全体でデータ破損を分散するスクリプトを実行します。
- 故意または管理者によって意図的に Active Directory スキーマが拡張され、悪意のあるまたは競合する変更が加えられます。
- 悪意のあるソフトウェアを Dc にインストールするために攻撃者によって管理されており、Microsoft サポートがバックアップからフォレストを回復することを推奨しています。

   > [!IMPORTANT]
   >  このホワイトペーパーでは、ハッキングまたは侵害されたフォレストを回復する方法に関するセキュリティ上の推奨事項については説明しません。 一般に、環境を強化するには、ハッシュの軽減対策手法に従うことをお勧めします。 詳細については、「 [PtH (パススルー) 攻撃とその他の資格情報の盗難手法](https://www.microsoft.com/download/details.aspx?id=36036)」を参照してください。

- どの Dc もレプリケーションパートナーとレプリケートすることはできません。
- どのドメインコントローラーでも、AD DS に変更を加えることはできません。
- 新しい Dc をどのドメインにもインストールすることはできません。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復 - 前提条件](AD-Forest-Recovery-Prerequisties.md)
- [AD フォレストの回復-カスタムフォレストの復旧計画の作成](AD-Forest-Recovery-Devising-a-Plan.md)
- [AD フォレストの回復-問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD フォレストの回復-回復方法を決定する](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD フォレストの回復-最初の回復を実行する](AD-Forest-Recovery-Perform-initial-recovery.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
- [AD フォレストの回復-よく寄せられる質問](AD-Forest-Recovery-FAQ.md)
- [AD フォレストの回復-マルチドメインフォレスト内の単一ドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)
- [AD フォレストの回復-Windows Server 2003 ドメインコントローラーを使用したフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md)
