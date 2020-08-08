---
title: 使用率データを消去する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 45cada9e-69b9-43df-b6f5-6d3942435809
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8ac13abad7b55e3bb592efc63b8d05d85c13f41d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944684"
---
# <a name="purge-utilization-data"></a>使用率データを消去する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、使用率データを IPAM データベースから削除するのに方法について説明します。

メンバーである必要があります **IPAM Administrators**, 、ローカル コンピューター **管理者** この手順を実行するには、グループ、またはそれと同等です。

## <a name="to-purge-the-ipam-database"></a>IPAM データベースを消去するには
1. サーバー マネージャーを開き、IPAM クライアント インターフェイスを参照します。
2. 次の場所のいずれかに移動します。 **IP アドレス ブロック**, 、**IP アドレス インベントリ**, 、または **IP アドレス範囲のグループ**します。
3. クリックして **タスク**, 、] をクリックし、 **使用率データの消去**します。 **使用率データの消去** ] ダイアログ ボックスが表示されます。
4. **すべての使用率を消去する前にデータ**, 、] をクリックして **日付を選択**します。
5. その日の前にすべてのデータベース レコードを削除する日付を選択します。
6. **[OK]** をクリックします。 IPAM では、指定したすべてのレコードを削除します。
