---
title: "Windows Server Essentials でのサーバーに接続しているコンピューターをトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e45b3d89-c057-4c70-a627-86fb06dd22aa
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9b0d11be08840ecedabab6fd4e96f5d453ea4857
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-connecting-computers-to-the-server-in-windows-server-essentials"></a>Windows Server Essentials でのサーバーに接続しているコンピューターをトラブルシューティングします。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象: 
  
 このトピックでは、コンピューターを Windows Server Essentials を実行しているサーバーまたは Windows Server Essentials に接続するときに発生する可能性のある問題のトラブルシューティングの指針を示します。  
  
> [!NOTE]
>  Windows Server Essentials と Windows Server Essentials コミュニティの最新のトラブルシューティング情報について、ことをお勧めを参照する、[Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserveressentials)します。 Windows Server Essentials フォーラムは、ヘルプについては、検索するか、質問をお勧めします。  
  
 ここでは、次の問題の解決方法を説明します。  
  

-   問題 1:[問題 1](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   問題 2: [2 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   問題 3: [3 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   問題 4: [4 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   問題 5: [5 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   問題 6: [6 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   問題 7: [7 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   問題 8: [8 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   問題 9: [9 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   問題 10: [10 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   問題 11: [11 の発行](Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

-   問題 1:[問題 1](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BMRK_Package)  
  
-   問題 2: [2 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2)  
  
-   問題 3: [3 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssue2a)  
  
-   問題 4: [4 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueNetFramework)  
  
-   問題 5: [5 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_Time)  
  
-   問題 6: [6 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ServiceStopped)  
  
-   問題 7: [7 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueReconnect)  
  
-   問題 8: [8 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_JoinWin7)  
  
-   問題 9: [9 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueAutologon)  
  
-   問題 10: [10 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_ConnectorIssueOldLogs)  
  
-   問題 11: [11 の発行](../support/Troubleshoot-connecting-computers-to-the-server-in-Windows-Server-Essentials.md#BKMK_UpgradeClientOS)  

  
##  <a name="BMRK_Package"></a>問題 1  
 **問題**  
  
 インストールが成功しなかったパッケージが表示されます。 Windows Server Essentials Connector をもう一度インストールしてみます。 問題が解決しない場合にお問い合わせください、ネットワーク管理者のエラーをサーバーにコンピューターを接続するときに  
  
 **説明**  
  
 この問題は、他の Windows 更新プログラムまたはアプリケーションのインストールが保留中とコネクタのインストールが取り消されたときに、Windows Server Essentials を実行しているサーバーにコンピューターを接続する場合に発生する可能性があります。  
  
 **解決策**  
  
 その他のすべての更新プログラムまたはアプリケーションのインストールを完了します。 要求された場合は、コンピューターを再起動します。  
  
##  <a name="BKMK_ConnectorIssue2"></a>問題 2  
 **問題**  
  
 Windows Server Essentials にコンピューターを参加させることはできません。  
  
 **説明**  
  
 コンピューター名に ASCII 以外の文字があるコンピューターは、Windows Server Essentials に参加することはできません。 コンピューター名には、非 ASCII 文字が含まれている場合、「予期しないエラーが発生しました。」エラー メッセージが表示されます。  
  
 **解決策**  
  
 ASCII 文字のみが含まれている名前で、クライアント コンピューターの名前を変更し、コンピューターを Windows Server Essentials を再度追加しようとしてください。  
  
##  <a name="BKMK_ConnectorIssue2a"></a>問題 3  
 **問題**  
  
 エラーを取得する、コネクタ ソフトウェアのインストールが取り消されたコンピューターをサーバーに接続するときに  
  
 **説明**  
  
 コンピューターをサーバーに接続できるようにするには、システム アカウントは、Windows Server Essentials ダッシュ ボードに表示されるサーバー フォルダーに対するフル コントロール アクセス許可が必要です。 必要なアクセス許可が与えられていない場合は、エラー「コネクター ソフトウェアのインストールが取り消された」メッセージ。  
  
 **解決策**  
  
 システム アカウントに付与**フル コントロール**各サーバー フォルダーに対するアクセスを許可します。  
  
#### <a name="to-grant-the-system-account-full-control-permissions-on-a-server-folder"></a>システム アカウントにサーバー フォルダーに対するフル コントロール アクセス許可を付与するには  
  
1.  Windows Server Essentials ダッシュ ボードを開きます。  
  
2.  をクリックして**記憶域**、] をクリックし、**サーバー フォルダー**します。  
  
3.  サーバー フォルダーを右クリックし、をクリックして**フォルダーを開き**します。 (表示されない場合、**フォルダーを開き**オプション、必要はありません、フォルダーのアクセス許可を設定します)。  
  
4.  Windows エクスプ ローラーの上部にあるネットワーク パスが、サーバー上の共有フォルダーを表示するサーバー共有] をクリックします。 たとえば、パスは**ネットワーク > Server01 > File History Backups**、] をクリックして**Server01**します。  
  
5.  サーバー フォルダーを右クリックし、をクリックして**プロパティ**します。  
  
6.  をクリックして、**セキュリティ**] タブ。  
  
7.  場合**フル コントロール**はシステム アカウントを許可しない] をクリックして**編集**、] をクリックし、**システム**します。 **System のアクセス許可**を選択、**許可**の横にあるチェック ボックスをオン**フル コントロール**します。  
  
8.  をクリックして**OK** 2 回クリックして、アクセス許可を更新し、閉じます**プロパティ**します。  
  
##  <a name="BKMK_ConnectorIssueNetFramework"></a>問題 4  
 **問題**  
  
 このアプリケーションの実行を取得する、次のバージョンの .NET Framework のいずれかをインストールする必要があります V4.5.50709"サーバーにコンピューターを接続するときにエラー。  
  
 **説明**  
  
 コンピューターを Windows Server Essentials を実行しているサーバーまたは Windows Server Essentials に接続するときに、ウィザードは、コンピューター上の .NET Framework バージョン 4.5.50709 をインストールしようとします。 ただし、.NET Framework バージョン 4.5 のそれより前のリリースが存在する場合、更新リリースをインストールすることはできませんし、このエラー メッセージで、接続の試行が失敗します。このアプリケーションを実行する、次のバージョンの、.NET Framework のいずれかをインストールする必要があります。V4.5.50709。 .NET Framework の適切なバージョンを取得する方法については、アプリケーション発行者に問い合わせてください。  
  
 **解決策**  
  
 .NET Framework 4.5 をコンピューターからアンインストールし、サーバーにコンピューターを接続します。  
  
#### <a name="to-uninstall-net-framework-45"></a>.NET Framework 4.5 をアンインストールするには  
  
1.  **開始**ページを開いて、クライアント コンピューターの**コントロール パネルの [**します。  
  
2.  コントロール パネルで、[**プログラム**、] をクリックして**プログラムのアンインストール**します。  
  
3.  右クリック**Microsoft .NET Framework 4.5**、] をクリックし、**アンインストール**します。  
  
4.  .NET Framework 4.5 が正常にアンインストールした後は、コンピューターをサーバーに接続します。 適切なリリースの .NET Framework 4.5 がコネクター ソフトウェアと一緒にインストールされます。  
  
##  <a name="BKMK_Time"></a>問題 5  
 **問題**  
  
 取得する、サーバーは使用できません。 この問題を解決するには、ネットワークの担当者にお問い合わせください。 コンピューターをサーバーに接続するときにエラー  
  
 **説明**  
  
 これは、接続されているコンピューターの日時が日時と、サーバーの時刻同期されていない場合に発生することができます。  Windows Server Essentials と Windows Server Essentials は、Windows Server Essentials または Windows Server Essentials ネットワークで実行しているコンピューターの日時を同期するのに時刻の同期サービスを使用します。 既定の認証プロトコルが認証プロセスの一環としてサーバーの時刻を使用するため、同期された時刻は重要です。 たとえば場合、クライアント コンピューターの時計が正しい日付と時刻、Windows Server Essentials に同期されていない、または Windows Server Essentials の認証が間違って可能性があります侵入の試みとしてのログオン要求を解釈し、ユーザーに対してアクセスが拒否します。  
  
 これは、サーバーの空きメモリが 5% 未満の場合に発生することができます。  
  
 これは、Windows Essentials サーバーに VPN 接続が既にあるしようとして、ドメイン アドレスを使用して、コネクタ ソフトウェアを社内設置型を構成する場合に発生することができます。  
  
 **解決策**  
  
1.  サーバー上のもので、クライアント コンピューターの日時を同期します。 コンピューターをサーバーに接続します。  
  
2.  サーバー側では、一部のアプリケーションを閉じて、サーバーにコンピューターを接続します。  
  
3.  VPN 接続を閉じて、サーバーにコンピューターを接続します。  
  
#### <a name="to-change-the-date-and-time-on-the-client-computer"></a>クライアント コンピューターの日時を変更するには  
  
1.  クライアント コンピューターの [開始] ページで、開く**コントロール パネルの [**します。  
  
2.  コントロール パネルで、をクリックして**時計、言語、および地域**、] をクリックし、**日付と時刻**します。  
  
3.  をクリックして**日付と時刻を変更する**を正しい日付と時刻、日付と時刻を設定し、[クリックして**OK**します。  
  
4.  をクリックして**OK**、し、コントロール パネル] を閉じます。  
  
5.  クライアント コンピューターをサーバーに接続を再試行します。 手順については、コンピューターをサーバーに接続するを参照してください。  
  
 それでも接続できないクライアント コンピューターをサーバーに、日付とサーバーの時刻が正しいことを確認します。 日付と時刻が正しくない場合は、それらを変更します。  
  
#### <a name="to-change-the-date-and-time-on-the-server"></a>日付とサーバーの時刻を変更するには  
  
1.  Windows Server Essentials または Windows Server Essentials のインストールと構成で設定したパスワードを使用して、サーバーにログオンします。  
  
    > [!NOTE]
    >  サーバーをリモートで管理している場合は、リモート デスクトップ接続を使用して、サーバーにログオンする必要があります。  
  
2.  **開始**] ページで、開く**コントロール パネルの [**します。  
  
3.  コントロール パネルで、をクリックして**時計、言語、および地域**、] をクリックし、**日付と時刻**します。  
  
4.  をクリックして**日付と時刻を変更する**を正しい日付と時刻、日付と時刻を設定し、[クリックして**OK**します。  
  
5.  をクリックして**OK**、し、コントロール パネル] を閉じます。  
  
6.  クライアント コンピューターでは、クライアント コンピューターをサーバーに接続を再試行します。 手順については、コンピューターをサーバーに接続するを参照してください。  
  
##  <a name="BKMK_ServiceStopped"></a>問題 6  
 **問題**  
  
 取得するが、予期しないエラーが発生しました。 この問題を解決するには、ネットワークの担当者にお問い合わせください。 コンピューターをサーバーに接続するときにエラー  
  
 **説明**  
  
 このエラー メッセージを表示する場合に、WSS Certificate Web Service が実行されていない可能性があります。  
  
 **解決策**  
  
 WSS Certificate Web Service を開始します。  
  
#### <a name="to-start-the-wss-certificate-web-service"></a>WSS Certificate Web Service を開始するには  
  
1.  サーバーの**開始**] ページで、開く**管理ツール**します。  
  
     **管理ツール**、右クリック**インターネット インフォメーション サービス (IIS) マネージャー**、] をクリックし、**開く**します。  
  
2.  ナビゲーション ウィンドウで、をクリックして**WSS Certificate Web Service**します。  
  
3.  **アクション**] ウィンドウで、をクリックして**開始**します。  
  
##  <a name="BKMK_ConnectorIssueReconnect"></a>問題 7  
 **問題**  
  
 この名前のコンピューターがサーバーに既に接続されている警告が表示されるコンピューターをサーバーに接続試行が失敗後にもう一度接続しようとすると、  
  
 **説明**  
  
 場合は、コンピューターをサーバーに接続する以前の試みがキャンセルまたは、中断した場合、もう一度接続しようとするときに次の警告が表示される可能性があります。この名前のコンピューターがサーバーに既に接続されています。 これは、初めてサーバーに接続しようとしたときに、証明書が発行されたために発生します。  
  
 **ソリューション**ことと同じ名前には、その他のコンピューターが既に接続されていないサーバーに場合は、] をクリックして**次**、次の手順を完了して、**コンピューターをサーバーに接続**ウィザード。  
  
##  <a name="BKMK_JoinWin7"></a>問題 8  
 **問題**  
  
 サーバーに Windows 7 Home を実行しているクライアント コンピューターに接続しようとすると、コネクタ ソフトウェアを実行するための Web ページが開きがクライアント コンピューターがサーバーに接続できません。  
  
 **説明**  
  
 ネットワーク上のルーターでマルチキャストを有効になっている場合は、サーバーと Windows 7 Home Basic または Windows 7 Home Premium を実行しているクライアント コンピューター間の通信は正しく機能しません。  
  
 **解決策**  
  
 ルーターでマルチキャストを無効にします。 一部のルーターでは、RIP-2M ルーティング プロトコルを無効にすることなどがあります。 詳細については、ルーターの製造元によって提供されたドキュメントを参照してください。  
  
##  <a name="BKMK_ConnectorIssueAutologon"></a>問題 9  
 **問題**  
  
 自動ログオンは、コンピューターをサーバーに接続した後、機能が停止しました  
  
 **説明**  
  
 自動ログオンが設定されている場合、ユーザー アカウントのコンピューターを Windows Server Essentials に接続するときに、コネクタ ソフトウェアがコンピューターにインストールされているときに、設定が上書きされます。  
  
 **解決策**この問題を解決するには、コンピューターをサーバーに接続するときにユーザー アカウントを使用するパスワードに注意してください。 コネクタ ソフトウェアがインストールされた後、そのアカウントを使用して自動ログオンを構成します。  
  
> [!NOTE]
>  Windows Server Essentials ドメイン アカウントでは、既定のパスワード ポリシーの要件を満たすパスワードが必要です。  
  
##  <a name="BKMK_ConnectorIssueOldLogs"></a>問題 10  
 **問題**  
  
 プレリリース版のコネクター ソフトウェアをアンインストールしても、既存のログは削除されません。  
  
 **説明**  
  
 リリース版を Windows Server Essentials のプレリリース版 (ベータ版または RC) のバージョンから更新した後、サーバーに接続された各コンピューターからコネクタ ソフトウェアを削除し、コンピューターを接続します、コネクタ ソフトウェアのリリース バージョンをインストールするには、もう一度ください。  
  
 ただし、ネットワーク コンピューターからコネクタ ソフトウェアを削除すると、そのコンピューターで %ProgramData%\Microsoft\Windows \logs\ フォルダー内の既存のログ ファイルは削除されません。 Logs フォルダーを削除しない場合、ログ ファイルが破損する Windows Server Essentials のリリース バージョンにコンピューターを接続するとします。  
  
 **解決策**ログ ファイルの破損を避けるためには、手動で Logs フォルダーを削除、更新したサーバーにクライアント コンピューターを再接続する前にします。  
  
#### <a name="to-reconnect-a-computer-after-a-server-update-without-corrupting-the-log-files"></a>ファイル サーバーは、ログが破損することがなく更新後にコンピューターを再接続するには  
  
1.  クライアント コンピューターからコネクタ ソフトウェアをアンインストールします。  
  
2.  %ProgramData%\Microsoft\Windows \ フォルダーから Logs フォルダーを削除します。  
  
3.  サーバーにコンピューターをもう一度接続します。 コネクタ ソフトウェアは、新しい Logs フォルダーとログ ファイルの作成のリリース バージョンをインストールするとします。  
  
##  <a name="BKMK_UpgradeClientOS"></a>問題 11  
 **問題**  
  
 クライアント コンピューター上のオペレーティング システムをアップグレードしたいです。  
  
 **説明**  
  
 、コネクタ ソフトウェアのインストール中に、クライアントがコネクターの前提条件を満たしていることを確認するクライアント オペレーティング システムに対してさまざまなチェックが実行されます。 コネクタ ソフトウェアをインストールした後にクライアントのオペレーティング システムをアップグレードする場合、存在できない可能性があります、前提条件の一部とクライアント コネクターが失敗する可能性があります。  
  
 **解決策**  
  
 クライアントのオペレーティング システムを別のバージョンにアップグレードする前に (たとえば、Windows XP またはにアップグレードする Windows Vista から Windows 7、Windows Vista)、コネクタ ソフトウェアをアンインストールする必要があります。 使用**プログラムの追加と削除**コントロール パネルの [します。 クライアント コネクターを再インストール、http://< を開くことによって、クライアント オペレーティング システムのアップグレードが完了したら、します。*サーバー*>]、[Web ブラウザーで接続ここで <*サーバー*> は、Windows Server Essentials サーバーの名前です。  
  
 コネクタ ソフトウェアがインストールされたクライアントをアップグレードした場合を使用して**プログラムの追加/削除**または**プログラムと機能**コネクタ ソフトウェアをアンインストールします。 コネクタ ソフトウェアをもう一度インストールし、します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials を管理します。](../manage/Manage-Windows-Server-Essentials.md)  
  
-   [Windows 2012 Server Essentials ConnectComputer トラブルシューティング (TechNet Wiki)](https://social.technet.microsoft.com/wiki/contents/articles/14370.windows-2012-server-essentials-connectcomputer-troubleshooting.aspx)
