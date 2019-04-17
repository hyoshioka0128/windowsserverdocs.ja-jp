---
title: "Windows Server Essentials Log Collector を実行します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6b49fee7ca4a19d5a501cf96c1ce356f8242c81f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector を実行します。
Windows Server Essentials Log Collector は、ネットワーク上のサーバーまたはコンピューターから実行できます。 サーバーから Log Collector を実行する場合は、サーバーからのみログを収集できます。 ネットワーク コンピューターから Log Collector を実行する場合は、そのコンピューターのログに加えて、サーバーからログを収集することもできます。  
  
 Log Collector を実行する適切な管理者特権が必要です。 サーバーのログ ファイルを収集している場合、サーバー管理者がおく必要があります。ネットワーク コンピューター上のログ ファイルを収集している場合は、そのコンピューターのクライアント管理者があります。  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>ウィザードを使用して、サーバーで Log Collector を実行するには  
  
1.  **開始**ページ] をクリックして、サーバーの**Windows Server Essentials Log Collector**します。  
  
    > [!NOTE]
    >  -   Log Collector プログラムが表示されない場合、**開始**] ページを参照**%system%\Program Files (x86) \Windows Server Essentials Log Collector**、順にダブルクリック**LogCollector**します。  
    > -   管理者特権を持つサーバーにログオンしていない場合、ログ コレクターでは、資格情報を入力するように求められます。  
  
2.  収集したログ ファイルを保存する場所のメッセージが表示されたら、既定の場所を選択できます**\\\ < ServerName\ > \logs**、または別の場所を指定します。 既定の場所を受け入れるようにクリックして**次**します。 場所を変更する] をクリックして**参照**、ログ ファイルを保存するフォルダーに移動し、をクリックして、**保存**します。  
  
    > [!NOTE]
    >  ログ ファイルのファイル名を指定する必要はありません。 Log Collector は、コンピューター名と、ファイルのタイムスタンプを連結することにより、zip ファイル コレクションを名します。  
  
3.  ログを収集している進行状況バーが表示されます。  
  
4.  ログ コレクション ファイルの内容を表示するには、選択、**ログが保存されているファイルの場所を開く**チェック ボックスをオンし] をクリックして**閉じます**ウィザードを終了し、ログ コレクション ファイルを開くにします。  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>ウィザードを使用してネットワーク コンピューターで Log Collector を実行するには  
  
1.  参照**%system%\Program Files (x86) \Windows Server Essentials Log Collector**、ファイルをダブルクリック**LogCollector.exe**します。  
  
    > [!NOTE]
    >  管理者特権を持つネットワーク コンピューターにログオンしていない場合、ユーザー名と表示されたら、パスワードを入力し、クリックして**次**します。  
  
2.  次のように、収集するログを選択します。  
  
    1.  選択、**サーバーのログ ファイル**サーバー上のログ ファイルを収集するチェック ボックスをオンします。  
  
    2.  **クライアント コンピューターのログ ファイル (このコンピューター)**既定では、Log Collector が実行しているネットワーク コンピューターからログを収集することを示すチェック ボックスをオンします。 サーバー ログを収集する場合は、オフ、**クライアント コンピューターのログ ファイル (このコンピューター)**チェック ボックスをオンします。  
  
    3.  をクリックして**次**します。  
  
3.  されたら、サーバーの管理者のユーザー名とパスワードを入力し、をクリックして**次**します。  
  
4.  クリックして、ログ ファイルを保存する場所を入力または参照**次**します。  
  
    > [!NOTE]
    >  ログ ファイルのファイル名を指定する必要はありません。 Log Collector は、コンピューター名と、ファイルのタイムスタンプを連結することにより、zip ファイル コレクションを名します。  
  
5.  ログを収集している進行状況バーが表示されます。  
  
6.  ログ コレクション ファイルの内容を表示するには、選択、**ログが保存されているファイルの場所を開く**チェック ボックスをオンし] をクリックして**閉じます**ウィザードを終了し、ログ コレクション ファイルを開くにします。  
  
### <a name="running-the-log-collector-manually"></a>Log Collector を手動で実行しています。  
 Log Collector をインストールしたら、ツールを実行する、スケジュールされたタスクが作成されます。 その後から Log Collector を実行することができます、**スケジュールされたタスク マネージャー**ウィザードを開始で問題がある場合に、ウィザードを使用しません。  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>サーバーで Log Collector を手動で実行するには  
  
1.  直接またはリモート サーバーにログオンします。  
  
2.  開いている、**タスク スケジューラ**します。  
  
3.  ルートに、**タスク スケジューラ ライブラリ**、という名前のスケジュールされたタスクを参照**LogCollector**します。  
  
4.  右クリック**LogCollector**、] をクリックし、**実行**します。 Log Collector は、サーバーで、既定のフォルダーに、ログを配置**\\\ < ServerName\ > \Logs**します。 ログを配置する場合、フォルダーに対する書き込みアクセス許可がない場合、またはフォルダーが存在しない場合、**< temp\ >**サブディレクトリ。  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>ネットワーク コンピューターで Log Collector を手動で実行するには  
  
1.  ログオン直接またはリモート ネットワーク コンピューターにします。  
  
2.  開いている、**タスク スケジューラ**します。  
  
3.  ルートに、**タスク スケジューラ ライブラリ**、という名前のスケジュールされたタスクを参照**LogCollector**します。  
  
4.  右クリック**LogCollector**、] をクリックし、**実行**します。 Log Collector ログを配置します、**< temp\ >**ネットワーク コンピューター上のフォルダーです。
