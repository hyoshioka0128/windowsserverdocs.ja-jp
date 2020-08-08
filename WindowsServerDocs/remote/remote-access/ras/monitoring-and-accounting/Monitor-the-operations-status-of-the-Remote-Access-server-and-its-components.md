---
title: リモート アクセス サーバーとそのコンポーネントの操作状態を監視する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e9cc5988ab688b7b9b6e0ebe91ebf7d0c65f0ed9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955119"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>リモート アクセス サーバーとそのコンポーネントの操作状態を監視する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

**注:** Windows Server 2012 では、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) は単一のリモート アクセスの役割に統合されています。

その操作の状況を監視するリモート アクセス サーバーの管理コンソールを使用できます。

> [!NOTE]
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。

#### <a name="to-monitor-the-remote-access-server-operations-status"></a>リモート アクセス サーバーの操作の状態を監視するには

1.  **サーバー マネージャー**で、[**ツール**] をクリックし、[**リモート アクセス管理**] をクリックします。

2.  クリックして **ダッシュ ボード** に移動する **リモート アクセス レポート** で、 **リモート アクセス管理コンソール**します。

3.  監視ダッシュ ボードに注意してください、 **操作の状況** 内でタイル、 **サーバーの状態** を並べて表示します。 このタイルには、サーバー操作の状態と、サーバーのすべてのコンポーネントの状態が一覧表示します。

4.  クリックして **更新** [ **タスク** 操作状態を再読み込みする右のペインで。 操作の状況を自動的に更新 5 分ごとに、これは、既定の更新間隔です。 既定の更新間隔を変更するにはクリックして **更新間隔の構成**します。

![Windows PowerShell](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***

次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

> [!NOTE]
> クラスターの状態を操作するためのコマンドは、参照用です。

```
PS> Get-RemoteAccessHealth
PS> Get-RemoteAccessHealth -Cluster
```



