---
title: Robocopy を使用して DFS レプリケーション用にファイルをプリシードする
description: Robocopy を使用して DFS レプリケーション用にファイルをプリシードする方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a0cad3c685c8609784c7096fe31d55294712c2e
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871979"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy を使用して DFS レプリケーション用にファイルをプリシードする

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

このトピックでは、Windows Server で分散ファイルシステム (DFS) レプリケーション (DFSR または DFS-R とも呼ばれます) のレプリケーションを設定するときに、コマンドラインツール**Robocopy**を使用してファイルをプリシードする方法について説明します。 DFS レプリケーションを設定したり、新しいレプリケーションパートナーを追加したり、サーバーを交換したりする前にファイルをプリシードすることにより、初期同期を高速化し、Windows Server 2012 R2 で DFS レプリケーションデータベースの複製を有効にすることができます。 Robocopy メソッドは、いくつかのプリシードメソッドの1つです。概要については、「 [Step 1: プレシード files for DFS レプリケーション](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)」を参照してください。

Robocopy (堅牢なファイルコピー) コマンドラインユーティリティは、Windows Server に付属しています。 このユーティリティには、セキュリティのコピー、バックアップ API のサポート、再試行機能、ログ記録など、さまざまなオプションが用意されています。 それ以降のバージョンには、マルチスレッドおよびバッファーなしの i/o サポートが含まれています。

>[!IMPORTANT]
>Robocopy は、排他的にロックされたファイルをコピーしません。 ファイルサーバー上の長い期間、ユーザーが多くのファイルをロックする傾向がある場合は、別の preseeding 処理方法を使用することを検討してください。 事前シード処理では、移行元サーバーと移行先サーバーのファイルリストの間で完全に一致する必要はありませんが、DFS レプリケーションに対して初期同期を実行したときに存在しないファイルが多いほど、事前シード処理の効率が低下します。 ロックの競合を最小限に抑えるには、組織のピーク時以外の時間帯に Robocopy を使用します。 事前シード処理の後、常に Robocopy ログを調べて、排他ロックが原因でスキップされたファイルを確実に把握できるようにします。

Robocopy を使用して DFS レプリケーション用にファイルをプリシードするには、次の手順を実行します。

1. [最新バージョンの Robocopy をダウンロードしてインストールします。](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [レプリケートされるファイルを安定化します。](#step-2-stabilize-files-that-will-be-replicated)
3. [レプリケートされたファイルを移行先サーバーにコピーします。](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>前提条件

事前シード処理には DFS レプリケーションが直接含まれないため、Robocopy でファイルコピーを実行するための要件を満たす必要があります。

- 移行元サーバーと移行先サーバーの両方で、ローカルの Administrators グループのメンバーであるアカウントが必要です。

- ファイルのコピーに使用するサーバー (移行元サーバーまたは移行先サーバー) に、最新バージョンの Robocopy をインストールします。オペレーティングシステムのバージョンの最新バージョンをインストールする必要があります。 手順について[は、「手順 2:レプリケート](#step-2-stabilize-files-that-will-be-replicated)されるファイルを安定化します。 Windows Server 2003 R2 を実行しているサーバーからファイルをプリシードする場合を除き、移行元または移行先のサーバーで Robocopy を実行できます。 移行先サーバーでは、通常、より新しいバージョンのオペレーティングシステムが使用されているため、最新バージョンの Robocopy にアクセスできます。

- コピー先のドライブに十分な記憶域スペースがあることを確認してください。 コピー先のパスにフォルダーを作成しないでください。Robocopy はルートフォルダーを作成する必要があります。
    
    >[!NOTE]
    >プリシードされたファイルに割り当てられる領域を決定するときは、時間の経過と共に予想されるデータ増加と DFS レプリケーションのストレージ要件を考慮してください。 計画のヘルプについては、「 [DFS レプリケーションの管理](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)」の「[ステージングフォルダーと競合して削除されたフォルダーのクォータサイズを編集](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11))する」を参照してください。

- 移行元サーバーで、必要に応じてプロセスモニターまたはプロセスエクスプローラーをインストールします。これを使用すると、ファイルをロックしているアプリケーションを確認できます。 ダウンロードについては、「[プロセスモニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[プロセスエクスプローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)」を参照してください。

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>手順 1:最新バージョンの Robocopy をダウンロードしてインストールする

Robocopy を使用してファイルをプリシードする前に、最新バージョンの**robocopy**をダウンロードしてインストールする必要があります。 これにより、Robocopy の出荷バージョン内の問題により、DFS レプリケーションがファイルをスキップしないようにします。

最新の互換性のある Robocopy バージョンのソースは、サーバーで実行されている Windows Server のバージョンによって異なります。 Windows Server 2008 R2 または Windows Server 2008 で最新バージョンの Robocopy を使用して修正プログラムをダウンロードする方法については、「 [Windows server 2008 およびでの分散ファイルシステム (DFS) テクノロジで現在利用可能な修正プログラムの一覧」を参照してください。Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)。

または、次の手順を実行して、オペレーティングシステムの最新の修正プログラムを見つけてインストールすることもできます。

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Windows Server の特定のバージョンに対応する Robocopy の最新バージョンを見つけてインストールする

1. Web ブラウザーでを開き[https://support.microsoft.com](https://support.microsoft.com/)ます。

2. **検索サポート**で、次の文字列を入力し`<operating system version>` 、を適切なオペレーティングシステムに置き換えて、enter キーを押します。
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    たとえば、 **「robocopy kbqfe "Windows Server 2008 R2"」** と入力します。

3. 最も大きい ID 番号 (つまり、最新バージョン) を使用して、修正プログラムを見つけてダウンロードします。

4. サーバーに修正プログラムをインストールします。

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>手順 2:レプリケートされるファイルの安定化

最新バージョンの Robocopy をサーバーにインストールした後、次の表に示す方法を使用して、ロックされたファイルがコピーをブロックしないようにする必要があります。 ほとんどのアプリケーションでは、ファイルを排他的にロックしません。 ただし、通常の操作では、ファイルサーバーでファイルのごく一部がロックされている可能性があります。

|ロックのソース|説明|軽減策|
|---|---|---|
|ユーザーは、共有上のファイルをリモートで開きます。|従業員は、標準のファイルサーバーに接続し、ドキュメント、マルチメディアコンテンツ、またはその他のファイルを編集します。 従来のホームフォルダーや共有データワークロードと呼ばれることもあります。|オフピークで営業時間外には、Robocopy 操作のみを実行します。 これにより、Robocopy がプリシード中にスキップする必要があるファイルの数が最小限に抑えられます。<br><br>Windows PowerShell **SmbShareAccess**コマンドレットと**SmbSession**コマンドレットを使用して、レプリケートされるファイル共有に対して読み取り専用アクセスを一時的に設定することを検討してください。 Everyone や認証されたユーザーなどの一般的なグループに対してアクセス許可を設定した場合、標準ユーザーは排他的なロックでファイルを開く可能性が低くなります (ファイルを開いたときにアプリケーションが読み取り専用アクセスを検出した場合)。<br><br>また、ファイルへのアクセスをブロックしたり、 **SmbShareAccess**コマンドレットを使用したりするために、SMB ポート445を受信する一時的なファイアウォール規則をそのサーバーに設定することも検討してください。 ただし、この2つの方法は、ユーザー操作の中断に非常に悪影響を及ぼします。|
|アプリケーションはローカルでファイルを開きます。|ファイルサーバーで実行されているアプリケーションワークロードでは、ファイルがロックされることがあります。|ファイルをロックしているアプリケーションを一時的に無効にするか、アンインストールします。 プロセスモニターまたはプロセスエクスプローラーを使用して、ファイルをロックしているアプリケーションを特定できます。 プロセスモニターまたはプロセスエクスプローラーをダウンロードするには、[プロセスモニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[プロセスエクスプローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)のページにアクセスしてください。|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>手順 3:レプリケートされたファイルを移行先サーバーにコピーする

レプリケートされるファイルのロックを最小限にすると、移行元サーバーから移行先サーバーにファイルを事前にシードすることができます。

>[!NOTE]
>Robocopy は、移行元コンピューターと移行先コンピューターのどちらでも実行できます。 次の手順では、移行先サーバーで Robocopy を実行する方法について説明します。通常は、より新しいオペレーティングシステムを実行しているため、より新しいオペレーティングシステムで提供される追加の Robocopy 機能を利用できます。

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>レプリケートされたファイルを Robocopy を使用して移行先サーバーにプリシードする

1. 移行元サーバーと移行先サーバーの両方で、ローカルの Administrators グループのメンバーであるアカウントを使用して、移行先サーバーにサインインします。

2. 管理者特権でのコマンド プロンプトを開きます。

3. 転送元サーバーから転送先サーバーにファイルを事前にシード処理するには、次のコマンドを実行します。これには、角かっこで囲まれた値のソース、ターゲット、ログファイルの各パスを指定します。
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    このコマンドは、ソースフォルダーのすべての内容をコピー先フォルダーにコピーします。パラメーターは次のとおりです。
    
    |パラメーター|説明|
    |---|---|
    |"\<ソースのレプリケートフォルダー\>のパス"|転送先サーバーで事前シードを行うソースフォルダーを指定します。|
    |"\<レプリケート先のレプリケート\>フォルダーのパス"|プリシードされたファイルを格納するフォルダーへのパスを指定します。<br><br>コピー先のフォルダーは、移行先サーバーに既に存在していてはなりません。 一致するファイルハッシュを取得するには、Robocopy は、ファイルを事前にシードするときにルートフォルダーを作成する必要があります。|
    |/e|サブディレクトリとそのファイル、および空のサブディレクトリをコピーします。|
    |/b|Backup モードでファイルをコピーします。|
    |/copyall|データ、属性、タイムスタンプ、NTFS アクセス制御リスト (ACL)、所有者情報、および監査情報を含む、すべてのファイル情報をコピーします。|
    |/r: 6|エラーが発生したときに、操作を6回再試行します。|
    |/w: 5|再試行を5秒間待機します。|
    |MT:64|64ファイルを同時にコピーします。|
    |/xd DfsrPrivate|DfsrPrivate フォルダーを除外します。|
    |/tee|ログファイルだけでなく、コンソールウィンドウに状態出力を書き込みます。|
    |/log \<ログファイルのパス >|書き込むログファイルを指定します。 ファイルの既存の内容を上書きします。 (既存のログファイルにエントリを追加するには`/log+ <log file path>`、を使用します)。|
    |/v|スキップされたファイルを含む詳細な出力を生成します。|
    
    たとえば、次のコマンドは、ソースのレプリケートされたフォルダー E:\\RF01 からコピー先のサーバー上のデータドライブ D にファイルをレプリケートします。
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy を使用して DFS レプリケーション用にファイルをプリシードする場合は、上記のパラメーターを使用することをお勧めします。 ただし、一部の値を変更したり、パラメーターを追加したりすることはできます。 たとえば、 */mt*パラメーターにより高い値 (スレッド数) を設定できる容量があることをテストすることができます。 また、主に大きなファイルをレプリケートする場合は、バッファーを使用しない i/o に対して **/j**オプションを追加することで、コピーのパフォーマンスを向上させることができます。 Robocopy パラメーターの詳細については、「 [robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy)コマンドラインリファレンス」を参照してください。

    >[!WARNING]
    >Robocopy を使用して DFS レプリケーション用にファイルをプリシードする場合、データ損失の可能性を回避するために、推奨されるパラメーターを次のように変更しないでください。
    >- */Mir*パラメーター (ディレクトリツリーをミラー化) または */mov*パラメーター (ファイルを移動してソースから削除する) は使用しないでください。
    >-  **/E**、 **/b**、および **/copyall**オプションは削除しないでください。

4. コピーが完了したら、エラーまたはスキップされたファイルのログを調べます。 ファイルのセット全体を再コピーするのではなく、Robocopy を使用して、スキップされたファイルを個別にコピーします。 排他ロックのためにファイルがスキップされた場合は、後で Robocopy を使用して個々のファイルをコピーするか、初期同期中に DFS レプリケーションによってネットワーク経由でのレプリケーションが必要であることを受け入れます。

## <a name="next-step"></a>次の手順

最初のコピーを完了し、Robocopy を使用して、スキップされたファイルの数ができるだけ多い問題を解決する場合は、Windows PowerShell または**dfsrdiag.exe**コマンドで**DfsrFileHash**コマンドレットを使用して、移行元サーバーと移行先サーバーのファイルハッシュ。 詳細な手順につい[ては、「手順 2:DFS レプリケーション](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)のプリシードファイルを検証します。
