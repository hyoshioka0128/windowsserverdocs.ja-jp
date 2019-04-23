---
title: リモート アクセス サーバーの操作上の問題を特定して解決する
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
ms.assetid: 7ce84c9f-fd1f-4463-8fc7-d2f33344a2c9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c58ff97e286f91610a321801d177a2977349fa78
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840463"
---
# <a name="identify-and-resolve-remote-access-server-operations-problems"></a>リモート アクセス サーバーの操作上の問題を特定して解決する

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

**注:** Windows Server 2012 では、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) は単一のリモート アクセスの役割に統合されています。  
  
リモート アクセス サーバー操作上の問題、その根本原因、および問題を解決するために必要な解像度を識別するために、次の手順を使用することができます。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
このトピックには、次のタスクの実行に関する情報が含まれます。  
  
- 操作の問題をシミュレートします。  
  
- 操作の問題を特定し、是正措置  
  
- IP ヘルパー サービスを復元します。  
  
### <a name="BKMK_Simulate"></a>操作の問題をシミュレートします。  
  
> [!CAUTION]  
> サーバーは、おそらく、リモート アクセスでは、問題が発生していないと正しく構成されている、ために、操作の問題をシミュレートするために、次の手順を使用できます。 場合は、サーバーは、運用環境でクライアント サービスに現在、この時点で以下のアクションを実行する可能性がありますしません。 代わりに、リモート アクセス サーバーで、今後生じる可能性のある問題に対処する方法について説明する手順を確認できます。  
  
IP ヘルパー サービス (IPHlpSvc) ホスト IPv6 移行テクノロジ (IP-HTTPS、6to4、Teredo など)、また、適切に機能する DirectAccess サーバーに必要です。 リモート アクセス サーバーでの操作をシミュレートされた問題を示すためには、(IPHlpSvc) のネットワーク サービスを停止する必要があります。  
  
##### <a name="to-stop-the-ip-helper-service"></a>IP ヘルパー サービスを停止するには  
  
1.  **開始**画面のリモート アクセス サーバーは、次のようにクリックします。**管理ツール**、し、ダブルクリック**サービス**します。  
  
2.  一覧で**サービス**下にスクロールし、右クリックし、 **IP ヘルパー**、 をクリックし、**停止**します。  
  
### <a name="BKMK_Identify"></a>操作の問題を特定し、是正措置  
IP ヘルパー サービスを無効にすると、リモート アクセス サーバーで、重大なエラーが発生します。 監視ダッシュ ボードは、サーバーの操作の状態と問題の詳細に表示されます。  
  
##### <a name="to-identify-the-details-and-take-corrective-action"></a>詳細情報を特定し、措置を実行するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  **[ダッシュボード]** をクリックして**リモート アクセス管理コンソール**の**リモート アクセス ダッシュボード**に移動します。  
  
3.  左側のウィンドウで、リモート アクセス サーバーが選択されているかどうかを確認し、中央のペインでをクリックして**操作の状況**します。  
  
4.  コンポーネントの動作状況を示す緑または赤のアイコンの一覧が表示されます。 をクリックして、 **IP-HTTPS**リスト内の行。 操作の詳細を示す行を選択したときに、**詳細**ペインとして次のとおりです。  
  
    **Error**  
  
    IP ヘルパー サービス (IPHlpSvc) が停止しました。 DirectAccess は、正常に機能しない可能性があります。 IP ヘルパー サービスは、接続のプラットフォーム、IPv6 移行テクノロジ、および IP-HTTPS を使用してトンネル接続を提供します。  
  
    **エラーの原因**  
  
    1.  IP ヘルパー サービスが停止しました。  
  
    2.  IP ヘルパー サービスが応答していません。  
  
    **解決方法**  
  
    1.  サービスが実行されていることを確認するには、入力**Get-service iphlpsc** Windows PowerShell プロンプトでします。  
  
    2.  サービスを有効にするには、入力**Start-service iphlpsvc**管理者特権での Windows PowerShell プロンプトからです。  
  
    3.  サービスを再起動するには、次のように入力します。 **Restart-service iphlpsvc**管理者特権での Windows PowerShell プロンプトからです。  
  
### <a name="BKMK_Restart"></a>IP ヘルパー サービスを復元します。  
IP ヘルパー サービスをリモート アクセス サーバーを復元するを開始または再起動、サービスでは、上記の解決手順を利用できるまたは IP ヘルパー サービス障害をシミュレートするために使用する手順を逆に、次の手順を使用することができます。  
  
##### <a name="to-restart-the-ip-helper-service-on-the-remote-access-server"></a>リモート アクセス サーバーの IP ヘルパー サービスを再起動するには  
  
1.  **開始**画面で、**管理ツール**、し、ダブルクリック**サービス**します。  
  
2.  一覧で**サービス**下にスクロールし、右クリックし、 **IP ヘルパー**、 をクリックし、**開始**します。  
  
![Windows PowerShell](../../../media/Identify-and-resolve-Remote-Access-server-operations-problems/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド。  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
PS> Get-RemoteAccessHealth | Where-Object {$_.Component -eq "IP-HTTPS"} | Format-List -Property *  
```  
  


