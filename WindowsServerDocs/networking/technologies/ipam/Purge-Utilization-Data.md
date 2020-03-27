---
title: 使用率データを消去する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a8542e643a9c4d33acad18523fd34eed8926413d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316773"
---
# <a name="purge-utilization-data"></a>使用率データを消去する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、使用率データを IPAM データベースから削除するのに方法について説明します。  

メンバーである必要があります **IPAM Administrators**, 、ローカル コンピューター **管理者** この手順を実行するには、グループ、またはそれと同等です。

## <a name="to-purge-the-ipam-database"></a>IPAM データベースを消去するには  
1. サーバー マネージャーを開き、IPAM クライアント インターフェイスを参照します。
2. 次の場所のいずれかに移動します。 **IP アドレス ブロック**, 、**IP アドレス インベントリ**, 、または **IP アドレス範囲のグループ**します。  
3. クリックして **タスク**, 、 をクリックし、 **使用率データの消去**します。 **使用率データの消去**  ダイアログ ボックスが表示されます。
4. **すべての使用率を消去する前にデータ**, 、 をクリックして **日付を選択**します。
5. その日の前にすべてのデータベース レコードを削除する日付を選択します。
6. **[OK]** をクリックすると、 IPAM では、指定したすべてのレコードを削除します。
