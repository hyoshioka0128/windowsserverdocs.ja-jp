---
title: ユーザー セッションを中断してアクティブな状態で保持する
description: 切断することがなく MultiPoint セッションからユーザーを中断する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: cc4310e6f7609464cf037b750bec6e5e805e0b26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815223"
---
# <a name="suspend-and-leave-user-session-active"></a>ユーザー セッションを中断してアクティブな状態で保持する
接続を切断したり、ユーザーのセッションを終了したくないときに、MultiPoint サービス システムからユーザーを中断できます。 管理ユーザーがユーザーのセッションを切断するのではなく、ユーザー自身がセッションを切断することもできます。 ユーザー セッションが中断されている間、セッションは、MultiPoint Services システムのコンピューターがシャットダウンまたは再起動されない限り、コンピューターのメモリ内にアクティブに保たれます。 コンピューターがシャットダウンまたは再起動されると、中断されていたセッションはすべて終了し、保存されていない作業は失われます。  
  
1.  ステーション モードで MultiPoint マネージャーを開き、クリックして、 **ステーション**  タブをクリックします。  
  
2.  **[コンピューター]** 列で、セッションを中断するコンピューターの名前をクリックします。  
  
3.  **[ステーションのタスク]** で、**[すべてのステーションを中断する]** をクリックします。  
  
ユーザーは、ユーザー セッションの中断後、同じステーションまたは別のステーションにログオンし、元のセッションで作業を続行できます。  
  
## <a name="see-also"></a>関連項目  
[ユーザー デスクトップを管理します。](manage-user-desktops-using-multipoint-dashboard.md)  
[ログオフまたはユーザー セッションの切断](Log-off-or-Disconnect-User-Sessions.md)