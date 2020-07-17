---
title: リモート アクセス サーバーとそのコンポーネントの操作状態を監視する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 077a3a64-2fa3-4994-9711-ec1fbdc081ba
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a93f8100b16da1cabbda8ed3e273a2601adb647a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860525"
---
# <a name="monitor-the-operations-status-of-the-remote-access-server-and-its-components"></a>リモート アクセス サーバーとそのコンポーネントの操作状態を監視する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

**注:** Windows Server 2012 が DirectAccess およびルーティングとリモート アクセス サービス (RRAS) を 1 つのリモート アクセス役割に結合します。  
  
その操作の状況を監視するリモート アクセス サーバーの管理コンソールを使用できます。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
#### <a name="to-monitor-the-remote-access-server-operations-status"></a>リモート アクセス サーバーの操作の状態を監視するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  クリックして **ダッシュ ボード** に移動する **リモート アクセス レポート** で、 **リモート アクセス管理コンソール**します。  
  
3.  監視ダッシュ ボードに注意してください、 **操作の状況** 内でタイル、 **サーバーの状態** を並べて表示します。 このタイルには、サーバー操作の状態と、サーバーのすべてのコンポーネントの状態が一覧表示します。  
  
4.  クリックして **更新**  **タスク** 操作状態を再読み込みする右のペインで。 操作の状況を自動的に更新 5 分ごとに、これは、既定の更新間隔です。 既定の更新間隔を変更するにはクリックして **更新間隔の構成**します。  
  
windows PowerShell の ![](../../../media/Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
> [!NOTE]  
> クラスターの状態を操作するためのコマンドは、参照用です。  
  
```  
PS> Get-RemoteAccessHealth  
PS> Get-RemoteAccessHealth -Cluster  
```  
  


