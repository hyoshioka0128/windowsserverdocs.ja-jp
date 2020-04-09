---
title: Windows Server Essentials Log Collector の実行
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 0d340223-fa24-4c75-ba8e-b654feb120ab
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6aac2ed382321349d39874c7db7617f6da845919
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852275"
---
# <a name="run-the-windows-server-essentials-log-collector"></a>Windows Server Essentials Log Collector の実行
Windows Server Essentials Log Collector は、サーバーまたはネットワーク上のコンピューターから実行できます。 サーバーから Log Collector を実行した場合、ログをサーバーからのみ収集できます。 ネットワーク コンピューターから Log Collector を実行した場合、そのコンピューターのログに加えて、サーバーから収集するログを選択できます。  
  
 Log Collector を実行するには、適切な管理者権限が必要です。 サーバーのログ ファイルを収集している場合は、サーバーの管理者である必要があります。ネットワーク コンピューターのログ ファイルを収集している場合、そのコンピューターのクライアント管理者である必要があります。  
  
#### <a name="to-run-the-log-collector-on-the-server-by-using-the-wizard"></a>ウィザードを使用してサーバーで Log Collector を実行するには  
  
1. サーバーの **[スタート]** ページで、 **[Windows Server Essentials Log Collector]** をクリックします。  
  
   > [!NOTE]
   > - Log Collector プログラムが**スタート**ページに表示されない場合は、 **%system%\program files Files (X86) \Windows Server Essentials Log collector**に移動し、 **[logcollector]** をダブルクリックします。  
   >   -   サーバーに管理者権限でログオンしていない場合は、ログ コントローラーでは資格情報の入力を求めるダイアログが表示されます。  
  
2. 収集したログファイルを保存する場所の入力を求められたら、既定の場所を選択するか、 **\\< \\ServerName\>\logs**を選択するか、別の場所を指定します。 既定の場所を承諾するには、 **[次へ]** をクリックします。 場所を変更するには、 **[参照]** をクリックし、ログ ファイルを保存するフォルダーに移動して、 **[保存]** をクリックします。  
  
   > [!NOTE]
   >  ログ ファイルのファイル名を指定する必要はありません。 ログコレクターは、ファイルのコンピューター名とタイムスタンプを連結して、zip ファイルコレクションに名前を指定します。  
  
3. ログの収集中には進行状況バーが表示されます。  
  
4. ログ コレクション ファイルの内容を表示するには、 **[ログが保存されている場所を開く]** チェック ボックスをオンにし、 **[閉じる]** をクリックしてウィザードを閉じ、ログ コレクション ファイルを開きます。  
  
#### <a name="to-run-the-log-collector-on-a-network-computer-by-using-the-wizard"></a>ウィザードを使用してネットワーク コンピューターで Log Collector を実行するには  
  
1.  **%System%\program files Files (x86) \Windows Server Essentials Log Collector**を参照し、ファイル**logcollector**をダブルクリックします。  
  
    > [!NOTE]
    >  ネットワーク コンピューターに管理者権限でログオンしていない場合、ダイアログが表示されたら、ユーザー名とパスワードを入力して、 **[次へ]** をクリックします。  
  
2.  次のように収集するログを選択します。  
  
    1.  **[サーバー ログ ファイル]** チェック ボックスをオンにして、サーバー上のログ ファイルを収集します。  
  
    2.  既定では、 **[クライアント コンピューターのログ ファイル (このコンピューター)]** チェック ボックスはオンになっています。これは、Log Collector が実行しているネットワーク コンピューターからログを収集することを示しています。 サーバー ログを収集するのみの場合は、 **[クライアント コンピューターのログ ファイル (このコンピューター)]** チェック ボックスをオフにします。  
  
    3.  **[次へ]** をクリックします。  
  
3.  ダイアログが表示されたら、サーバー管理者のユーザー名とパスワードを入力し、 **[次へ]** をクリックします。  
  
4.  ログ ファイルを保存する場所を入力または参照して、 **[次へ]** をクリックします。  
  
    > [!NOTE]
    >  ログ ファイルのファイル名を指定する必要はありません。 ログコレクターは、ファイルのコンピューター名とタイムスタンプを連結して、zip ファイルコレクションに名前を指定します。  
  
5.  ログの収集中には進行状況バーが表示されます。  
  
6.  ログ コレクション ファイルの内容を表示するには、 **[ログが保存されている場所を開く]** チェック ボックスをオンにし、 **[閉じる]** をクリックしてウィザードを閉じ、ログ コレクション ファイルを開きます。  
  
### <a name="running-the-log-collector-manually"></a>Log Collector を手動で実行する  
 Log Collector がインストールされると、ツールを実行するためにスケジュールされたタスクが作成されます。 ウィザードの開始で問題が発生した場合は、ウィザードを使用せずに、後で **[スケジュールされたタスク マネージャー]** から Log Collector を実行できます。  
  
##### <a name="to-manually-run-the-log-collector-on-the-server"></a>サーバーで Log Collector を手動で実行するには  
  
1.  サーバーに直接またはリモートでログオンします。  
  
2.  **[タスク スケジューラ]** を開きます。  
  
3.  **[タスク スケジューラ ライブラリ]** のルートで、 **[LogCollector]** という名前のスケジュールされたタスクを参照します。  
  
4.  **[LogCollector]** を右クリックし、 **[実行]** をクリックします。 ログコレクターは、サーバーの既定のフォルダー **\\\\< ServerName\>\Logs**にログを配置します。 フォルダーに対する書き込みアクセス許可がない場合、またはフォルダーが存在しない場合、ログは **< temp\>** サブディレクトリに配置されます。  
  
##### <a name="to-manually-run-the-log-collector-on-a-network-computer"></a>ネットワーク コンピューターで Log Collector を手動で実行するには  
  
1.  ネットワーク コンピューターに直接またはリモートでログオンします。  
  
2.  **[タスク スケジューラ]** を開きます。  
  
3.  **[タスク スケジューラ ライブラリ]** のルートで、 **[LogCollector]** という名前のスケジュールされたタスクを参照します。  
  
4.  **[LogCollector]** を右クリックし、 **[実行]** をクリックします。 ログコレクターは、ネットワークコンピューターの **< temp\>** フォルダーにログを配置します。
