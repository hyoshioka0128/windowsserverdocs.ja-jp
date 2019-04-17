---
title: 使用率データを削除します。
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c41be119099aed4867df1bae1a55e2fbaa5c9064
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="purge-utilization-data"></a>使用率データを削除します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、使用率データを IPAM データベースから削除するのに方法について説明します。  

メンバーである必要がある**IPAM Administrators**、ローカル コンピューター**管理者**この手順を実行するには、グループ、またはそれと同等です。

## <a name="to-purge-the-ipam-database"></a>IPAM データベースを削除するには  
1. サーバー マネージャーを開き、IPAM クライアント インターフェイスを参照します。
2. 次の場所のいずれかに移動します。**IP アドレス ブロック**、**IP アドレス インベントリ**、または**IP アドレス範囲のグループ**します。  
3. をクリックして**タスク**、] をクリックし、**使用率データの消去**します。 **使用率データの消去**] ダイアログ ボックスが開きます。
4. **すべての使用率を消去する前にデータ**、] をクリックして**日付を選択して**します。
5. その日の前に、すべてのデータベース レコードを削除する日付を選択します。
6. をクリックして**OK**します。 IPAM では、指定したすべてのレコードを削除します。
