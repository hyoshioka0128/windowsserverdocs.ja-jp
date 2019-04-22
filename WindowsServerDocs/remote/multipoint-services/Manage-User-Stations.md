---
title: ユーザー ステーションの管理
description: ユーザー ステーションが MultiPoint services を管理する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b418578d-3a4c-49b0-90db-8389b320b2f6
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 8c5351f3e8ec9890ef72905b646c37e9b049745e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823723"
---
# <a name="manage-user-stations"></a>ユーザー ステーションの管理
このセクションでは、MultiPoint Services のシステムを構成する*ステーション*を管理する方法について説明します。 MultiPoint Services システムを管理するには、両方の管理 MultiPoint Manager のハードウェアおよびソフトウェア コンポーネントが含まれます。 MultiPoint Services システムでは、デスクトップは、各ユーザー ステーションのモニターに表示されるソフトウェアのユーザー インターフェイスをします。  
  
## <a name="station-status"></a>ステーションの状態  
**[ステーション]** タブでは、各デスクトップの次の種類の状態を表示できます。状態は次のとおりです。  
  
-   ログオンしているユーザー  
  
-   コンピューターではまだアクティブであるが、中断されているユーザー セッション  
  
-   使用中のステーションと使用しているユーザー  
  
デスクトップの状態を参照する方法の詳細については、「[ユーザーの接続状態の表示](View-User-Connection-Status.md)」のトピックを参照してください。  

>[!TIP] 
> 各ステーションにはわかりやすい名前を割り当てることができます。そうすれば、ステーションをより簡単に識別できます。 **ステーションの識別** を使用します。割り当てられた画面にステーション名が表示されます。
  
## <a name="different-ways-to-log-standard-users-off-of-the-multipoint-services-system"></a>MultiPoint Services システムから標準のユーザーをログオフさせるさまざまな方法  
*管理ユーザー*は、MultiPoint Services システムのアクティブ ユーザーに影響を与えることなく、いつでも Windows からログオフできます。 *標準ユーザー*も、MultiPoint Services システムのセッションを*切断*したり、*ログオフ*したりできます。 ディスクの保護が有効になっている場合、ユーザーがその日の作業を終えるとき、作業をコンピューターまたは外部のストレージ デバイスに保存して、MultiPoint Services システムがシャットダウンされても保存した作業を別の日に取得できるようにする必要があります。  
  
管理ユーザーは、標準ユーザーをログオフさせるのではなく、その*セッション*を終了させる必要がある場合があります。 標準ユーザーのセッションは、次のいずれかの方法で終了させることができます。  
  
-   セッションを終了させ、ユーザーをログオフさせます。 ユーザーのセッションの終了に関する詳細については、「[ユーザー セッションの終了](End-a-User-Session.md)」のトピックを参照してください。  
  
-   ユーザーのセッションを一時的に終了させ、MultiPoint Services システムのコンピューター メモリ内でセッションをアクティブに維持します。 中断されているユーザーが作業を継続するには、同じまたは別のステーションからのセッションに再接続します。 ユーザーのセッションの中断に関する詳細は、「[ユーザー セッションを中断してアクティブな状態で保持する](Suspend-and-Leave-User-Session-Active.md)」のトピックを参照してください。  
  
## <a name="set-a-station-to-automatically-log-on"></a>自動ログオンするステーションの設定  
管理ユーザーは、MultiPoint Services を実行するコンピューターが起動される際に、1 つ以上のステーションを自動ログオンさせるようセットアップすることができます。 自動ログオンの詳細については、「[ステーションでの自動ログオンのセットアップ](Set-up-a-Station-for-Automatic-Logon.md)」のトピックを参照してください。  
  
## <a name="split-a-station"></a>ステーションの分割  
解像度が 1024 x 768 を超えるステーションのモニターはいずれも、2 つのステーションに分割できます。 ステーションの分割の詳細については、「[ユーザー ステーションの分割](Split-a-User-Station.md)」のトピックを参照してください。  
  
## <a name="see-also"></a>関連項目  
[ユーザー接続の状態の表示](View-User-Connection-Status.md)  
[ログオフまたはユーザー セッションの切断](Log-off-or-Disconnect-User-Sessions.md)  
[中断し、ユーザー セッションをアクティブなままにします](Suspend-and-Leave-User-Session-Active.md)  
[自動ログオン用ステーションをセットアップします。](Set-up-a-Station-for-Automatic-Logon.md)  
[ユーザー セッションを終了します。](End-a-User-Session.md)  
[ユーザー ステーションを分割します。](Split-a-User-Station.md)