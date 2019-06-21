---
title: リモート アクセス サーバー上の既存の負荷を監視する
description: このトピックでは、リモート アクセスの監視とアカウンティング Windows Server 2016 では、ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 62fa2895-62ae-42cf-817c-53e06ac2a26c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dc232a52e82f3b66164d30a134ed9e422db0964a
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282684"
---
# <a name="monitor-the-existing-load-on-the-remote-access-server"></a>リモート アクセス サーバー上の既存の負荷を監視する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

**注:** Windows Server 2012 では、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) は単一のリモート アクセスの役割に統合されています。  
  
用語 **ロード** リモート アクセス サーバーに接続の数に関連する統計情報を参照します。 リモート アクセス サーバーで負荷を追跡するために必要な手順を次に示します。  
  
パフォーマンス モニター カウンターを使用するには、統計を追跡や、サーバーの負荷の統計情報を表示するためのリモート アクセス サーバーの管理コンソールで提供される監視ダッシュ ボードを使用できます。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
#### <a name="to-use-the-monitoring-dashboard-to-monitor-the-remote-access-server-load"></a>監視ダッシュ ボードを使用して、リモート アクセス サーバーの負荷を監視するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  **[ダッシュボード]** をクリックして**リモート アクセス管理コンソール**の**リモート アクセス ダッシュボード**に移動します。  
  
3.  監視ダッシュ ボードに注意してください、 **リモート クライアントの状態** 内でタイル、 **サーバーの状態** を並べて表示します。 このタイルには、接続されているリモート クライアントの合計数、接続されている DirectAccess クライアントの総数、および過去 24 時間に接続しているユーザーの最大数などの統計情報が一覧表示します。  
  
4.  クリックして **更新**  **タスク** 正常性状態を再読み込みする右のペインでします。 既定の更新間隔を変更するにはクリックして **更新間隔の構成**  **タスク**します。  
  
#### <a name="to-use-the-performance-monitor-tool-to-monitor-performance-counters-on-the-remote-access-server"></a>パフォーマンス モニター ツールを使用して、リモート アクセス サーバーのパフォーマンス カウンターを監視するには  
  
1.  クリックして **開始**, 、 をクリックして **管理ツール**, をダブルクリックし、 **パフォーマンス モニター**します。  
  
2.  **パフォーマンス**, 、クリックして **パフォーマンス モニター**します。  
  
3.  クリックして、 **追加**  ボタン (緑色十字形のアイコンで示されます)、 **パフォーマンス モニター** ツールバーです。  
  
4.  一覧から **使用可能なカウンター**, 、内のすべてのカウンターを選択、 **RAS** と **RAmgmtsvc** カテゴリ、およびクリック **追加 >>** します。  
  
5.  一覧から、もう一度 **使用可能なカウンター**, 、内のすべてのカウンターを選択、 **IPsec 接続** カテゴリ、およびクリック **追加 >> します。**  
  
6.  をクリックして **OK** で選択したカウンターを追加する、 **パフォーマンス モニター** 追跡用のコンソールです。  
  
**パフォーマンス モニター** グラフィカルに選択したサーバーの負荷の統計情報を示します。  
  
![Windows PowerShell](../../../media/Monitor-the-existing-load-on-the-Remote-Access-server/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary  
```  
  


