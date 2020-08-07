---
title: ユーザー ステーションの管理
description: MultiPoint Services でユーザーステーションを管理する方法について説明します。
ms.topic: article
ms.assetid: b418578d-3a4c-49b0-90db-8389b320b2f6
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: bcbf12b3d9a9a83cab98fb342f325436e42a17a9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951867"
---
# <a name="manage-user-stations"></a>ユーザー ステーションの管理
このセクションでは、MultiPoint Services のシステムを構成する*ステーション*を管理する方法について説明します。 MultiPoint Services システムの管理には、MultiPoint マネージャーのハードウェアコンポーネントとソフトウェアコンポーネントの管理の両方が含まれます。 MultiPoint Services システムでデスクトップは、各ユーザーのステーションのモニターに表示されるソフトウェアのユーザー インターフェイスを指します。

## <a name="station-status"></a>ステーションの状態
[**ステーション**] タブでは、デスクトップごとに次の種類の状態を表示できます。状態は次のとおりです。

-   ログオンしているユーザー

-   コンピューターではまだアクティブであるが、中断されているユーザー セッション

-   使用中のステーションと使用しているユーザー

デスクトップの状態を参照する方法の詳細については、「[ユーザーの接続状態の表示](View-User-Connection-Status.md)」のトピックを参照してください。

>[!TIP]
> 各ステーションにはわかりやすい名前を割り当てることができます。そうすれば、ステーションをより簡単に識別できます。 **ステーションの識別** を使用します。割り当てられた画面にステーション名が表示されます。

## <a name="different-ways-to-log-standard-users-off-of-the-multipoint-services-system"></a>MultiPoint Services システムから標準のユーザーをログオフさせるさまざまな方法
*管理ユーザー*は、MultiPoint Services システムのアクティブ ユーザーに影響を与えることなく、いつでも Windows からログオフできます。 *標準ユーザー*も、MultiPoint Services システムのセッションを*切断*したり、*ログオフ*したりできます。 ディスクの保護が有効になっている場合、ユーザーがその日の作業を終えるとき、作業をコンピューターまたは外部のストレージ デバイスに保存して、MultiPoint Services システムがシャットダウンされても保存した作業を別の日に取得できるようにする必要があります。

管理ユーザーは、ユーザーがログオフするのではなく、標準ユーザーの*セッション*を終了することが必要になる場合があります。 標準ユーザーのセッションは、次の2つの方法のいずれかで終了できます。

-   セッションを終了させ、ユーザーをログオフさせます。 ユーザーのセッションを終了する方法の詳細については、「[ユーザーセッションを終了する](End-a-User-Session.md)」を参照してください。

-   ユーザーのセッションを一時的に終了するようにユーザーを中断しますが、セッションは MultiPoint Services システムのコンピューターメモリ内でアクティブなままにしておきます。 中断されているユーザーが作業を継続するには、同じまたは別のステーションからのセッションに再接続します。 ユーザーのセッションを中断する方法の詳細については、「[ユーザーセッションを中断してアクティブ](Suspend-and-Leave-User-Session-Active.md)にする」を参照してください。

## <a name="set-a-station-to-automatically-log-on"></a>自動ログオンするステーションの設定
管理ユーザーは、MultiPoint Services を実行するコンピューターが起動される際に、1 つ以上のステーションを自動ログオンさせるようセットアップすることができます。 自動ログオンの詳細については、「[ステーションでの自動ログオンのセットアップ](Set-up-a-Station-for-Automatic-Logon.md)」のトピックを参照してください。

## <a name="split-a-station"></a>ステーションの分割
解像度が 1024 x 768 を超えるステーションのモニターはいずれも、2 つのステーションに分割できます。 ステーションの分割の詳細については、「[ユーザー ステーションの分割](Split-a-User-Station.md)」のトピックを参照してください。

## <a name="see-also"></a>参照
[ユーザーの接続状態](View-User-Connection-Status.md) 
 の表示[ユーザーセッション](Log-off-or-Disconnect-User-Sessions.md) 
 のログオフまたは切断[ユーザーセッションを中断してアクティブ](Suspend-and-Leave-User-Session-Active.md) 
 のままにする[ステーションの自動ログオン](Set-up-a-Station-for-Automatic-Logon.md) 
 をセットアップする[ユーザーセッション](End-a-User-Session.md) 
 を終了する[ユーザーステーションを分割する](Split-a-User-Station.md)