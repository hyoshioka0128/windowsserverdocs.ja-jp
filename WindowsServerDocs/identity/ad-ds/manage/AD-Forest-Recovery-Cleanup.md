---
title: AD フォレストの回復-クリーンアップ
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.openlocfilehash: 74f4518ead647aa4a3c8e4f7a8388c8735d466e1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956709"
---
# <a name="ad-forest-recovery---cleanup"></a>AD フォレストの回復-クリーンアップ

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

 必要に応じて、次の回復後の手順を実行します。

- フォレスト全体が回復された後、元の DNS 構成に戻すことができます。これには、各 Dc の優先 DNS サーバーおよび代替 DNS サーバーの構成が含まれます。 DNS サーバーが誤動作前として構成されると、以前の名前解決機能が復元されます。 回復されていない Dc の DNS レコードを削除します。
- 回復されていないすべての Dc の Windows インターネットネームサービス (WINS) レコードを削除します。
- 操作マスタの役割をドメインまたはフォレスト内の他の Dc に転送し、障害発生前の構成に基づいて、より多くのグローバルカタログサーバーを追加することができます。
- フォレスト全体が以前の状態に復元されるので、追加されたすべてのオブジェクト (ユーザーやコンピューターなど) と、この時点以降に既存のオブジェクトに対して行われたすべての更新 (パスワードの変更など) が失われます。 そのため、不足しているオブジェクトを再作成し、必要に応じて不足している更新プログラムを再適用する必要があります。
- 外部の信頼関係がバックアップから自動的に復元されないため、外部のドメインおよびフォレストとの出力方向の信頼を復元する必要がある場合もあります。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
