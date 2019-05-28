---
ms.assetid: 60fca6b2-f1c0-451f-858f-2f6ab350d220
title: データ重複除去の相互運用性
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/16/2016
ms.openlocfilehash: 9453811b0f76b249c245990293ba82cf5a6e0867
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624632"
---
# <a name="data-deduplication-interoperability"></a>データ重複除去の相互運用性

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2019

## <a id="supported"></a>サポートされています

### <a id="supported-ReFS"></a>ReFS
データ重複除去は Windows Server 2019 の時点でサポートされています。 

### <a id="supported-clusters"></a>フェールオーバー クラスタ リング

クラスター内のすべてのノードに[データ重複除去機能がインストールされている](install-enable.md#install-dedup)場合、[フェールオーバー クラスタリング](../..//failover-clustering/failover-clustering-overview.md)は完全にサポートされます。 その他の重要な注意事項:

* [手動で開始されたデータ重複除去ジョブ](run.md#running-dedup-jobs-manually)はクラスター共有ボリュームの所有者ノードで実行する必要があります。
* スケジュールされたデータ重複除去ジョブはクラスター タスクに保管されるため、重複除去対象のボリュームを別のノードが引き継いだ場合、スケジュール済みのジョブは次回の予定時間に実施されます。
* データ重複除去は[クラスター OS のローリング アップグレード](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md)機能と完全に相互運用します。
* データ重複除去は[記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)の NTFS フォーマットされたボリューム (ミラーまたはパリティ) で完全にサポートされます。 層が複数あるボリュームでは重複除去はサポートされません。 詳細については、[ReFS でのデータ重複除去](interop.md#unsupported-refs)に関するセクションを参照してください。

### <a id="supported-storage-replica"></a>記憶域レプリカ
[記憶域レプリカ](../storage-replica/storage-replica-overview.md)は完全にサポートされています。 データ重複除外は、セカンダリ コピーに対して実行しないように構成する必要があります。

### <a id="supported-branchcache"></a>BranchCache
サーバーおよびクライアント上で [BranchCache](../../networking/branchcache/branchcache.md) を有効にすると、ネットワーク全体でデータ アクセスを最適化できます。 BranchCache を有効にしたシステムで、データ重複除去を実行するリモートのファイル サーバーと WAN を介して通信を行う場合、重複除去対象のすべてのファイルにはあらかじめインデックスとハッシュが作成されています。 このため、ブランチ オフィスからのデータ要求を素早く処理することができます。 これは、BranchCache 対応サーバーを事前にインデックス化またはハッシュ化することと似ています。

### <a id="supported-dfsr"></a>DFS レプリケーション
データ重複除去は、分散ファイル システム (DFS) レプリケーションと併用できます。 ファイルを最適化または非最適化しても、ファイルは変化しないのでレプリケーションはトリガーされません。 DFS レプリケーションは、ネットワークを節約するため、チャンク ストアのチャンクではなく、Remote Differential Compression (RDC) を使用します。 レプリカがデータ重複除去を使用している場合は、レプリカ上のファイルも重複除去を使用して最適化できます。

### <a id="supported-quotas"></a>クォータ
データ重複除去では、重複除去が有効になっているボリューム ルート フォルダーにハード クォータを作成することはできません。 ボリューム ルートにハード クォータが設定されていると、ボリュームの実際の空き領域とクォータで制限された領域が同じになりません。 その結果、重複除去最適化ジョブが失敗する可能性があります。 ただし、重複除去が有効になっているボリューム ルートにソフト クォータを作成することはできます。 

重複除去対象のボリュームでクォータを有効にした場合、クォータではファイルの物理サイズではなく論理サイズが使用されます。 ファイルが重複除去されていてもクォータの使用率 (クォータのしきい値を含む) は変わりません。 ボリューム ルートのソフト クォータやサブフォルダーのクォータなど、クォータのその他の機能は重複除去が使用されていても通常どおりに機能します。

### <a id="supported-windows-server-backup"></a>Windows Server バックアップ
Windows Server バックアップでは、最適化されたボリュームをそのまま (つまり、重複除去の対象データを削除せずに) バックアップすることができます。 次の手順で、ボリュームのバックアップ方法と、ボリュームまたはボリュームから選択したファイルの復元方法を示します。
1. Windows Server バックアップをインストールします。  
    ```PowerShell
    Install-WindowsFeature -Name Windows-Server-Backup
    ```

2. 次のコマンドを実行して E: ボリュームを別のボリュームにバックアップします。ボリューム名は状況に合った適切なものに置き換えてください。  
    ```PowerShell
    wbadmin start backup –include:E: -backuptarget:F: -quiet
    ```
3. 作成したバックアップのバージョン ID を取得します。

    ```PowerShell
    wbadmin get versions
    ```

    この出力バージョン ID は、日付と時刻の文字列を例になります。08/18/2016-06:22.

4. ボリューム全体を復元します。
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--または--**  

    特定のフォルダー (この場合は、E:\Docs フォルダー) を復元します。
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a id="unsupported"></a>サポートされていません。

### <a id="unsupported-windows-client"></a>Windows 10 (クライアント OS)
Windows 10 では、データ重複除去はサポートされていません。 Windows コミュニティの人気ブログの中には、Windows Server 2016 からバイナリを削除して Windows 10 をインストールする方法を説明した記事がいくつかありますが、これはデータ重複除去の開発の一部として検証されたシナリオではありません。 [この項目のサポートをご希望の場合は、Windows Server Storage UserVoice の Windows 10 vNext で票を投じることができます](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/9011008-add-deduplication-support-to-client-os)

### <a id="unsupported-windows-search"></a>Windows Search
Windows Search では、データ重複除去はサポートされていません。 データ重複除去では再解析ポイントが使用されますが、Windows Search ではこのインデックスを作成できないため、重複除去対象のすべてのファイルをスキップし、インデックスから除外します。 その結果、重複除去されたボリュームでは検索結果が不完全になる場合があります。 [この項目のサポートをご希望の場合は、Windows Server Storage UserVoice の Windows Server vNext で票を投じることができます](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/17888647-make-windows-search-service-work-with-data-dedupli)。

### <a id="unsupported-robocopy"></a>robocopy
特定の Robocopy コマンドによってチャンク ストアが破損することがあるため、データ重複除去での Robocopy の実行はお勧めしません。 チャンク ストアは、ボリュームのシステム ボリューム情報フォルダーに格納されます。 データ チャンクは移行先ボリュームにコピーされないため、フォルダーが削除されると、ソース ボリュームからコピーされた最適化済みファイル (再解析ポイント) が破損します。
