---
title: Robocopy を使用して、DFS レプリケーション用にファイルをプレシード
description: DFS レプリケーション用にファイルをプレシードする Robocopy.exe を使用する方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: eaec563157a77fd4e782842a81e5b59e49a5ea09
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621303"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Robocopy を使用して、DFS レプリケーション用にファイルをプレシード

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

このトピックでは、コマンド ライン ツールを使用する方法を説明します。 **Robocopy.exe**、Windows Server の分散ファイル システム (DFS) レプリケーション (DFSR または Dfs-r とも呼ばれます) のレプリケーションを設定するときに、ファイルをプレシードします。 DFS レプリケーションをセットアップする前に、ファイルを事前シード処理、新しいレプリケーション パートナーを追加またはサーバーに置き換える、初期同期を高速化し、Windows Server 2012 R2 の DFS レプリケーション データベースの複製を有効にすることができます。 Robocopy メソッドは、いくつか preseeding メソッドのいずれか概要については、次を参照してください。[手順 1: DFS レプリケーション用にファイルをプレシード](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>)します。

Robocopy (堅牢なファイル コピー) コマンド ライン ユーティリティは、Windows Server に含まれています。 このユーティリティは、コピー セキュリティ、バックアップ API サポート、再試行機能、およびログ記録を含む広範なオプションを提供します。 以降のバージョンには、マルチ スレッド処理とされていないバッファー内の I/O のサポートが含まれます。

>[!IMPORTANT]
>Robocopy では、排他的ロックされたファイルはコピーしません。 ユーザーは、長時間にわたって、ファイル サーバー上の多数のファイルをロックする傾向がある、異なる preseeding メソッドを使用してを検討してください。 事前シード処理は完全に一致するファイルのリスト、ソースと移行先サーバーの間は必要ありませんが、DFS レプリケーション、下がります事前シード処理の初期同期が実行されるときに存在しないファイルは。 ロックの競合を最小限に抑えるには、ピーク時以外に、組織の Robocopy を使用します。 常に排他ロックのためにどのファイルがスキップされたかを理解していることを確認する事前シード処理の後に Robocopy のログを調べる。

Robocopy を使用して、DFS レプリケーション用にファイルをプレシードする、次の手順に従います。

1. [ダウンロードして、Robocopy の最新バージョンをインストールします。](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [レプリケートされるファイルを安定化します。](#step-2-stabilize-files-that-will-be-replicated)
3. [移行先サーバーにレプリケートされたファイルをコピーします。](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>前提条件

事前シード処理も、DFS レプリケーションは直接関係は、ためだけの Robocopy ファイル コピーを実行するための要件を満たす必要があります。

- ソースと宛先の両方のサーバー上でローカルの Administrators グループのメンバーであるアカウントが必要です。

- Robocopy の最新バージョンを使用するファイルをコピーするサーバーにインストール、移行元サーバーまたは対象サーバーのいずれかオペレーティング システムのバージョンの最新バージョンをインストールする必要があります。 手順については、次を参照してください。[手順 2。レプリケートされるファイルを安定化](#step-2-stabilize-files-that-will-be-replicated)します。 Windows Server 2003 R2 を実行しているサーバーからファイルを事前シード処理は、しない限り、ソースまたは移行先サーバーで Robocopy を実行できます。 通常より新しいオペレーティング システムのバージョンを移行先サーバーでは、Robocopy の最新バージョンにアクセスできます。

- インストール先ドライブ上に十分な記憶域があることを確認します。 パスにコピーするには、フォルダーを作成できません。Robocopy には、ルート フォルダーを作成する必要があります。
    
    >[!NOTE]
    >Preseeded ファイル用に割り当てる領域の量を決定する場合は、DFS レプリケーションの時間と記憶域の要件に予想されるデータの増加を検討してください。 ヘルプを計画するには、次を参照してください。[ステージング フォルダーおよび競合して削除済みフォルダーのクォータ サイズを編集する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11))で[DFS レプリケーションを管理する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)します。

- ソース サーバーでは、必要に応じてプロセス モニターまたはファイルをロックしているアプリケーションの確認に使用できるプロセス エクスプ ローラーをインストールします。 ダウンロードについては、次を参照してください。[プロセス モニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer)します。

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>手順 1:ダウンロードして Robocopy の最新バージョンのインストール

ファイルをプレシードを Robocopy を使用する前に、ダウンロードしての最新バージョンをインストールする必要があります**Robocopy.exe**します。 これにより、DFS レプリケーションが Robocopy の出荷バージョン内で問題があるためファイルをスキップしません。

最新の互換性のある Robocopy バージョンのソースは、サーバーで実行されている Windows Server のバージョンによって異なります。 Windows Server 2008 R2 の Robocopy または Windows Server 2008 の最新バージョンで修正プログラムをダウンロードする方法の詳細については、次を参照してください[分散ファイル システム (DFS) テクノロジ Windows Server 2008 で現在使用可能な修正プログラムの一覧。および Windows Server 2008 R2 で](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t)します。

または、検索して、次の手順を実行してオペレーティング システムの最新の修正プログラムをインストールできます。

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>検索して、特定のバージョンの Windows Server 用の Robocopy の最新バージョンのインストール

1. Web ブラウザーで開きます[ https://support.microsoft.com](https://support.microsoft.com/)します。

2. **検索をサポート**、次の入力文字列`<operating system version>`Enter キーを押します, 適切なオペレーティング システム。
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    たとえば、入力**robocopy.exe カードを"Windows Server 2008 R2"** します。

3. 見つけて最高の ID 番号 (これは、最新のバージョン) を持つ修正プログラムをダウンロードします。

4. サーバーに修正プログラムをインストールします。

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>手順 2:安定した状態にレプリケートされるファイル

Robocopy の最新バージョンをサーバーにインストールした後はロックされているファイルを防ぐためから次の表で説明する方法を使用してブロックをコピーする必要があります。 ほとんどのアプリケーションでは、ファイルは排他的ロックしないでください。 ただし、通常の操作中にファイルのごく一部をファイル サーバー上でロックする可能性があります。

|ロックのソース|説明|軽減策|
|---|---|---|
|ユーザーは、リモート共有上のファイルを開きます。|従業員は、標準的なファイル サーバーに接続して、ドキュメント、マルチ メディア コンテンツ、またはその他のファイルを編集します。 従来のホーム フォルダーまたは共有データのワークロードとも呼ばれます。|Robocopy の操作中にのみ実行ピーク時以外に、非営業時間。 これには、Robocopy は、事前シード処理中にスキップする必要があるファイルの数が最小限に抑えます。<br><br>Windows PowerShell を使用してレプリケートされるファイル共有の読み取り専用アクセスを一時的に設定することも**Grant SmbShareAccess**と**閉じる SmbSession**コマンドレット。 読み取り専用に Everyone または Authenticated Users などの一般的なグループのアクセス許可を設定すると、標準ユーザーが排他ロック (この場合、アプリケーションは、ファイルが開かれたときに、読み取り専用アクセスを検出) ファイルを開くことはあまり可能性があります。<br><br>一時的なファイアウォール規則を設定することも検討 SMB ポート 445 の受信をサーバーにファイルへのアクセスをブロックまたはを使用して、**ブロック SmbShareAccess**コマンドレット。 ただし、これらのメソッドの両方がユーザーの操作に非常に悪影響を与えるです。|
|アプリケーションでは、ローカル ファイルを開きます。|場合によって、ファイル サーバーで実行されているアプリケーション ワークロードでは、ファイルをロックします。|一時的に無効にするか、ファイルをロックしているアプリケーションをアンインストールします。 プロセス モニターまたはプロセス エクスプ ローラーを使用すると、ファイルをロックしているアプリケーションを決定します。 Process Monitor またはプロセス エクスプ ローラーをダウンロードするには、次を参照してください。、[プロセス モニター](https://docs.microsoft.com/sysinternals/downloads/procmon)と[Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer)ページ。|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>手順 3:移行先サーバーにレプリケートされたファイルをコピーします。

レプリケートされるファイルのロックを最小限に抑えると後、は、移行先サーバーに移行元サーバーからファイルをプレシードことができます。

>[!NOTE]
>Robocopy は、元のコンピューターまたは対象のコンピューターのいずれかで実行できます。 次の手順では、通常より新しいオペレーティング システムが提供する追加の Robocopy 機能を活用するためより新しいオペレーティング システムを実行している移行先サーバーでの Robocopy の実行について説明します。

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Robocopy で移行先サーバーにレプリケートされたファイルをプレシードします。

1. ソースと宛先の両方のサーバー上でローカルの Administrators グループのメンバーであるアカウントを使用して移行先サーバーにサインインします。

2. 管理者特権でのコマンド プロンプトを開きます。

3. 移行先サーバーに元のファイルをプレシードするには、独自のソース、宛先、およびログ ファイルのパスのかっこで囲まれた値を置き換えて、次のコマンドを実行します。
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    このコマンドは、次のパラメーターを使用して、移行先フォルダーにソース フォルダーのすべての内容をコピーします。
    
    |パラメーター|説明|
    |---|---|
    |"\<ソース フォルダーのパスをレプリケートする\>"|移行先サーバーにプレシードするソース フォルダーを指定します。|
    |"\<先フォルダーのパスをレプリケートする\>"|Preseeded ファイルを保存するフォルダーへのパスを指定します。<br><br>コピー先のフォルダーは、移行先サーバーに既に存在する必要があります。 一致するファイルのハッシュを取得するには、とき、ファイルを preseeds Robocopy がルート フォルダーを作成する必要があります。|
    |/e|サブディレクトリのファイルと空のサブディレクトリにコピーします。|
    |/b|Backup モードでファイルをコピーします。|
    |/copyall|すべてのファイルは、データ、属性、タイムスタンプ、NTFS アクセス制御リスト (ACL)、所有者情報、および監査情報をコピーします。|
    |/r:6|エラーが発生したときに 6 回の操作を再試行します。|
    |/w:5|5 秒間再試行を待機します。|
    |MT:64|64 のファイルを同時にコピーします。|
    |/xd DfsrPrivate|DfsrPrivate フォルダーを除外します。|
    |/tee|ログ ファイルのほか、コンソール ウィンドウには、状態の出力を書き込みます。|
    |/log\<ログ ファイルのパス >|書き込み先のログ ファイルを指定します。 ファイルの既存の内容を上書きします。 (既存のログ ファイルにエントリを追加するには使用`/log+ <log file path>`)。|
    |/v|含まれる詳細出力の生成には、ファイルがスキップされます。|
    
    次のコマンドが e: レプリケートするソース フォルダーからファイルを複製するなど、\\RF01、移行先サーバー上のデータ ドライブ D に。
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Robocopy を使用して、DFS レプリケーション用にファイルをプレシードする場合は、上記のパラメーターを使用することをお勧めします。 ただし、その値の一部を変更または追加のパラメーターを追加できます。 より高い値 (スレッド数) を設定する容量があることをテスト見つける可能性がありますなど、 */MT*パラメーター。 またより大きなファイルを複製し、主に場合、できますを追加して、コピーのパフォーマンスを向上させること、 **/j**バッファなし I/O のオプション。 Robocopy のパラメーターの詳細については、次を参照してください。、 [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy)コマンド ライン リファレンス。

    >[!WARNING]
    >Robocopy を使用して、DFS レプリケーション用にファイルをプレシードする場合は、データ損失の可能性を避けるため、次の変更にしないで推奨パラメーター。
    >- 使用しないでください、 */mir*パラメーター (つまり、ディレクトリ ツリーをミラー化) または */mov*パラメーター (つまり、ファイルを移動し、それらをソースから削除します)。
    >-  削除しないでください、 **/e**、 **/b**、および **/copyall**オプション。

4. コピーが完了したら後、は、エラーまたはスキップされたファイルのログを調べます。 ファイルのセット全体を再コピーではなく、個別にスキップされたファイルをコピーするのにには、Robocopy を使用します。 排他ロックのためファイルをスキップした場合は、個々 のファイルを Robocopy 後で、コピーを試すか、それらのファイルをネットワーク経由のレプリケーション DFS レプリケーションで初期同期中に要求することに同意します。

## <a name="next-step"></a>次の手順

使用する初期のコピーが完了し、Robocopy、できるだけ多くのスキップしたファイルに関する問題の解決を使用して後、 **Get DfsrFileHash**で Windows PowerShell コマンドレットまたは**Dfsrdiag**コマンドソースと移行先サーバー上のファイル ハッシュを比較することによって、preseeded ファイルを検証します。 詳細については、次を参照してください。[手順 2。DFS レプリケーションの Preseeded ファイルを検証する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)します。
