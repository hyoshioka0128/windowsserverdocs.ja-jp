---
title: リモート アクセス サーバーとそのコンポーネントの操作状態を監視する
description: このトピックでは、リモート アクセスの監視とアカウンティング Windows Server 2016 では、ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83d12826bd8128bc38d84c252045d74cf416457e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882883"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>リモート アクセス サーバーとそのコンポーネントの操作状態を監視する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

**注:** Windows Server 2012 では、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) は単一のリモート アクセスの役割に統合されています。  
  
その操作の状況を監視するリモート アクセス サーバーの管理コンソールを使用できます。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
#### <a name="to-monitor-the-remote-access-server-operations-status"></a>リモート アクセス サーバーの操作の状態を監視するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  クリックして **ダッシュ ボード** に移動する **リモート アクセス レポート** で、 **リモート アクセス管理コンソール**します。  
  
3.  監視ダッシュ ボードに注意してください、 **操作の状況** 内でタイル、 **サーバーの状態** を並べて表示します。 このタイルには、サーバー操作の状態と、サーバーのすべてのコンポーネントの状態が一覧表示します。  
  
4.  クリックして **更新**  **タスク** 操作状態を再読み込みする右のペインで。 操作の状況を自動的に更新 5 分ごとに、これは、既定の更新間隔です。 既定の更新間隔を変更するにはクリックして **更新間隔の構成**します。  
  
![Windows PowerShell](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
> [!NOTE]  
> クラスターの状態を操作するためのコマンドは、参照用です。  
  
```  
PS> Get-RemoteAccessHealth  
PS> Get-RemoteAccessHealth -Cluster  
```  
  


