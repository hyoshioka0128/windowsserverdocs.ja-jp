---
title: ユーザー セッションを中断してアクティブな状態で保持する
description: MultiPoint セッションを切断せずに、ユーザーを中断する方法について説明します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 0ef9d98584df568438cc3c905a7c86cd58f53343
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394929"
---
# <a name="suspend-and-leave-user-session-active"></a>ユーザー セッションを中断してアクティブな状態で保持する
ユーザーのセッションを終了したくない場合は、MultiPoint Services システムからユーザーを切断または中断することができます。 管理ユーザーがユーザーのセッションを切断するのではなく、ユーザー自身がセッションを切断することもできます。 ユーザーセッションが中断されている間は、コンピューターがシャットダウンまたは再起動されるまで、セッションは MultiPoint Services システムのコンピューターメモリ内でアクティブなままになります。 コンピューターがシャットダウンまたは再起動されると、中断されていたセッションはすべて終了し、保存されていない作業は失われます。  
  
1.  ステーション モードで MultiPoint マネージャーを開き、クリックして、 **ステーション**  タブをクリックします。  
  
2.  **[コンピューター]** 列で、セッションを中断するコンピューターの名前をクリックします。  
  
3.  **[ステーションのタスク]** で、 **[すべてのステーションを中断する]** をクリックします。  
  
ユーザーは、ユーザー セッションの中断後、同じステーションまたは別のステーションにログオンし、元のセッションで作業を続行できます。  
  
## <a name="see-also"></a>関連項目  
[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)  
[ユーザー セッションをログオフまたは切断する](Log-off-or-Disconnect-User-Sessions.md)