---
title: AD フォレストの回復のクリーンアップ
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: fa7193cc800eac0fee6425a66bd5cd82d8c822c1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868963"
---
# <a name="ad-forest-recovery---cleanup"></a>AD フォレストの回復のクリーンアップ

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

 必要に応じて、次の後の復旧手順を実行します。  
  
- フォレスト全体を回復すると後、は、Dc の各優先および代替 DNS サーバーの構成を含む元の DNS 構成に戻すことができます。 DNS サーバーが構成され、障害前に、と、その前の名前解決機能が復元されます。 復旧されていない dc には、すべての DNS レコードを削除します。  
- 復旧されていないすべての dc には、Windows インターネット ネーム サービス (WINS) レコードを削除します。  
- 操作マスターの役割をドメインまたはフォレスト内の他の Dc に転送し、障害発生前に、構成に基づいて、グローバル カタログ サーバーを追加します。  
- フォレスト全体を以前の状態に復元すると、追加された任意のオブジェクト (ユーザーとコンピューター など、この時点より後の既存のオブジェクトに加えられた (パスワードの変更) などのすべての更新は失われます。 そのため、これら不足しているオブジェクトを再作成し、適切な更新プログラムを再適用する必要があります。  
- バックアップからこれらの外部の信頼関係が自動的に復元されなかったので、外部のドメインとフォレスト、出力方向の信頼を復元する必要もあります。

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
