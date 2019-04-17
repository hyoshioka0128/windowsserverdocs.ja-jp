---
title: "AD フォレストの回復 - クリーンアップ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 2f652d08304a17ecbfde51bbb6f35e4666cd9eca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---cleanup"></a>AD フォレストの回復 - クリーンアップ 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 必要に応じて、次の post 回復手順を実行します。  
  
-   フォレスト全体を修復した後は、Dc の各優先および代替 DNS サーバーの構成を含む、元の DNS 構成に戻すことができます。 構成後は、DNS サーバーは、誤動作前に、と、上記の名前解決の機能が復元されます。 リカバリされていない Dc に対するすべての DNS レコードを削除します。  
  
-   リカバリされていないすべての Dc の Windows インターネット ネーム サービス (WINS) レコードを削除します。  
  
-   ドメインまたはフォレスト内の他の Dc を操作マスターの役割を転送し、障害発生前に、の構成に基づいたグローバル カタログ サーバーを追加できます。  
  
-   フォレスト全体を以前の状態に復元すると、ために、追加された任意のオブジェクト (ユーザーとコンピューター] など、この時点以降後に既存のオブジェクトに加えられた (パスワードの変更) などのすべての更新は失われます。 したがって、不足しているオブジェクトを再作成し、必要に応じて、不足している更新プログラムを再適用する必要があります。  
  
-   これらの外部の信頼関係がバックアップから自動的に復元されなかったので、外部ドメインとフォレスト、出力方向の信頼を復元する必要もあります。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  



