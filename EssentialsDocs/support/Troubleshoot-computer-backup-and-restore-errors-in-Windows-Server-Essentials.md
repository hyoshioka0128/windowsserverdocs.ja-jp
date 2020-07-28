---
title: Windows Server Essentials でのコンピューター バックアップと復元エラーのトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 06/25/2013
ms.topic: article
ms.assetid: 5cc73aff-d2c0-4cf9-a23d-ef928ae5ddc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: de384437a1d135aa60cf8d65a8031faa22983bb0
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180268"
---
# <a name="troubleshoot-computer-backup-and-restore-errors-in-windows-server-essentials"></a>Windows Server Essentials でのコンピューター バックアップと復元エラーのトラブルシューティング

> 適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

以下の手順を使用して、バックアップ構成の問題、不完全または失敗したバックアップ、バックアップの正常性アラート、およびファイル、フォルダー、またはシステムの完全復元の問題などの Windows Server Essentials でのコンピューターのバックアップのトラブルシューティングを行います。

> [!NOTE]
> Windows Server Essentials コミュニティの最新のトラブルシューティング情報については、 [Windows Server Essentials フォーラム](https://docs.microsoft.com/answers/topics/windows-server-essentials.html)を参照してください。

## <a name="troubleshoot-backup-configuration-issues-for-a-connected-computer"></a>接続しているコンピューターのバックアップ構成の問題のトラブルシューティング

以下の手順を使用して、Windows Server Essentials サーバーにバックアップされるコンピューターのバックアップ構成の問題のトラブルシューティングを行います。

### <a name="errors"></a>エラー

- バックアップ構成が正常に完了しませんでした

- コンピューターの情報の収集中にエラーが発生しました

- バックアップからコンピューターの削除中にエラーが発生しました

### <a name="resolutions"></a>解決策

#### <a name="to-troubleshoot-errors-that-occur-while-you-configure-backups-for-a-connected-computer"></a>接続しているコンピューターのバックアップの構成中に発生するエラーのトラブルシューティングを行うには

1. コンピューターが、ネットワーク デバイス経由でネットワークに接続されていることを確認します。

2. コンピューターに接続されているネットワーク デバイスも、ネットワークに接続されており、電源が入っていて、正しく機能していることを確認します。

3. Windows Server Client Backup Service と Windows Server Client Computer Backup Provider Service がサーバーで実行されていることを確認します。

#### <a name="to-start-computer-backup-services-on-the-server"></a>サーバーでコンピューターのバックアップ サービスを開始するには

1. サーバーで、[**スタート**] をクリックし、[**管理ツール**] をクリックして、[**サービス**] をクリックします。

2. 下にスクロールし、[**Windows Server Client Computer Backup Provider Service**] をクリックします。 サービスの状態が [**開始**] でない場合、サービスを右クリックし、[**開始**] をクリックします。

3. [**Windows Server Client Computer Backup Service**] をクリックします。 サービスの状態が [**開始**] でない場合、サービスを右クリックし、[**開始**] をクリックします。

4. [**サービス**] を閉じます。

5. クライアント コンピューターで、Windows Server Client Computer Backup Provider Service が実行していることを確認します。

#### <a name="to-start-the-computer-backup-service-on-the-client-computer"></a>クライアント コンピューターでコンピューターのバックアップ サービスを開始するには

1. クライアント コンピューターで、[**スタート**] をクリックし、[**プログラムとファイルの検索**] ボックスに、「**サービス**」と入力して、Enter キーを押します。

2. 下にスクロールし、[**Windows Server Client Computer Backup Provider Service**] をクリックします。 サービスの状態が [**開始**] でない場合、サービスを右クリックし、[**開始**] をクリックします。

3. [**サービス**] を閉じます。

4. アラートを調べて、バックアップ データベースにエラーがあるかどうかを判断します。 エラーがある場合は、アラートの指示に従って、バックアップ データベースを修復します。

5. コンピューターから Windows Server Essentials コネクタ ソフトウェアをアンインストールし、再インストールします。 詳細については、トピック「[コネクタ ソフトウェアのアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)」と「[コネクタ ソフトウェアのインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)」を参照してください。

## <a name="troubleshoot-a-backup-that-did-not-complete-properly"></a>正常に完了しなかったバックアップのトラブルシューティング

バックアップが失敗状態である場合、成功したバックアップの部分がなく、復元するために使用できるデータがありません。 ただし、バックアップが不完全状態である場合は、バックアップ構成に指定されたすべての項目がバックアップされたわけではありませんが、一部のデータは復元に使用できる可能性があります。

### <a name="errors"></a>エラー

- バックアップが不完全です

- バックアップが失敗しました

### <a name="resolutions"></a>解決策

#### <a name="to-identify-volumes-that-were-not-backed-up-successfully"></a>正常にバックアップされなかったボリュームを識別するには

1. Windows Server Essentials ダッシュボードを開き、[**コンピューターとバックアップ**] をクリックします。

2. バックアップが正常に完了しなかったコンピューターの名前をクリックし、[**タスク**] ウィンドウの [**コンピューターのプロパティの表示**] をクリックします。

3. 正常に完了しなかったバックアップをクリックし、[**詳細の表示**] をクリックします。

4. [**バックアップの詳細**] ダイアログ ボックスで、バックアップが成功したすべてのボリュームの状態に緑のチェックが表示されます。

#### <a name="to-troubleshoot-an-unsuccessful-backup-of-a-volume"></a>失敗したボリュームのバックアップのトラブルシューティングを行うには

1. コンピューターに接続されているハード ディスクがオンになっていて、正しく機能していることを確認します。

2. **chkdsk/f/r** を実行して、ハード ディスク上のエラーを修正し (**/f**)、不良セクターから読み取り可能な情報を回復します (**/r**)。 **chkdsk**の実行の詳細については、「 [CHKDSK](https://go.microsoft.com/fwlink/?LinkId=206562)」を参照してください。

3. バックアップの実行中に、コンピューターがシャットダウンしていないか、またはネットワークから切断されていないことを確認します。

4. 各ボリュームに、バックアップを実行するために十分な空き領域があることを確認します。 バックアップでは VSS スナップショットを作成するために、クライアント コンピューター上にいくらかの追加のディスク領域が必要です。 システムで予約されていないすべてのボリュームで、使用可能なディスク領域の 10% 以上が空いている必要があります。 システム予約ボリュームで、ボリューム サイズが 500 MB 未満である場合、VSS ではスナップショットを作成するために 32 MB の空き領域が必要です。ボリュームが 500 MB 以上の場合は、VSS では 320 MB の空き領域が必要です。

    ボリュームの空き領域が不十分である場合は、以下のいずれかの解決方法を試してみてください。

    - ボリュームを拡張します。 システム予約ボリュームを除いて、任意のベーシックまたはダイナミック ボリュームを拡張できます。

        **ボリュームを拡張するには**

        1. [コントロール パネル] で、[**システムとセキュリティ**] をクリックします。

        2. **[管理ツール]** の **[ハード ディスク パーティションの作成とフォーマット]** をクリックします。

        3. 拡張するボリュームを右クリックします。 [**ボリュームの拡張**] が有効になっている場合、そのオプションを選択します。 オプションが有効でない場合は、ボリュームを拡張できません。

        4. ボリュームの拡張ウィザードの手順に従って、ボリュームを拡張します。

    - ボリュームから内容を削除して、使用できる領域を増やします。

            > [!NOTE]
            > If you need to free up space on the system reserved volume, you can move the System Recovery Image to a different volume. For instructions, see [Deploy a System Recovery Image](/previous-versions/windows/it-pro/windows-7/dd744280(v=ws.10)).

    - クライアント バックアップからボリュームを除外します。 これは、ボリューム上のデータのバックアップ コピーを維持することが重要でない場合にのみ実行してください。

            > [!WARNING]
            > If you exclude the system reserved volume from a client backup, the client system will not be backed up, and you will not be able to perform a full system restore on the computer.

5. サーバーで、バックアップが正常に完了するために十分なディスク領域がサーバーにないことを示す他のアラートを確認します。 アラートの指示に従って、問題を修正します。

6. ボリューム シャドウ コピー サービス (VSS) の問題のトラブルシューティングを行うには、コマンド プロンプトで **vssadmin** を実行します。 **vssadmin**の詳細については、 [VSSADMIN](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754968(v=ws.10))を参照してください。

## <a name="troubleshoot-backup-health-alert-issues"></a>バックアップの正常性アラートの問題のトラブルシューティング

### <a name="errors"></a>エラー

- Windows Server Solutions Computer Backup Provider Service は動作を停止しました

- Windows Server Solutions Client Computer Backup Provider Service は動作を停止しました

### <a name="resolutions"></a>解決策

#### <a name="to-troubleshoot-a-backup-health-alert"></a>バックアップの正常性アラートのトラブルシューティングを行うには

1. アラートでバックアップ データベースに問題があることが示された場合は、アラートの指示に従って、問題を修正します。

2. アラートでバックアップ サービスが実行していないことが示された場合は、エラー メッセージを受け取ったサーバーまたはクライアント コンピューターで、サービスの開始を試みます。

#### <a name="to-start-backup-services-on-the-server"></a>サーバーでバックアップサービスを開始するには * *

1. サーバーで、[**スタート**] をクリックし、[**管理ツール**] をクリックして、[**サービス**] をクリックします。

    > [!NOTE]
    >  サーバーをリモートで管理している場合、リモート デスクトップ接続を使用して、サーバーのデスクトップにアクセスする必要があります。 リモート デスクトップ接続の使用については、「 [リモート デスクトップ接続を使用した別のコンピューターへの接続](https://support.microsoft.com/help/4028379/windows-10-how-to-use-remote-desktop)」を参照してください。

2. 下にスクロールし、[**Windows Server Client Computer Backup Provider Service**] をクリックします。 サービスの状態が [**開始**] でない場合、サービスを右クリックし、[**開始**] をクリックします。

3. [**Windows Server Client Computer Backup Service**] をクリックします。 サービスの状態が [**開始**] でない場合、サービスを右クリックし、[**開始**] をクリックします。

4. [**サービス**] を閉じます。

##### <a name="to-start-backup-services-on-a-client-computer"></a>クライアント コンピューターでバックアップ サービスを開始するには

1. クライアント コンピューターで、[**スタート**] をクリックし、[**プログラムとファイルの検索**] ボックスに、「**サービス**」と入力して、Enter キーを押します。

2. [**Windows Server Client Computer Backup Provider Service**] を右クリックし、[**開始**] をクリックします。

3. [**サービス**] を閉じます。

4. クライアント コンピューターまたはサーバー上のイベント ログで、バックアップ サービスまたはドライバーに関連する問題を確認します。

5. エラー メッセージを受け取ったサーバーまたはクライアント コンピューターを再起動します。

6. 正常性アラートで、クライアント バックアップに影響を及ぼす可能性がある他の問題を確認します。

## <a name="troubleshoot-a-file-or-folder-restore"></a>ファイルまたはフォルダーの復元のトラブルシューティング

### <a name="errors"></a>エラー

- ファイルまたはフォルダーの復元は正しく完了しませんでした。

### <a name="resolutions"></a>解決策

#### <a name="to-troubleshoot-an-unsuccessful-file-or-folder-restore"></a>失敗したファイルまたはフォルダーの復元のトラブルシューティングを行うには

1. コンピューターが、ネットワーク デバイス経由でネットワークに接続されていることを確認します。

2. コンピューターに接続されているネットワーク デバイスも、ネットワークに接続されており、電源が入っていて、正しく機能していることを確認します。

3. アラートを調べて、バックアップ データベースにエラーがあるかどうかを判断します。 エラーがある場合は、アラートの指示に従って、バックアップ データベースを修復します。

4. 別のバックアップからファイルまたはフォルダーを復元してみます。

5. **Windows Server Solution Computer Restore Driver** がインストールされていて、正しく動作していることを確認します。

    **Windows Server Solution Computer Restore Driver の状態を確認するには**

    1. [**スタート**] をクリックし、[**プログラムとファイルの検索**] ボックスに、「**デバイス マネージャー**」と入力して、Enter キーを押します。

    2. デバイス マネージャーで [**システム デバイス**] をクリックし、[**Windows Server Solutions Computer Restore Driver**] までスクロールします。

    3. ドライバーが表示されていない場合:

        1. 管理者特権でコマンド プロンプトを開き、次のコマンドを実行します。

             **%ProgramFiles%\Windows Server\Bin\BackupDriverInstaller.exe ですか?-i**

        2. デバイス マネージャーを更新します。 ドライバーが表示されるはずです。

    4. 表示されたアイコンがコンピューター モニターである場合、ドライバーが正しくインストールされ実行しています。 デバイス マネージャーを閉じます。

    5. 表示されたアイコンがコンピューター モニターでない場合

        1. [**Windows Server Solutions Computer Restore Driver**] を右クリックし、[**プロパティ**] をクリックします。

        2. [**ドライバー**] タブをクリックし、[**ドライバーの更新**] をクリックします。

        3. [**自動的に更新されたドライバー ソフトウェアを検索します**] をクリックし、手順に従って、ドライバーを更新します。

    6. デバイス マネージャーを閉じます。

6. コンピューターから Windows Server Essentials コネクタ ソフトウェアをアンインストールし、再インストールします。 詳細については、トピック「[コネクタ ソフトウェアのアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)」と「[コネクタ ソフトウェアのインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_11)」を参照してください。

## <a name="troubleshoot-a-full-system-restore"></a>システムの完全復元のトラブルシューティング

### <a name="errors"></a>エラー

- システムの完全復元後、クライアント コンピューターにログオンできません。

### <a name="resolutions"></a>解決策

コンピューターの名前を変更し、後でコンピューター名を変更する前に保存されたバックアップを復元する必要がある場合、復元後に、ドメイン アカウントでログオンしようとすると、次のエラーが表示されます。"サーバーのセキュリティ データベースにこのワークステーションの信頼関係に対するコンピューター アカウントがありません。" コンピューターへのネットワーク アクセスを再度取得するには、コネクタ ソフトウェアを削除し、Windows ドメインからコンピューターを削除して、再度サーバーに接続します。

#### <a name="to-regain-network-access-to-a-restored-computer-after-a-computer-name-change"></a>コンピューター名を変更した後に復元されたコンピューターへのネットワーク アクセスを回復するには

1. ローカル管理者としてコンピューターにログオンします。

2. コネクタ ソフトウェアをアンインストールします。 詳細については、「[コネクタ ソフトウェアのアンインストール](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_13)」を参照してください。

3. ドメインからコンピューターを削除します。 詳細については、「[Windows ドメインからコンピューターを削除する](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_8)」を参照してください。

4. コンピューターを再度サーバーに接続します。 詳細については、「[コンピューターをサーバーに接続する方法](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9)」を参照してください。

## <a name="additional-references"></a>その他のリファレンス

- [Windows Server Essentials のサポート](Support-Windows-Server-Essentials.md)