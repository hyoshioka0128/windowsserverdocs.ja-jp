---
title: robocopy を使用して DFS レプリケーション用にファイルのプレシードを行う
description: Robocopy.exe を使用して DFS レプリケーション用にファイルの事前シード処理を行う方法。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ff800fc2a0885cec39ca104607d7207f0bd8ce0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815605"
---
# <a name="use-robocopy-to-pre-seed-files-for-dfs-replication"></a>robocopy を使用して DFS レプリケーション用にファイルのプレシードを行う

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

このトピックでは、Windows Server で分散ファイル システム (DFS) レプリケーション (別名 DFSR または DFS-R) 用のレプリケーションを設定するときに、コマンドライン ツール (**Robocopy.exe**) を使用してファイルを事前シード処理する方法について説明します。 DFS レプリケーションの設定、新しいレプリケーション パートナーの追加、またはサーバーの交換を実行する前にファイルを事前シード処理することで、初期同期を高速化し、Windows Server 2012 R2 の DFS レプリケーション データベースを複製できます。 Robocopy メソッドは、さまざまな事前シード処理方法の 1 つです。概要については、「[手順 1: DFS レプリケーション用にファイルを事前シード処理する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)」を参照してください。

Robocopy (堅牢なファイル コピー) コマンドライン ユーティリティは、Windows Server に付属しています。 このユーティリティには、コピーのセキュリティ、バックアップ API のサポート、再試行機能、ログ記録などの豊富なオプションが用意されています。 最近のバージョンには、マルチスレッドとバッファーなし I/O のサポートが含まれています。

>[!IMPORTANT]
>Robocopy では、排他ロックされたファイルはコピーされません。 ユーザーがファイル サーバー上に長期にわたって多くのファイルをロックする傾向がある場合は、別の事前シード処理方法を使用することを検討してください。 事前シード処理では、ソース サーバーとターゲット サーバー上のファイル リストが完全に一致している必要はありませんが、DFS レプリケーションのために初期同期が実行されるときに存在しないファイルが多ければ多いほど、事前シード処理の効果は低下します。 ロックの競合を最小限に抑えるために、組織のピーク時以外の時間帯に Robocopy を使用してください。 事前シード処理の後、常に Robocopy ログを調べて、排他ロックが原因でスキップされたファイルを確実に把握してください。

Robocopy を使用して DFS レプリケーション用にファイルの事前シード処理を行うには、次の手順を実行します。

1. [最新バージョンの Robocopy をダウンロードしてインストールします。](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [レプリケートされるファイルを安定化します。](#step-2-stabilize-files-that-will-be-replicated)
3. [レプリケートされたファイルをターゲット サーバーにコピーします。](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>前提条件

事前シード処理には DFS レプリケーションは直接的には関与していないため、Robocopy でファイル コピーを実行するための要件のみを満たす必要があります。

- ソース サーバーとターゲット サーバーの両方でローカルの管理者グループのメンバーであるアカウントが必要です。

- ファイルのコピーに使用するサーバー (ソース サーバーまたはターゲット サーバー) に、最新バージョンの Robocopy をインストールします。オペレーティング システムのバージョンに対応する最新バージョンをインストールする必要があります。 手順については、「[手順 2: レプリケートされるファイルを安定化する](#step-2-stabilize-files-that-will-be-replicated)」を参照してください。 Windows Server 2003 R2 を実行しているサーバーからファイルを事前シード処理する場合を除き、ソースまたはターゲット サーバーのどちらでも Robocopy を実行できます。 通常はより新しいバージョンのオペレーティング システムが使用されているターゲット サーバーで、最新バージョンの Robocopy にアクセスできます。

- ターゲット ドライブに十分な記憶域スペースがあることを確認してください。 コピー先のパスにフォルダーを作成しないでください。ルート フォルダーは、Robocopy で作成する必要があります。
    
    >[!NOTE]
    >事前シード処理されたファイルに割り当てられるスペースを決めるときは、時が経つにつれて増加するデータの推定量と DFS レプリケーションのストレージ要件を考慮してください。 計画のヘルプについては、「[DFS レプリケーションの管理](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)」の「[ステージング フォルダーのクォータ サイズと競合で削除されるフォルダーを編集する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11))」を参照してください。

- ソース サーバーで、必要に応じてプロセス モニターまたはプロセス エクスプローラーをインストールします。これにより、ファイルをロックしているアプリケーションを確認できます。 ダウンロードについては、「[プロセス モニター](https://docs.microsoft.com/sysinternals/downloads/procmon)」と「[プロセス エクスプローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)」を参照してください。

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>手順 1:最新バージョンの Robocopy をダウンロードしてインストールする

Robocopy を使用してファイルを事前シード処理する前に、最新バージョンの **Robocopy.exe** をダウンロードしてインストールする必要があります。 これにより、Robocopy の出荷バージョン内の問題によって DFS レプリケーションでファイルがスキップされることがなくなります。

最新の互換性のある Robocopy バージョンのソースは、サーバーで実行されている Windows Server のバージョンによって異なります。 Windows Server 2008 R2 または Windows Server 2008 用の最新バージョンの Robocopy と修正プログラムのダウンロードの詳細については、「[Windows Server 2008 と Windows Server 2008 R2 での分散ファイル システム (DFS) テクノロジの現在利用可能な修正プログラムの一覧](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)」を参照してください。

または、次の手順を実行することで、オペレーティング システムの最新の修正プログラムを見つけてインストールすることもできます。

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Windows Server の特定のバージョンに対応する最新バージョンの Robocopy を見つけてインストールする

1. Web ブラウザーで、[https://support.microsoft.com](https://support.microsoft.com/) を開きます。

2. **サポートの検索**で、次の文字列を入力し、`<operating system version>` を適切なオペレーティング システムに置き換えてから Enter キーを押します。
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    たとえば、「**robocopy.exe kbqfe "Windows Server 2008 R2"** 」と入力します。

3. ID 番号が最も大きい修正プログラム (これが最新バージョンです) を見つけてダウンロードします。

4. サーバーに修正プログラムをインストールします。

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>手順 2:レプリケートされるファイルを安定化する

最新バージョンの Robocopy をサーバーにインストールした後、次の表に示す方法を使用して、ロックされたファイルによってコピーがブロックされないようにする必要があります。 ほとんどのアプリケーションでは、ファイルが排他ロックされることはありません。 ただし、通常の操作中に、ファイル サーバーでファイルのごく一部がロックされる可能性があります。

|ロックのソース|説明|軽減策|
|---|---|---|
|ユーザーが共有のファイルをリモートで開いている。|従業員が標準のファイル サーバーに接続し、ドキュメント、マルチメディア コンテンツ、またはその他のファイルを編集しています。 従来のホーム フォルダーまたは共有データ ワークロードと呼ばれることもあります。|オフピークの営業時間外にのみ、Robocopy 操作を実行します。 これにより、事前シード処理中に Robocopy でスキップする必要があるファイルの数が最小限に抑えられます。<br><br>Windows PowerShell の **Grant-SmbShareAccess** コマンドレットと **Close-SmbSession** コマンドレットを使用して、レプリケートされるファイル共有に対して読み取り専用アクセスを一時的に設定することを検討します。 Everyone や認証されたユーザーなどの一般的なグループのアクセス許可を読み取りに設定すると、標準ユーザーが排他ロックでファイルを開く可能性は低くなります (ファイルが開くときにアプリケーションで読み取り専用アクセスが検出される場合)。<br><br>そのサーバーへの受信となる SMB ポート 445 に対して、ファイルへのアクセスをブロックするか **Block-SmbShareAccess** コマンドレットを使用する一時的なファイアウォール規則を設定することを検討することもできます。 ただし、これらの方法は、どちらもユーザーの操作に大きな影響を与えます。|
|アプリケーションでファイルがローカルで開かれる。|ファイル サーバーで実行されるアプリケーション ワークロードで、ファイルがロックされることがあります。|ファイルをロックしているアプリケーションを一時的に無効にするか、アンインストールします。 プロセス モニターまたはプロセス エクスプローラーを使用して、ファイルをロックしているアプリケーションを特定できます。 プロセス モニターまたはプロセス エクスプローラーをダウンロードするには、[プロセス モニター](https://docs.microsoft.com/sysinternals/downloads/procmon) ページと[プロセス エクスプローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer) ページにアクセスしてください。|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>手順 3:レプリケートされたファイルをターゲット サーバーにコピーする

レプリケートされるファイルのロックを最小限に抑えた後、ソース サーバーからターゲット サーバーにファイルを事前シード処理できます。

>[!NOTE]
>ソース コンピューターとターゲット コンピューターのどちらでも Robocopy を実行できます。 次の手順では、ターゲット サーバーで Robocopy を実行する方法について説明します。このサーバーでは、通常はより新しいオペレーティング システムが実行されているため、より新しいオペレーティング システムによって提供される追加の Robocopy 機能を利用できます。

### <a name="pre-seed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>レプリケートされたファイルを Robocopy を使用してターゲット サーバーに事前シード処理する

1. ソース サーバーとターゲット サーバーの両方でローカルの管理者グループのメンバーであるアカウントを使用してターゲット サーバーにサインインします。

2. 管理者特権でのコマンド プロンプトを開きます。

3. ソース サーバーからターゲット サーバーにファイルを事前シード処理するには、次のコマンドを実行します。かっこで囲まれたソース、ターゲット、およびログ ファイルの各パスを置き換えます。
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    このコマンドによって、ソース フォルダーのすべての内容が、次のパラメーターを使用して、ターゲット フォルダーにコピーされます。
    
    |パラメーター|説明|
    |---|---|
    |"\<レプリケートのソース フォルダー のパス\>"|ターゲット サーバーで事前シード処理するソース フォルダーを指定します。|
    |"\<レプリケートのターゲット フォルダーのパス\>"|事前シード処理されたファイルを格納するフォルダーへのパスを指定します。<br><br>ターゲット フォルダーは、ターゲット サーバーに既に存在していてはなりません。 Robocopy では、一致するファイル ハッシュを取得するため、ファイルを事前シード処理するときにルート フォルダーを作成する必要があります。|
    |/e|サブディレクトリとそれらのファイルをコピーします。空のサブディレクトリもコピーします。|
    |/b|Backup モードでファイルをコピーします。|
    |/copyall|データ、属性、タイムスタンプ、NTFS アクセス制御リスト (ACL)、所有者情報、および監査情報を含むすべてのファイル情報をコピーします。|
    |/r:6|エラーが発生したときに、操作を 6 回再試行します。|
    |/w:5|再試行と再試行の間、5 秒間待機します。|
    |MT:64|64 個のファイルを同時にコピーします。|
    |/xd DfsrPrivate|DfsrPrivate フォルダーを除外します。|
    |/tee|状態の出力を、コンソール ウィンドウとログ ファイルに書き込みます。|
    |/log \<ログ ファイルのパス>|書き込み先のログ ファイルを指定します。 ファイルの既存の内容を上書きします (既存のログ ファイルにエントリを追加するには、`/log+ <log file path>` を使用します)。|
    |/v|スキップされたファイルを含む詳細出力を生成します。|
    
    たとえば、次のコマンドでは、レプリケートされたソース フォルダー E:\\RF01 からターゲット サーバー上のデータ ドライブ D にファイルがレプリケートされます。
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\pre-seedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy を使用して DFS レプリケーション用にファイルを事前シード処理するときは上記のパラメーターを使用することをお勧めします。 ただし、一部の値を変更したり、パラメーターを追加したりできます。 たとえば、テストによって、 */MT* パラメーターに対してより大きな値 (スレッド カウント) を設定できる容量があることが明らかになる場合があります。 また、主に大きなファイルをレプリケートする場合は、バッファーなし I/O 用の **/j** オプションを追加することで、コピーのパフォーマンスを向上させることが可能である場合があります。 Robocopy パラメーターの詳細については、[Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) のコマンド ライン リファレンスを参照してください。

    >[!WARNING]
    >Robocopy を使用して DFS レプリケーション用にファイルを事前シード処理する際のデータ損失の可能性を回避するために、推奨されるパラメーターに対して次のような変更は行わないでください。
    >- */mir* パラメーター (ディレクトリ ツリーをミラー化する) または */mov* パラメーター (ファイルを移動した後、ソースから削除する) は使用しないでください。
    >-  **/e**、 **/b**、および **/copyall** オプションを削除しないでください。

4. コピーが完了したら、ログを調べて、エラーまたはスキップされたファイルがないか確認します。 ファイルのセット全体を再コピーするのではなく、Robocopy を使用して、スキップされたファイルを個別にコピーします。 排他ロックのためにファイルがスキップされた場合は、後で Robocopy を使用して個々のファイルをコピーするか、これらのファイルでは初期同期中に DFS レプリケーションによるネットワーク経由でのレプリケーションが要求されることを受け入れます。

## <a name="next-step"></a>次のステップ

初回のコピーを完了し、Robocopy を使用してできるだけ多くのスキップされたファイルの問題を解決した後、Windows PowerShell で **Get-DfsrFileHash** コマンドレットを使用するか、**Dfsrdiag** コマンドを使用して、ソース サーバーとターゲット サーバーのファイル ハッシュを比較することで事前シード処理されたファイルを検証します。 手順について詳しくは、「[手順 2: DFS レプリケーション用に事前シード処理されたファイルを検証する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)」を参照してください。
