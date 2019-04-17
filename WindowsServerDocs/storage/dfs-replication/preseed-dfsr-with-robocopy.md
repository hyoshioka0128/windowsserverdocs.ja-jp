---
title: Robocopy を使用してファイルを DFS レプリケーションの preseed
description: DFS レプリケーションのファイルを preseed に Robocopy.exe を使用する方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7a14b1a1e0f91002b201869e4c68187ffaf3f8f
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082383"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy を使用してファイルを DFS レプリケーションの preseed

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

このトピックでは、Windows Server で分散ファイル システム (DFS) レプリケーション (DFSR またはまたとも呼ばれます) の複製を設定するときにファイルを preseed に**Robocopy.exe**、コマンド ライン ツールを使用する方法について説明します。 ファイルを preseeding DFS レプリケーションをセットアップする前に、新しいレプリケーション パートナーを追加またはサーバーに置き換える、初回の同期を高速化して、Windows Server 2012 R2 DFS レプリケーション データベースの複製を有効にすることができます。 Robocopy 方法は、複数の preseeding 方法のいずれか概要については、次を参照してください。[手順 1: DFS レプリケーションのファイルを preseed](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)します。

Robocopy (堅牢なファイルのコピー) のコマンド ライン ユーティリティは、Windows Server に含まれています。 ユーティリティには、コピー セキュリティ、バックアップ API サポート、再試行機能、およびログを含む広範なオプションが用意されています。 以降のバージョンには、マルチ スレッド対応していないバッファー I/O サポートが含まれます。

>[!IMPORTANT]
>Robocopy はロックされているファイルのみをコピーできません。 ユーザーが長期間に、ファイル サーバー上の多数のファイルをロックするオプションは場合、は、さまざまな preseeding メソッドを使用してを検討してください。 Preseeding は、元と移行先のサーバー上のファイルの一覧の間の完全一致は必要ありませんが、さらに効果的 preseeding DFS レプリケーションは、最初の同期の実行時に存在しないファイルです。 ロックの競合を最小化するには、組織のピーク時に Robocopy を使用します。 常にファイルを排他モードでロックの理由により、スキップされたかを理解していることを確認する preseeding 後 Robocopy ログを確認します。

Robocopy DFS レプリケーションのファイルを preseed を使用するのには、次の手順を実行します。

1. [ダウンロードして、Robocopy の最新バージョンをインストールします。](#step-1:-download-and-install-the-latest-version-of-robocopy)
2. [複製するファイルを安定します。](#step-2:-stabilize-files-that-will-be-replicated)
3. [貼り付け先のサーバーにレプリケートされたファイルをコピーします。](#step-3:-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>前提条件

Preseeding 直接伴わない DFS レプリケーション、ためだけ Robocopy とファイルのコピーを実行するための要件を満たしている必要があります。

- アカウントの元と移行先の両方のサーバーでローカルの管理者グループのメンバーである必要があります。

- ファイルのコピーを使用しているサーバーで Robocopy の最新バージョンをインストールする: ソース サーバーまたは、宛先のサーバーオペレーティング システムのバージョンの最新バージョンをインストールする必要があります。 手順については、次を参照してください。[手順 2: 複製されるファイルの安定](#step-2:-stabilize-files-that-will-be-replicated)します。 Windows Server 2003 R2 を実行しているサーバーからファイルを preseeding は、しない限り、ソースまたはリンク先のいずれかのサーバーで Robocopy を実行できます。 オペレーティング システムの最新バージョンには、通常、宛先サーバーでは、Robocopy の最新バージョンにアクセスできます。

- ドライブ上に十分なディスク領域があることを確認します。 コピーする予定のパス上のフォルダーを作成できません: Robocopy ルート フォルダーを作成する必要があります。
    
    >[!NOTE]
    >Preseeded ファイル用に割り当てるには、どの程度領域を決定するときは、DFS レプリケーションの時間と記憶域の要件に必要なデータの増加率を検討してください。 ヘルプを計画、[管理 DFS レプリケーション](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)で[ステージング フォルダーと競合してフォルダーの削除済みのクォータ サイズの編集](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11))を参照してください。

- ソース サーバーでは、必要に応じてプロセス モニターまたはプロセスのエクスプ ローラー、アプリケーションがロックされたファイルのチェックを使用するとをインストールします。 ダウンロードについては、[プロセスのモニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[プロセス エクスプ ローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)を参照してください。

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>手順 1: をダウンロードして Robocopy の最新バージョンをインストールします。

ファイルを preseed に Robocopy を使用する前に、ダウンロードして**Robocopy.exe**の最新バージョンをインストールする必要があります。 これは、DFS レプリケーションが Robocopy の出荷バージョン内での問題のファイルを省略しないことを確認します。

互換性のある Robocopy の最新バージョンのソースは、サーバーで実行されている Windows Server のバージョンによって異なります。 最新バージョンの Windows Server 2008 R2 の Robocopy または Windows Server 2008 で修正プログラムをダウンロードする方法の詳細については、[分散ファイル システム (DFS) 技術と Windows Server 2008 で現在利用可能な修正プログラムの一覧を参照してください。Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)します。

または、検索し、オペレーティング システムの最新の修正プログラムをインストールするには、次の手順を実行できます。

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>検索し、特定のバージョンの Windows Server Robocopy の最新バージョンをインストールします。

1. Web ブラウザーで開く[https://support.microsoft.com](https://support.microsoft.com/)します。

2. **サポートの検索**] で、次を入力文字列`<operating system version>`適切なオペレーティング システムで Enter キーを押します。
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    たとえば、 **robocopy.exe カード"Windows Server 2008 R2"** を入力します。

3. 検索し、最高の ID 番号 (つまり、最新バージョン) の修正プログラムをダウンロードします。

4. サーバー上の修正プログラムをインストールします。

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>手順 2: 安定複製されるファイル

サーバー上で Robocopy の最新バージョンをインストールした後、次の表で説明する方法を使用してブロック コピーからロックされているファイルできないようにします。 ほとんどのアプリケーションでファイルを排他モードでロックしません。 ただし、標準の処理中にごく一部のファイルをファイル サーバーでロックすることがあります。

|ロックのソース|説明|軽減策|
|---|---|---|
|ユーザーは、リモートで共有上のファイルを開きます。|従業員が標準のファイル サーバーに接続し、ドキュメント、マルチ メディア コンテンツ、またはその他のファイルを編集します。 従来のホーム フォルダーまたはワークロードのデータの共有と呼ばれることもあります。|Robocopy の操作中にのみ実行ピーク、業務時間外です。 これは、preseeding 中 Robocopy をスキップする必要がありますファイルの数を最小化します。<br><br>Windows PowerShell の**許可を付与する SmbShareAccess**と**閉じる SmbSession**コマンドレットを使用して、複製されるファイルの共有に読み取り専用のアクセスを一時的に設定してください。 読み取りにすべてのユーザーの認証されたユーザーなどの一般的なグループのアクセス許可を設定すると、標準的なユーザーが排他ロック (場合は、アプリケーションは、ファイルを開くと、読み取り専用のアクセスを検出) ファイルを開くことはあまり可能性があります。<br><br>一時的なファイアウォール ルールを設定する必要がありますも一般法ポート 445 はファイルへのアクセスをブロックまたは**ブロック SmbShareAccess**コマンドレットを使用するには、そのサーバーに受信します。 ただし、これらのメソッドの両方が非常に、ユーザーの操作を停止します。|
|アプリケーションでは、ローカル ファイルを開きます。|アプリケーションのワークロードがファイル サーバーで実行されているファイルをロックします。|一時的に無効にするか、ファイルがロックされているアプリケーションをアンインストールします。 アプリケーションのロックされたファイルを決定するのには、プロセス モニターまたはプロセス エクスプ ローラーを使用できます。 プロセス モニターまたはプロセスのエクスプ ローラーをダウンロードするには、[プロセスのモニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[プロセス エクスプ ローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)のページを参照してください。|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>手順 3: 宛先サーバーにレプリケートされたファイルをコピーします。

複製されるファイルのロックを最小化すると後ソース サーバーから、宛先のサーバーにファイルを preseed ことができます。

>[!NOTE]
>元のコンピューターまたは対象のコンピューターでは、Robocopy を実行できます。 次の手順では、通常は最新のオペレーティング システムをする可能性のあるその他の Robocopy 機能を活用するより最近のオペレーティング システムを実行している宛先のサーバーで Robocopy を実行しているについて説明します。

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Preseed Robocopy と移動先のサーバー レプリケートされたファイル

1. 元と移行先の両方のサーバーでローカルの管理者グループのメンバーであるアカウントを使用して、宛先のサーバーにサインインします。

2. 管理者特権でのコマンド プロンプトを開きます。

3. 貼り付け先のサーバーにソースからファイルを preseed するには、独自のソース、宛先、およびログ ファイルのパスで囲まれた値の代わりに、次のコマンドを実行します。
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    このコマンドは、次のパラメーターを使用して、目的のフォルダーに、元のフォルダーのすべての内容をコピーします。
    
    |パラメーター|説明|
    |---|---|
    |「< ソース レプリケート フォルダー path\ > \」|宛先のサーバーで preseed に元のフォルダーを指定します。|
    |"\ < リンク先の複製フォルダー path\ >"|Preseeded ファイルを格納するフォルダーへのパスを指定します。<br><br>コピー先のフォルダーは、先のサーバーに既にに存在しない必要があります。 一致するファイルのハッシュを移動するには、ファイルを preseeds ことと、Robocopy はルート フォルダーを作成する必要があります。|
    |/e|サブディレクトリのファイルと空のサブディレクトリをコピーします。|
    |/b|バックアップ モードでのファイルをコピーします。|
    |copyal/|データ、属性、タイムスタンプ、NTFS アクセス制御リスト (ACL)、所有者情報、情報を監査するなど、すべてのファイル情報をコピーします。|
    |/r:6|エラーが発生したときに 6 回操作を再試行します。|
    |/w:5|5 秒間再試行を待機します。|
    |MT:64|64 ファイルを同時にコピーします。|
    |/xd DfsrPrivate|DfsrPrivate フォルダーを除外します。|
    |/tee|ログ ファイルだけでなく、コンソール ウィンドウには、状態の出力を書き込みます。|
    |ログイン/\ < ログ ファイルのパス >|ログ ファイルの作成を指定します。 既存のファイルの内容を上書きします。 (エントリを追加するには、既存のログ ファイルにするには使用`/log+ <log file path>`.)|
    |/v|作成の詳細な出力を含むファイルをスキップします。|
    
    たとえば、次のコマンド ファイル E:\\RF01、複製ソース フォルダーからに複製先サーバー上のデータ ドライブ D:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >DFS レプリケーションのファイルを preseed に Robocopy を使用する場合は、上記のパラメーターを使用することをお勧めします。 ただし、その値の一部を変更または追加のパラメーターを追加できます。 たとえば、テスト */MT*パラメーターの高い値 (スレッド数) を設定する容量があることを把握することがあります。 また、主より大きなファイルを複製するが場合、バッファー i/o **/j**オプションを追加してコピーのパフォーマンスを向上させることが必要があります。 Robocopy パラメーターの詳細については、 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy)コマンド ライン リファレンスを参照してください。

    >[!WARNING]
    >DFS レプリケーションのファイルを preseed に Robocopy を使用すると、データの損失を避けるため、変更しないでください、次に推奨されるパラメーター。
    >- */Mir*パラメーター (をディレクトリ ツリーを反映) または (つまり、ファイルを移動し、それらをソースから削除) */mov*パラメーターを使わないでください。
    >-  **/E**、 **/b**、および **/copyall**オプションを削除しないでください。

4. コピーが完了した後は、任意のエラーまたはスキップしたファイルのログを調べます。 ファイルのセット全体の過程ではなく、個別にスキップされたファイルをコピーするのにには、Robocopy を使用します。 排他ロックの理由により、ファイルをスキップした場合は、Robocopy と個別ファイル後で、コピーを試すか、ネットワーク上にポインターを複製の初期同期中に DFS レプリケーションでこれらのファイルを要求することに同意します。

## <a name="next-step"></a>次の手順

Preseeded ファイルを比較することで確認するのに Windows PowerShell または**Dfsrdiag**コマンドで**Get DfsrFileHash**コマンドレットを使用する最初のコピーを完了して、このボックスにできるだけ多くのファイルをスキップ問題を解決するのに Robocopy を使用した後は元と移行先のサーバーでファイルのハッシュします。 詳細については、次を参照してください。[手順 2: DFS レプリケーションの Preseeded ファイルの検証](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)します。