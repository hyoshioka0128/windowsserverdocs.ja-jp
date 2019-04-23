---
title: 使用率データを消去する
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
ms.openlocfilehash: 7b471417d4c44c22f115443f1f2dcca6f351e6f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827943"
---
# <a name="purge-utilization-data"></a>使用率データを消去する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、使用率データを IPAM データベースから削除するのに方法について説明します。  

メンバーである必要があります **IPAM Administrators**, 、ローカル コンピューター **管理者** この手順を実行するには、グループ、またはそれと同等です。

## <a name="to-purge-the-ipam-database"></a>IPAM データベースを消去するには  
1. サーバー マネージャーを開き、IPAM クライアント インターフェイスを参照します。
2. 次の場所のいずれかに移動します。**IP アドレス ブロック**、 **IP アドレス インベントリ**、または**IP アドレス範囲のグループ**します。  
3. クリックして **タスク**, 、 をクリックし、 **使用率データの消去**します。 **使用率データの消去**  ダイアログ ボックスが表示されます。
4. **すべての使用率を消去する前にデータ**, 、 をクリックして **日付を選択**します。
5. その日の前にすべてのデータベース レコードを削除する日付を選択します。
6. **[OK]** をクリックします。 IPAM では、指定したすべてのレコードを削除します。
