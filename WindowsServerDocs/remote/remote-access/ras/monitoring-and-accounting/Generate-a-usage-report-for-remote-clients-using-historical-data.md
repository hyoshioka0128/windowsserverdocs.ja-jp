---
title: 履歴データを使ってリモート クライアントの使用状況レポートを生成する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0305467b-ce39-4532-a05a-2cc5ff946f55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bae50345e8a6fd4018857e2a754d0274ce02855d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367254"
---
# <a name="generate-a-usage-report-for-remote-clients-using-historical-data"></a>履歴データを使ってリモート クライアントの使用状況レポートを生成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

**注:** Windows Server 2012 が DirectAccess およびルーティングとリモート アクセス サービス (RRAS) を 1 つのリモート アクセス役割に結合します。  
  
リモート アクセス サーバーで管理コンソールを使用して、サーバーにアクセスしているリモート クライアントの使用状況レポートを生成することができます。 リモート クライアントの使用状況レポートを生成するには、最初にリモート アクセス サーバーのアカウンティングを有効します。 レポートを生成した後は、サーバーにロード統計を表示するためのリモート アクセス サーバーの管理コンソールで提供される監視ダッシュ ボードを使用することができます。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
#### <a name="to-enable-accounting-on-the-remote-access-server"></a>リモート アクセス サーバーでアカウンティングを有効にするには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  クリックして **レポート** に移動する **リモート アクセス レポート** で、 **リモート アクセス管理コンソール**します。  
  
3.  をクリックして **アカウンティングを構成する** で、 **リモート アクセス レポート** タスク ペインです。  
  
4.  選択、 **受信トレイ アカウンティングを使用する** リモート アクセス サーバーでアカウンティングを有効にする チェック ボックスです。  
  
5.  をクリックして **適用** をサーバーで、アカウンティング構成を有効にし、をクリックし、 **閉じる** 、サーバーが、構成を正常に適用した後です。  
  
#### <a name="to-generate-the-usage-report"></a>使用状況レポートを生成するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  クリックして **レポート** に移動する **リモート アクセス レポート** で、 **リモート アクセス管理コンソール**します。  
  
3.  中央のペインで、レポートの期間を選択するカレンダーの日付をクリックして **開始日:** と **終了日:** , 、クリックして **レポートの生成**します。  
  
4.  選択した時間とそれらについての詳細な統計情報内で、リモート アクセス サーバーに接続されているユーザーの一覧が表示されます。 一覧の最初の行をクリックします。 行を選択すると、リモート ユーザーの活動は、プレビュー ウィンドウに表示されます。 選択して、 **サーバー負荷の統計情報** 、サーバー上の履歴の負荷を表示するプレビュー ウィンドウにタブをクリックします。  
  
    をクリックして、 **サーバー負荷の統計情報** 、サーバー上の履歴の負荷を表示するプレビュー ウィンドウにタブをクリックします。  
  
> [!NOTE]  
> **セッションについて**  
>   
> リモート アクセスのアカウンティングがの概念に基づく **セッション**します。 異なり、 **接続**, 、 **セッション** はリモート クライアントの IP アドレスとユーザー名の組み合わせによって一意に識別します。 たとえば、リモートのクライアントでは、Client1 というコンピューター トンネルが形成される場合、セッションが作成されアカウンティング データベースに格納されています。 名前付きの User1 がしばらくしてからのクライアントから接続するユーザーが渡されます (ただし、コンピューター トンネルがアクティブのまま)、セッションが別のセッションとして記録されます。 セッションの違いは、コンピューター トンネルとユーザーのトンネルの違いを保持します。  
  
windows PowerShell の ![](../../../media/Generate-a-usage-report-for-remote-clients-using-historical-data/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
次のスクリプトでのレポートを作成する日付範囲の変更、 **- StartDateTime** と **- EndDateTime** パラメーター。  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
Shows server load statistics.  
PS> Get-RemoteAccessUserActivity -HostIPAddress 10.0.0.1 -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
```  
  


