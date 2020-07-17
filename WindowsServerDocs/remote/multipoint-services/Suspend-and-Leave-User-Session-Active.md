---
title: ユーザー セッションを中断してアクティブな状態で保持する
description: MultiPoint セッションを切断せずに、ユーザーを中断する方法について説明します。
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 5263bce3-fe92-4398-8393-2e3a4e05d530
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 2d2771fd60f4d8c11c602a4c5d55f3b5ae2d8b11
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861625"
---
# <a name="suspend-and-leave-user-session-active"></a>ユーザー セッションを中断してアクティブな状態で保持する
ユーザーのセッションを終了したくない場合は、MultiPoint Services システムからユーザーを切断または中断することができます。 管理ユーザーがユーザーのセッションを切断するのではなく、ユーザー自身がセッションを切断することもできます。 ユーザーセッションが中断されている間は、コンピューターがシャットダウンまたは再起動されるまで、セッションは MultiPoint Services システムのコンピューターメモリ内でアクティブなままになります。 コンピューターがシャットダウンまたは再起動されると、中断されていたセッションはすべて終了し、保存されていない作業は失われます。  
  
1.  ステーション モードで MultiPoint マネージャーを開き、クリックして、 **ステーション**  タブをクリックします。  
  
2.  **[コンピューター]** 列で、セッションを中断するコンピューターの名前をクリックします。  
  
3.  **[ステーションのタスク]** で、 **[すべてのステーションを中断する]** をクリックします。  
  
ユーザーは、ユーザー セッションの中断後、同じステーションまたは別のステーションにログオンし、元のセッションで作業を続行できます。  
  
## <a name="see-also"></a>参照  
[ユーザーデスクトップの管理](manage-user-desktops-using-multipoint-dashboard.md)  
[ユーザー セッションをログオフまたは切断する](Log-off-or-Disconnect-User-Sessions.md)