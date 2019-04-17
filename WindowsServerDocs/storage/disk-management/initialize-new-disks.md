---
title: "新しいディスクの初期化"
description: "この記事では、新しいディスクを初期化する方法について説明します。"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 587553746d45eceab654efd4d120038088d32991
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="initialize-new-disks"></a>新しいディスクの初期化

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

> [!NOTE]
> 以下の手順を実行するには、少なくとも **Backup Operators** または **Administrators** グループのメンバーである必要があります。

## <a name="to-initialize-new-disks"></a>新しいディスクを初期化するには
1.  [ディスクの管理] で、初期化するディスクを右クリックし、次に **[ディスクの初期化]** をクリックします。

2.  **[ディスクの初期化]** ダイアログ ボックスで、初期化するディスクを選択します。 パーティション スタイルとして、マスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のいずれかを選択できます。

## <a name="additional-considerations"></a>その他の考慮事項

-   新しいディスクは、"**初期化されていません**" と表示されます。 ディスクを使用する前に、まず初期化する必要があります。 ディスクを追加した後でディスクの管理を開始すると、ディスクの初期化ウィザードが表示され、ディスクを初期化できます。

> [!NOTE]
> 新しいディスクがベーシック ディスクとして初期化されます。

