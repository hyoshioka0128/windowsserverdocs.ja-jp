---
title: "コンピューターのバックアップのトラブルシューティングを行うし、Windows Server Essentials でのエラーの復元"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 06/25/2013
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 37e79661442ba9f66a564b6c6c8fb57db1978454
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>コンピューターのバックアップのトラブルシューティングを行うし、Windows Server Essentials でのエラーの復元

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

バックアップ構成の問題、不完全または失敗したバックアップ、バックアップの正常性アラートの場合は、ファイル、フォルダー、またはシステムの完全復元の問題など、Windows Server Essentials でのコンピューターのバックアップのトラブルシューティングを行うには、これらの手順を使用します。  
  
> [!NOTE]
>  Windows Server Essentials コミュニティから最新のトラブルシューティング情報を参照してください、[Windows Server Essentials フォーラム](https://social.technet.microsoft.com/Forums//winserveressentials/threads)します。  
  
##  <a name="BKMK_TroubleshootBackupConfigurationIssues"></a>接続されているコンピューターのバックアップの構成に関する問題をトラブルシューティングします。  
 Windows Server Essentials サーバーにバックアップされているコンピューターのバックアップの構成に関する問題のトラブルシューティングを行うには、これらの手順を使用します。  
  
### <a name="errors"></a>エラー  
  
-   バックアップの構成が正常に完了しませんでした。  
  
-   コンピューターの情報の収集中エラー  
  
-   バックアップからコンピューターの削除中エラー  
  
### <a name="resolutions"></a>解決策  
  
##### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>接続されているコンピューターのバックアップを構成するときに発生したエラーのトラブルシューティング  
  
1.  ネットワーク デバイス経由、コンピューターがネットワークに接続されていることを確認します。  
  
2.  正しく機能しているネットワーク デバイスに接続しているコンピューターがネットワーク、電源が入ってにも接続されていることを確認することです。  
  
3.  Windows Server Client Backup Service と Windows Server Client Computer Backup Provider Service がサーバーで実行されていることを確認します。  
  
    ###### <a name="to-start-computer-backup-services-on-the-server"></a>サーバーのコンピューターのバックアップ サービスを開始するには  
  
    1.  サーバーで、をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、**サービス**します。  
  
    2.  下にスクロールし、クリックして**Windows Server Client Computer Backup Provider Service**します。 サービスの状態がない場合**開始**、サービスを右クリックし、[クリックして**開始**します。  
  
    3.  をクリックして**Windows Server Client Computer Backup Service**します。 サービスの状態がない場合**開始**、サービスを右クリックし、[クリックして**開始**します。  
  
    4.  閉じる**サービス**します。  
  
4.  クライアント コンピューターで Windows Server Client Computer Backup Provider Service が実行されていることを確認します。  
  
    ###### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>クライアント コンピューターのコンピューターのバックアップ サービスを開始するには  
  
    1.  クライアント コンピューターで、をクリックして**開始**、種類**サービス**で、**プログラムとファイルを検索**テキスト ボックスに、し、Enter キーを押します。  
  
    2.  下にスクロールし、クリックして**Windows Server Client Computer Backup Provider Service**します。 サービスの状態がない場合**開始**、サービスを右クリックし、[クリックして**開始**します。  
  
    3.  閉じる**サービス**します。  
  
5.  バックアップ データベースでエラーがあるかどうかを決定するアラートを確認します。 エラーがある場合は、バックアップ データベースを修復するアラートの指示に従います。  
  
6.  コンピューターから、Windows Server Essentials コネクタ ソフトウェアをアンインストールし、後で再インストールします。 詳細については、トピックを参照してください。[コネクタ ソフトウェアをアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)と[コネクタ ソフトウェアをインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)します。  
  
##  <a name="BKMK_TroubleshootaBackupThatDidNotCompleteProperly"></a>正常に完了しなかったバックアップをトラブルシューティングします。  
 バックアップが、失敗した状態、成功したバックアップの部分は、データがないはありませんを復元するために使用できます。 ただし、バックアップが、不完全な状態、しないすべての項目で指定されたバックアップの構成がバックアップされたが、一部のデータを復元するための利用可能な場合があります。  
  
### <a name="errors"></a>エラー  
  
-   バックアップが完了します。  
  
-   バックアップが失敗しました  
  
### <a name="resolutions"></a>解決策  
  
##### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>正常にバックアップされなかったボリュームを識別するには  
  
1.  Windows Server Essentials ダッシュ ボードを開き、クリックして**コンピューターとバックアップ**します。  
  
2.  ここでバックアップしなかったしない、正常に完了し、] をクリックし、コンピューターの名前をクリックして**コンピューターのプロパティを表示**で、**タスク**ウィンドウ。  
  
3.  バックアップが正常に完了されず] をクリックしをクリックして**の詳細を表示**します。  
  
4.  **バックアップの詳細**ダイアログ ボックスで、緑色のチェックが正常にバックアップされているすべてのボリュームの状態が表示されます。  
  
##### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>失敗したボリュームのバックアップのトラブルシューティング  
  
1.  正しく機能しているハード ディスクが有効で、コンピューターに接続されていることを確認することです。  
  
2.  実行**chkdsk/f/r**ハード ディスクのすべてのエラーを修正する (**/f**)、不良セクターから読み取り可能な情報を回復し、(**/r**)。 実行の詳細については**chkdsk**を参照してください[CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562)します。  
  
3.  コンピューターがないシャット ダウンまたはバックアップの実行中に、ネットワークから切断されていることを確認してください。  
  
4.  バックアップを実行するのには、各ボリュームに十分な空き領域があることを確認します。 バックアップには、VSS スナップショットを作成するクライアント コンピューターでは、いくつか追加のディスク領域が必要です。 予約済みのシステムではないすべてのボリュームで使用可能なディスク領域の 10% 以上が無料でなければなりません。 システム予約ボリューム上のボリューム サイズが 500 MB 未満の場合 VSS が必要です 32 MB の空き領域。スナップショットを作成するには場合は、ボリュームが 500 MB 以上で、VSS 320 MB の空き領域が必要です。  
  
     ボリュームに十分な空き領域がある場合は、これらの解決方法のいずれかを試してください。  
  
    -   ボリュームを拡張します。 システム予約ボリュームを除く任意のベーシックまたはダイナミック ボリュームを拡張することができます。  
  
        ###### <a name="to-extend-a-volume"></a>ボリュームを拡張するには  
  
        1.  コントロール パネルで、をクリックして**システムとセキュリティ**します。  
  
        2.  [**管理ツール**、] をクリックして**ハード ディスク パーティションの作成とフォーマット**します。  
  
        3.  拡張するボリュームを右クリックします。 場合**ボリュームの拡張**が有効にすると、そのオプションを選択します。 オプションが有効でない場合は、ボリュームを拡張することはできません。  
  
        4.  ボリュームを拡張するボリュームの拡張ウィザードの手順に従います。  
  
    -   多くの領域を利用できるようにするボリュームからコンテンツを削除します。  
  
        > [!NOTE]
        >  をシステム予約ボリュームの領域を解放する必要がある場合は、別のボリュームに、システム回復イメージを移動できます。 手順については、次を参照してください。[システム回復イメージを展開](https://technet.microsoft.com/library/dd744280\(v=ws.10\).aspx)します。  
  
    -   クライアントのバックアップからボリュームを除外します。 ボリューム上のデータのバックアップ コピーを維持するために重要な場合にのみは、これを実行します。  
  
        > [!WARNING]
        >  クライアント バックアップからシステム予約ボリュームを除外する場合、クライアント システムはバックアップされません、し、コンピューターでシステムの完全復元を実行することができなきます。  
  
5.  サーバー バックアップを正常に完了するのに十分なディスク領域がないことを示す、サーバー上の他のアラートを確認します。 問題を修正するアラートの指示に従います。  
  
6.  実行**vssadmin**ボリューム シャドウ コピー サービス (VSS) のトラブルシューティングにコマンド プロンプトでを発行します。 について**vssadmin**を参照してください[VSSADMIN](https://go.microsoft.com/fwlink/?LinkID=94332)します。  
  
##  <a name="BKMK_TroubleshootBackupHealthAlertIssues"></a>バックアップの正常性アラートの問題をトラブルシューティングします。  
  
### <a name="errors"></a>エラー  
  
-   Windows Server Solutions Computer Backup Provider Service は動作を停止しました  
  
-   Windows Server Solutions クライアント Computer Backup Provider Service は動作を停止しました  
  
### <a name="resolutions"></a>解決策  
  
##### <a name="to-troubleshoot-a-backup-health-alert"></a>バックアップの正常性アラートのトラブルシューティング  
  
1.  アラートは、データベースのバックアップがある問題を示して場合、は、問題を修正のアラートの指示に従います。  
  
2.  アラートは、バックアップ サービスが実行されていないことを伝える場合、サーバーまたはエラー メッセージを受信したクライアント コンピューターでサービスを開始してみます。  
  
    ###### <a name="to-start-backup-services-on-the-server"></a>サーバーでバックアップ サービスを開始するには  
  
    1.  サーバーで、をクリックして**開始**、] をクリック**管理ツール**、] をクリックし、**サービス**します。  
  
        > [!NOTE]
        >  サーバーをリモートで管理している場合は、サーバーのデスクトップにアクセスするリモート デスクトップ接続を使用する必要があります。 リモート デスクトップ接続の使用については、次を参照してください。[リモート デスクトップ接続を使用して別のコンピューターに接続する](https://windows.microsoft.com/windows-vista/Connect-to-another-computer-using-Remote-Desktop-Connection)します。  
  
    2.  下にスクロールし、クリックして**Windows Server Client Computer Backup Provider Service**します。 サービスの状態がない場合**開始**、サービスを右クリックし、[クリックして**開始**します。  
  
    3.  をクリックして**Windows Server Client Computer Backup Service**します。 サービスの状態がない場合**開始**、サービスを右クリックし、[クリックして**開始**します。  
  
    4.  閉じる**サービス**します。  
  
    ###### <a name="to-start-backup-services-on-a-client-computer"></a>クライアント コンピューターでバックアップ サービスを開始するには  
  
    1.  クライアント コンピューターで、をクリックして**開始**、種類**サービス**で、**プログラムとファイルを検索**クリックして、テキスト ボックスに、次のように入力してください。  
  
    2.  右クリック**Windows Server Client Computer Backup Provider Service**、] をクリックし、**開始**します。  
  
    3.  閉じる、**サービス**します。  
  
3.  クライアント コンピューターまたはサービスまたはドライバーのバックアップに関連する問題のサーバー上のイベント ログを確認します。  
  
4.  サーバーまたはエラー メッセージを受信したクライアント コンピューターを再起動します。  
  
5.  クライアントのバックアップに影響があります。その他の問題の正常性アラートを確認します。  
  
##  <a name="BKMK_FileAndFolder"></a>ファイルまたはフォルダーの復元をトラブルシューティングします。  
  
### <a name="errors"></a>エラー  
  
-   ファイルまたはフォルダーの復元が正常に完了しませんでした。  
  
### <a name="resolutions"></a>解決策  
  
##### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>失敗した場合、ファイルまたはフォルダーの復元のトラブルシューティング  
  
1.  ネットワーク デバイス経由、コンピューターがネットワークに接続されていることを確認します。  
  
2.  正しく機能しているネットワーク デバイスに接続しているコンピューターがネットワーク、電源が入ってにも接続されていることを確認することです。  
  
3.  バックアップ データベースでエラーがあるかどうかを決定するアラートを確認します。 エラーがある場合は、バックアップ データベースを修復するアラートの指示に従います。  
  
4.  別のバックアップからファイルやフォルダーを復元してください。  
  
5.  確認して、**Windows Server Solution Computer Restore Driver**がインストールされているし、正常に動作します。  
  
    ###### <a name="to-check-the-status-of-the-windows-server-solution-computer-restore-driver"></a>Windows Server Solution Computer Restore Driver の状態を確認するには  
  
    1.  をクリックして**開始**、種類**デバイス マネージャー**で、**プログラムとファイルを検索**クリックして、テキスト ボックスに、次のように入力してください。  
  
    2.  デバイス マネージャーで、クリックして**システム デバイス**、までスクロール**Windows Server Solutions Computer Restore Driver**します。  
  
    3.  ドライバーが表示されていない: 場合  
  
        1.  管理者特権でコマンド プロンプトを開き、次のコマンドを実行します。  
  
             **%ProgramFiles%\Windows Server\Bin\BackupDriverInstaller.exe ですか。  私**  
  
        2.  デバイス マネージャーを更新します。 ドライバーが表示されます。  
  
    4.  表示されるアイコンがコンピューター モニターである場合は、ドライバーはインストールし、実行適切です。 デバイス マネージャーを閉じます。  
  
    5.  表示されるアイコンがコンピューター モニターではない場合  
  
        1.  右クリック**Windows Server Solutions Computer Restore Driver**、] をクリックし、**プロパティ**します。  
  
        2.  をクリックして、**ドライバー**タブをクリックし、をクリックして**ドライバーの更新**します。  
  
        3.  をクリックして**更新されたドライバー ソフトウェアを自動的に検索**、ドライバーを更新する指示に従ってします。  
  
    6.  デバイス マネージャーを閉じます。  
  
6.  コンピューターから、Windows Server Essentials コネクタ ソフトウェアをアンインストールし、後で再インストールします。 詳細については、トピックを参照してください。[コネクタ ソフトウェアをアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)と[コネクタ ソフトウェアをインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)します。  
  
##  <a name="BKMK_Troubleshootfullsystemrestoreissues"></a>システムの完全復元をトラブルシューティングします。  
  
### <a name="errors"></a>エラー  
  
-   システムの完全復元した後、クライアント コンピューターにログオンできません。  
  
### <a name="resolutions"></a>解決策  
 このエラーが表示されます、コンピューターの名前を変更すると、後で、コンピューター名を変更、復元後に、ドメイン アカウントでログオンしようとする前に保存されたバックアップを復元する必要があります"サーバーのセキュリティのデータベースがありませんこのワークステーションの信頼関係に対するコンピューター アカウント。"。 コンピューターへのネットワーク アクセスを再度取得するために、コネクタ ソフトウェアを削除する、Windows ドメインからコンピューターを削除およびサーバーにもう一度接続します。  
  
##### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>コンピューター名を変更した後に復元されたコンピューターへのネットワーク アクセスを回復するには  
  
1.  ローカル管理者としてコンピューターにログオンします。  
  
2.  コネクタ ソフトウェアをアンインストールします。 詳細については、次を参照してください。[コネクタ ソフトウェアをアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)します。  
  
3.  コンピューターをドメインから削除します。 詳細については、次を参照してください。[コンピューターを Windows ドメインから削除](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)します。  
  
4.  サーバーにコンピューターをもう一度接続します。 詳細については、次を参照してください。[コンピューター、サーバーに接続](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials をサポートします。](Support-Windows-Server-Essentials.md)