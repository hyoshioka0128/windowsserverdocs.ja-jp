---
title: リモート アクセス サーバーの操作上の問題を特定して解決する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ce84c9f-fd1f-4463-8fc7-d2f33344a2c9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: db10f784f383938edb29b18d7e8febf869378abc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404562"
---
# <a name="identify-and-resolve-remote-access-server-operations-problems"></a>リモート アクセス サーバーの操作上の問題を特定して解決する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

**注:** Windows Server 2012 では、DirectAccess およびルーティングとリモート アクセス サービス (RRAS) は単一のリモート アクセスの役割に統合されています。  
  
リモートアクセスサーバーの操作の問題、その根本原因、および問題の解決に必要な解決策を特定するには、次の手順を実行します。  
  
> [!NOTE]  
> このトピックで説明するタスクを完了には、Domain Admins グループのメンバーまたは各コンピューターの Administrators グループのメンバーとしてサインインする必要があります。 Administrators グループのメンバーであるアカウントでサインインしているときにタスクを完了できない場合は、Domain Admins グループのメンバーであるアカウントでサインインしているときにタスクを実行するみてください。  
  
このトピックには、次のタスクの実行に関する情報が含まれています。  
  
- 操作の問題をシミュレートする  
  
- 操作の問題を特定して修正措置を行う  
  
- IP ヘルパーサービスを復元する  
  
### <a name="BKMK_Simulate"></a>操作の問題をシミュレートする  
  
> [!CAUTION]  
> リモートアクセスサーバーが正しく構成されていて、問題が発生していない可能性があるため、次の手順を使用して操作の問題をシミュレートできます。 サーバーが現在運用環境でクライアントにサービスを提供している場合は、現時点ではこれらの操作を行わないようにすることをお勧めします。 代わりに、今後、リモートアクセスサーバーで発生する可能性のある問題に対処する方法を理解するための手順を参照できます。  
  
IP ヘルパーサービス (IPHlpSvc) は、IPv6 移行テクノロジ (ip-https、6to4、Teredo など) をホストし、DirectAccess サーバーが正常に機能するために必要です。 リモートアクセスサーバーでのシミュレートされた操作の問題を示すには、(IPHlpSvc) ネットワークサービスを停止する必要があります。  
  
##### <a name="to-stop-the-ip-helper-service"></a>IP ヘルパーサービスを停止するには  
  
1.  リモートアクセスサーバーの**スタート**画面で、 **[管理ツール]** をクリックし、 **[サービス]** をダブルクリックします。  
  
2.  **サービス**の一覧で下にスクロールし、 **[IP ヘルパー]** を右クリックして、 **[停止]** をクリックします。  
  
### <a name="BKMK_Identify"></a>操作の問題を特定して修正措置を行う  
IP ヘルパーサービスを無効にすると、リモートアクセスサーバーで重大なエラーが発生します。 監視ダッシュボードには、サーバーの操作の状態と問題の詳細が表示されます。  
  
##### <a name="to-identify-the-details-and-take-corrective-action"></a>詳細を特定して修正措置を実行するには  
  
1.  **サーバー マネージャー**, をクリックして **ツール**, 、順にクリック **リモート アクセス管理**します。  
  
2.  **[ダッシュボード]** をクリックして**リモート アクセス管理コンソール**の**リモート アクセス ダッシュボード**に移動します。  
  
3.  左側のウィンドウでリモートアクセスサーバーが選択されていることを確認し、中央のウィンドウで **[操作の状態]** をクリックします。  
  
4.  緑または赤のアイコンを持つコンポーネントの一覧が表示されます。これらのアイコンは動作状態を示します。 一覧の**ip-https 行をクリックします**。 行を選択すると、次のように、**詳細**ウィンドウに操作の詳細が表示されます。  
  
    **Error**  
  
    IP ヘルパーサービス (IPHlpSvc) が停止しました。 DirectAccess が想定どおりに機能しない可能性があります。 IP ヘルパーサービスは、接続プラットフォーム、IPv6 移行テクノロジ、および ip-https を使用してトンネル接続を提供します。  
  
    **引き起こし**  
  
    1.  IP ヘルパーサービスが停止しました。  
  
    2.  IP ヘルパーサービスが応答していません。  
  
    **解決方法**  
  
    1.  サービスが実行されていることを確認するには、Windows PowerShell プロンプトで「 **Get service iphlpsc** 」と入力します。  
  
    2.  サービスを有効にするには、管理者特権の Windows PowerShell プロンプトで「 **iphlpsvc** 」と入力します。  
  
    3.  サービスを再起動するには、管理者特権の Windows PowerShell プロンプトで「 **restart-service iphlpsvc** 」と入力します。  
  
### <a name="BKMK_Restart"></a>IP ヘルパーサービスを復元する  
リモートアクセスサーバーで IP ヘルパーサービスを復元するには、上の解決手順に従ってサービスを開始または再起動します。または、次の手順を使用して、IP ヘルパーサービスのエラーをシミュレートするために使用した手順を元に戻します。  
  
##### <a name="to-restart-the-ip-helper-service-on-the-remote-access-server"></a>リモートアクセスサーバーで IP ヘルパーサービスを再起動するには  
  
1.  **[スタート]** 画面で、 **[管理ツール]** をクリックし、 **[サービス]** をダブルクリックします。  
  
2.  **サービス**の一覧で、下へスクロールして **[IP ヘルパー]** を右クリックし、 **[開始]** をクリックします。  
  
@no__t 0Windows PowerShell](../../../media/Identify-and-resolve-Remote-Access-server-operations-problems/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
```  
PS> Get-RemoteAccessHealth | Where-Object {$_.Component -eq "IP-HTTPS"} | Format-List -Property *  
```  
  


