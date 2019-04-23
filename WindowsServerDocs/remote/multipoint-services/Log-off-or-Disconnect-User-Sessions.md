---
title: ユーザー セッションをログオフまたは切断する
description: 手動でユーザーをログオフする方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3e9bbcdc-e33b-481e-8b46-787a4f6d58bc
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 518e9dc9ba9603d988a7e21e08caa29db9f04bde
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854943"
---
# <a name="log-off-or-disconnect-user-sessions"></a>ユーザー セッションをログオフまたは切断する
MultiPoint Services ユーザーは、ログオンし、任意の Windows セッションと同じよ、デスクトップのセッションからログオフします。 ユーザーは切断したり、MultiPoint Services ステーションが使用されていないが、そのセッションは MultiPoint Services システムのコンピューターのメモリ内でアクティブなままにするために、セッションを中断できます。  
  
さらに、管理ユーザーは、ユーザーが MultiPoint Services セッションから切断されているかがシステムからログオフを忘れた場合、ユーザーのセッションを終了できます。  
  
## <a name="logging-off-or-disconnecting-a-session"></a>セッションのログオフまたは切断  
次の表では、管理者またはユーザーがセッションのログオフ、中断、または終了に使用できるさまざまなオプションについて説明します。  
  
|||  
|-|-|  
|**操作**|**効果**|  
|クリックして**開始**、設定 をクリックして、ユーザー名 (右上隅) をクリックしておよびクリックして**サインアウト**します。|セッションは終了し、ステーションは任意のユーザーによるログオンに使用できます。|  
|**[開始]** をクリックし、**[設定]** をクリックし、[電源] をクリックして、**[切断]** をクリックします。|セッションは切断されますが、コンピューターのメモリ内に保持されています。 ステーションは、同じユーザーまたは別のユーザーによるログオンに使用できるようになります。|  
|クリックして**開始**、設定 をクリックして、ユーザー名 (右上隅) をクリックしておよびクリックして**ロック**|ステーションはロックされ、セッションはコンピューターのメモリ内に保持されています。|  
  
## <a name="suspending-or-ending-a-users-session"></a>ユーザーのセッションの中断または終了  
次の表では、管理ユーザーがユーザーのセッションの切断または終了に使用できるさまざまなオプションについて説明します。  
  
|||  
|-|-|  
|**操作**|**効果**|  
|**中断します。** MultiPoint マネージャーを使用して、**ステーション** タブをユーザーのセッションを中断します。 詳細については、「[ユーザー セッションを中断してアクティブな状態で保持する](Suspend-and-Leave-User-Session-Active.md)」トピックを参照してください。|ユーザーのセッションは終了し、コンピューターのメモリに保持されます。 ステーションは、同じユーザーまたは別のユーザーによるログオンに使用できるようになります。 ユーザーは、同じステーションまたは別のステーションにログオンし、仕事を続けることができます。|  
|**終わり：** MultiPoint マネージャーを使用して、**ステーション** タブ、ユーザーのセッションを終了します。 **[ステーション]** タブではすべてのユーザー セッションを終了することもできます。詳細については、「[ユーザー セッションの終了](End-a-User-Session.md)」トピックを参照してください。|ユーザーのセッションは終了し、ステーションは任意のユーザーによるログオンに使用できるようになります。 ユーザーのセッションは **[ステーション]** タブに表示されなくなり、コンピューターのメモリにも残りません。|  
  
## <a name="see-also"></a>関連項目  
[中断し、ユーザー セッションをアクティブなままにします](Suspend-and-Leave-User-Session-Active.md)  
[ユーザー セッションを終了します。](End-a-User-Session.md)  
[ユーザー デスクトップを管理します。](manage-user-desktops-using-multipoint-dashboard.md)  
[ユーザー セッションをログオフします。](Log-Off-User-Sessions.md)    