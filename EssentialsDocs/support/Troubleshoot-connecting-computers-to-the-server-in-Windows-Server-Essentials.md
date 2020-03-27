---
title: Windows Server Essentials 内のサーバーにコンピューターを接続する場合のトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4e2a707bf72ca7e371b6503116262e737102c769
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318591"
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Windows Server Essentials 内のサーバーにコンピューターを接続する場合のトラブルシューティング

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials 
  
 このトピックでは、Windows Server Essentials または Windows Server Essentials を実行しているサーバーにコンピューターを接続するときに発生する可能性がある問題のトラブルシューティングのガイダンスを示します。  
  
> [!NOTE]
>  Windows Server Essentials および Windows Server Essentials コミュニティの最新のトラブルシューティング情報については、 [Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserveressentials)を参照することをお勧めします。 Windows Server Essentials フォーラムは、ヘルプを検索したり、質問したりするために最適な場所です。  
  
 このトピックでは、次の問題に関する解決策を取り上げます。  
  

-   問題 1:[問題 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   問題 2:[問題 2](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   問題 3:[問題 3](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   問題 4:[問題 4](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   問題 5:[問題 5](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   問題 6:[問題 6](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   問題 7:[問題 7](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   問題 8:[問題 8](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   問題 9:[問題 9](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   問題 10:[問題 10](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   問題 11:[問題 11](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

-   問題 1:[問題 1](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   問題 2:[問題 2](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   問題 3:[問題 3](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   問題 4:[問題 4](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   問題 5:[問題 5](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   問題 6:[問題 6](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   問題 7:[問題 7](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   問題 8:[問題 8](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   問題 9:[問題 9](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   問題 10:[問題 10](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   問題 11:[問題 11](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

  
##  <a name="issue-1"></a><a name="BMRK_Package"></a>問題1  
 **問題**  
  
 パッケージのインストールが成功しませんでした。 Windows Server Essentials コネクターをもう一度インストールしてみてください。 問題が解決しない場合は、コンピューターをサーバーに接続するときに、ネットワーク管理者のエラーに問い合わせてください  
  
 **説明**  
  
 この問題は、Windows Server Essentials を実行しているサーバーにコンピューターを接続しているときに、他の Windows 更新プログラムまたはアプリケーションのインストールが保留中で、コネクタのインストールがキャンセルされた場合に発生する可能性があります。  
  
 **ソリューション**  
  
 他のすべての更新プログラムまたはアプリケーション インストールを完了します。 ダイアログが表示されたら、コンピューターを再起動します。  
  
##  <a name="issue-2"></a><a name="BKMK_ConnectorIssue2"></a>問題2  
 **問題**  
  
 コンピューターを Windows Server Essentials に参加させることはできません  
  
 **説明**  
  
 コンピューター名に ASCII 以外の文字が含まれているコンピューターを Windows Server Essentials に参加させることはできません。 コンピューター名に ASCII 以外の文字が含まれている場合、「予期しないエラーが発生しました」というエラー メッセージが表示されます。  
  
 **ソリューション**  
  
 クライアントコンピューターの名前を ASCII 文字のみが含まれる名前に変更してから、コンピューターを Windows Server Essentials にもう一度追加してみてください。  
  
##  <a name="issue-3"></a><a name="BKMK_ConnectorIssue2a"></a>問題3  
 **問題**  
  
 コンピューターをサーバーに接続すると、コネクタソフトウェアのインストールがキャンセルされてエラーが発生する  
  
 **説明**  
  
 コンピューターをサーバーに接続できるようにするには、SYSTEM アカウントに、Windows Server Essentials ダッシュボードに表示されるサーバーフォルダーに対するフルコントロールのアクセス許可が必要です。 必要なアクセス許可が付与されていない場合、「コネクター ソフトウェアのインストールが取り消されます」というエラー メッセージが表示されます。  
  
 **ソリューション**  
  
 SYSTEM アカウントに、各サーバー フォルダーに対する **[フル コントロール]** アクセス許可を付与します。  
  
#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>サーバー フォルダーに対するフル コントロール アクセス許可を SYSTEM アカウントに付与するには  
  
1.  Windows Server Essentials ダッシュボードを開きます。  
  
2.  **[記憶域]** をクリックし、 **[サーバー フォルダー]** をクリックします。  
  
3.  サーバー フォルダを右クリックし、 **[フォルダーを開く]** をクリックします。 ( **[フォルダーを開く]** オプションが表示されない場合、対象フォルダーでアクセス許可を設定する必要はありません。)  
  
4.  Windows エクスプローラー上部にあるネットワーク パスで、[サーバー共有] をクリックし、対象サーバー上の共有フォルダーを表示します。 たとえば、パスが **[ネットワーク] > Server01 > [ファイル履歴のバックアップ]** の場合、**Server01** をクリックします。  
  
5.  サーバー フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
6.  **[セキュリティ]** タブをクリックします。  
  
7.  SYSTEM アカウントに対して **[フル コントロール]** を選択できない場合、 **[編集]** 、 **[SYSTEM]** とクリックします。 **[システムのアクセス許可]** で、 **[フル コントロール]** の隣にある **[許可]** チェック ボックスをオンにします。  
  
8.  **[OK]** を 2 回クリックし、アクセス許可を更新して **[プロパティ]** を閉じます。  
  
##  <a name="issue-4"></a><a name="BKMK_ConnectorIssueNetFramework"></a>問題4  
 **問題**  
  
 このアプリケーションを実行するには、コンピューターをサーバーに接続するときに、次のいずれかのバージョンの .NET Framework: V 4.5.50709 "エラーをインストールする必要があります。  
  
 **説明**  
  
 Windows Server Essentials または Windows Server Essentials を実行しているサーバーにコンピューターを接続すると、ウィザードは .NET Framework バージョン4.5.50709 をコンピューターにインストールしようとします。 ただし、以前のリリースの .NET Framework バージョン4.5 が存在する場合、更新されたリリースをインストールすることはできません。また、このアプリケーションを実行するには、次のいずれかのバージョンの .NET Framework をインストールする必要があります。V 4.5.50709。 適切なバージョンの .NET Framework を取得する方法については、割り当て発行者に問い合わせてください。  
  
 **ソリューション**  
  
 .NET Framework 4.5 をコンピューターからアンインストールしてから、コンピューターをサーバーに接続します。  
  
#### <a name="to-uninstall-net-framework-45"></a>.NET Framework 4.5 をアンインストールするには  
  
1.  クライアント コンピューターの **[スタート]** ページで、 **[コントロール パネル]** を開きます。  
  
2.  [コントロール パネル] の **[プログラム]** で、 **[プログラムのアンインストール]** をクリックします。  
  
3.  **[Microsoft .NET Framework 4.5]** を右クリックし、 **[アンインストール]** をクリックします。  
  
4.  .NET Framework 4.5 のアンインストールが正常に実行された後、サーバーにコンピューターを接続します。 適切なリリースの .NET Framework 4.5 がコネクター ソフトウェアと一緒にインストールされます。  
  
##  <a name="issue-5"></a><a name="BKMK_Time"></a>問題5  
 **問題**  
  
 サーバーを取得できません。 この問題を解決するには、ネットワークの担当者にお問い合わせください。 というエラー メッセージが表示される  
  
 **説明**  
  
 接続対象コンピューターの日時がサーバーの日時と同期されていない場合に生じる可能性があります。  Windows Server Essentials と Windows Server Essentials では、時刻同期サービスを使用して、Windows Server Essentials または Windows Server Essentials ネットワークで実行されているコンピューターの日付と時刻を同期します。 既定の認証プロトコルでは認証プロセスの一環としてサーバー時刻が使用されるため、同期された時刻は重要です。 たとえば、クライアントコンピューターの時計が正しい日付と時刻に同期されていない場合、Windows Server Essentials または Windows Server Essentials の認証では、ログオン要求が誤って侵入の試みとして解釈され、ユーザーへのアクセスが拒否されることがあります。  
  
 これは、サーバーの空きメモリが5% 未満の場合に発生する可能性があります。  
  
 Windows Essentials Server に対する VPN 接続が既に確立されていて、ドメイン アドレスを使用して内部設置型のコネクター ソフトウェアを設定しようとすると発生する可能性があります。  
  
 **ソリューション**  
  
1.  クライアント コンピューターの日時をサーバー上の日時と同期します。 次に、サーバーとコンピューターを接続します。  
  
2.  サーバー側の一部のアプリケーションを閉じてから、サーバーにコンピューターを接続します。  
  
3.  VPN 接続を閉じ、サーバーにコンピューターを接続します。  
  
#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>クライアント コンピューターの日時を変更するには  
  
1. クライアント コンピューターの スタート ページで、**コントロール パネル** を開きます。  
  
2. [コントロール パネル] で、 **[時計、言語、および地域]** をクリックし、 **[日付と時刻]** をクリックします。  
  
3. **[日付と時刻の変更]** をクリックして日付と時刻を正しく設定し、 **[OK]** をクリックします。  
  
4. **[OK]** をクリックし、[コントロール パネル] を閉じます。  
  
5. クライアント コンピューターのサーバーへの接続を再試行します。 手順については、「コンピューターをサーバーに接続する方法」を参照してください。  
  
   それでもクライアント コンピューターをサーバーに接続できない場合は、サーバー上の日時が正しいことを確認してください。 日時が正しくない場合、変更します。  
  
#### <a name="to-change-the-date-and-time-on-the-server"></a>サーバー上の日付と時刻を変更するには  
  
1.  Windows Server Essentials または Windows Server Essentials のインストールと構成時に設定したパスワードを使用して、サーバーにログオンします。  
  
    > [!NOTE]
    >  サーバーをリモートで管理している場合、リモート デスクトップ接続を使用してサーバーにログオンする必要があります。  
  
2.  **[スタート]** ページで、 **[コントロール パネル]** を開きます。  
  
3.  [コントロール パネル] で、 **[時計、言語、および地域]** をクリックし、 **[日付と時刻]** をクリックします。  
  
4.  **[日付と時刻の変更]** をクリックして日付と時刻を正しく設定し、 **[OK]** をクリックします。  
  
5.  **[OK]** をクリックし、[コントロール パネル] を閉じます。  
  
6.  クライアント コンピューターで、サーバーへの接続を再試行します。 手順については、「コンピューターをサーバーに接続する方法」を参照してください。  
  
##  <a name="issue-6"></a><a name="BKMK_ServiceStopped"></a>問題6  
 **問題**  
  
 予期しないエラーが発生しました。 この問題を解決するには、ネットワークの担当者にお問い合わせください。 というエラー メッセージが表示される  
  
 **説明**  
  
 このエラー メッセージが表示された場合は、WSS Certificate Web Service が実行されていない可能性があります。  
  
 **ソリューション**  
  
 WSS Certificate Web Service を開始します。  
  
#### <a name="to-start-the-wss-certificate-web-service"></a>WSS Certificate Web Service を開始するには  
  
1.  サーバーの **[スタート]** ページで、 **[管理ツール]** を開きます。  
  
     **[管理ツール]** で **[インターネット インフォメーション サービス (IIS) マネージャー]** を右クリックし、 **[開く]** をクリックします。  
  
2.  ナビゲーション ウィンドウで、 **[WSS Certificate Web Service]** をクリックします。  
  
3.  **[操作]** ウィンドウで、 **[開始]** をクリックします。  
  
##  <a name="issue-7"></a><a name="BKMK_ConnectorIssueReconnect"></a>問題7  
 **問題**  
  
 接続の試行が失敗した後にコンピューターをサーバーに接続しようとすると、"この名前のコンピューターは既にサーバーに接続されています" という警告が表示されます。  
  
 **説明**  
  
 以前にコンピューターをサーバーに接続しようとしたときに、キャンセルまたは中断された場合は、もう一度接続しようとすると、次の警告が表示されることがあります。この名前のコンピューターは既にサーバーに接続されています。 これは、初めてサーバーに接続を試みたときに証明書が発行されているために生じます。  
  
 **解決策**: 同じ名前の他のコンピューターが対象のサーバーに接続されていないことが分かっている場合には、 **[次へ]** をクリックして次の手順を実行して、 **[コンピューターをサーバーに接続]** ウィザードを完了します。  
  
##  <a name="issue-8"></a><a name="BKMK_JoinWin7"></a>問題8  
 **問題**  
  
 Windows 7 Home が実行されているクライアント コンピューターをサーバーに接続しようとすると、コネクター ソフトウェアを実行するための Web ページが開くものの、クライアント コンピューターがサーバーに接続できない  
  
 **説明**  
  
 ネットワーク上のルーターでマルチキャストが有効になっている場合、Windows 7 Home Basic または Windows 7 Home Premium が実行されているクライアント コンピューターとサーバー間の通信が正しく行えません。  
  
 **ソリューション**  
  
 ルーターでマルチキャストを無効にします。 一部のルーターでは、RIP-2M ルーティング プロトコルの無効化もそれに含まれる場合があります。 詳細については、ルーターの製造元によって提供されているドキュメントを参照してください。  
  
##  <a name="issue-9"></a><a name="BKMK_ConnectorIssueAutologon"></a>問題9  
 **問題**  
  
 サーバーにコンピューターを接続した後、自動ログオンが機能しなくなった  
  
 **説明**  
  
 コンピューターを Windows Server Essentials に接続するときに、ユーザーアカウントに自動ログオンが設定されている場合、この設定はコンピューターにコネクタソフトウェアがインストールされているときに上書きされます。  
  
 **解決策**: この問題を解決するには、コンピューターをサーバーに接続するときに、ユーザー アカウントに使用するパスワードをメモしてください。 コネクター ソフトウェアのインストール後、そのアカウントを使用するように自動ログオンを構成します。  
  
> [!NOTE]
>  Windows Server Essentials ドメインアカウントには、既定のパスワードポリシー要件を満たすパスワードが必要です。  
  
##  <a name="issue-10"></a><a name="BKMK_ConnectorIssueOldLogs"></a>問題10  
 **問題**  
  
 プレリリース版のコネクター ソフトウェアをアンインストールしても既存のログが削除されない  
  
 **説明**  
  
 プレリリース (ベータ版または RC) 版の Windows Server Essentials からリリース版に更新した後、サーバーに接続されている各コンピューターからコネクタソフトウェアを削除してから、コンピューターを再接続して、リリースされたをインストールする必要があります。コネクタソフトウェアのバージョン。  
  
 ただし、ネットワーク コンピューターからコネクター ソフトウェアを削除しても、そのコンピューター上の %ProgramData%\Microsoft\Windows Server\Logs\ フォルダー内の既存のログ ファイルは削除されません。 Logs フォルダーを削除しないと、Windows Server Essentials のリリース版にコンピューターを接続したときに、ログファイルが破損する可能性があります。  
  
 **解決策**: ログ ファイルの破損を回避するには、Logs フォルダーを手動で削除してから、更新されたサーバーに対してクライアント コンピューターを再接続します。  
  
#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>サーバーの更新後にログ ファイルを破損することなくコンピューターに再接続するには  
  
1.  クライアント コンピューターからコネクター ソフトウェアをアンインストールします。  
  
2.  %ProgramData%\Microsoft\Windows Server\ フォルダーから Logs フォルダーを削除します。  
  
3.  コンピューターを再度サーバーに接続します。 それにより、リリース版のコネクター ソフトウェアがインストールされ、新しい Logs フォルダーとログ ファイルが作成されます。  
  
##  <a name="issue-11"></a><a name="BKMK_UpgradeClientOS"></a>問題11  
 **問題**  
  
 クライアント コンピューター上でオペレーティング システムをアップグレードしたい  
  
 **説明**  
  
 コネクター ソフトウェアのインストール中に、クライアントのオペレーティング システムに対して、クライアントがコネクターの前提条件すべてを満たしていることを確認するための各種チェックが実行されます。 コネクター ソフトウェアのインストール後にクライアントのオペレーティング システムをアップグレードすると、一部の前提条件が満たされず、クライアント コネクターで障害が発生する可能性があります。  
  
 **ソリューション**  
  
 クライアントのオペレーティング システムを別のバージョンにアップグレードするには (たとえば、Windows XP を Windows Vista へ、または Windows Vista を Windows 7 へアップグレードする場合)、コネクター ソフトウェアをアンインストールする必要があります。 [コントロール パネル] の **[プログラムの追加と削除]** を使用します。 クライアントのオペレーティングシステムのアップグレードが完了したら、 http://<*server*> を開き、Web ブラウザーで [接続] を開いて、クライアントコネクタを再インストールできます。ここで <*server*> は、Windows server Essentials サーバーの名前です。  
  
 コネクター ソフトウェアがインストールされているクライアントをアップグレードした場合には、 **[プログラムの追加と削除]** または **[プログラムと機能]** を使用してコネクター ソフトウェアをアンインストールします。 その後、コネクター ソフトウェアを再びインストールします。  
  
## <a name="see-also"></a>参照  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)  
  
-   [Windows 2012 Server Essentials ConnectComputer のトラブルシューティング (TechNet Wiki)](https://social.technet.microsoft.com/wiki/contents/articles/14370.windows-2012-server-essentials-connectcomputer-troubleshooting.aspx)
