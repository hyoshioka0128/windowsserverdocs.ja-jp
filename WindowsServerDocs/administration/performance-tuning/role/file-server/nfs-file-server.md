---
title: NFS のファイル サーバーのパフォーマンス チューニング
description: NFS のファイル サーバーのパフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: RoopeshB, NedPyle
ms.date: 10/16/2017
ms.openlocfilehash: 06a2a7206d3673046bd5a926a657bac91b02bf5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879013"
---
# <a name="performance-tuning-nfs-file-servers"></a>パフォーマンス チューニングの NFS のファイル サーバー

## <a href="" id="servicesnfs"></a>モデルの NFS 用サービス


次のセクションは、Microsoft Services for Network File System (NFS) モデルのクライアント/サーバー通信に関する情報を提供します。 NFS v2 および NFS v3 は、大半のバージョンのプロトコルを広く展開するため、MaxConcurrentConnectionsPerIp を除き、レジストリ キーのすべてが、v2 の NFS および NFS v3 のみに適用されます。

レジストリ チューニング NFS v4.1 プロトコルの必要はありません。

### <a name="service-for-nfs-model-overview"></a>モデルの概要の NFS 用サービス

NFS 用 Microsoft サービスでは、Windows と UNIX の混在環境を所有している企業のファイル共有ソリューションを提供します。 この通信モデルは、クライアント コンピューターとサーバーで構成されます。 クライアント アプリケーションでは、リダイレクター (Rdbss.sys) および NFS ミニ リダイレクター (Nfsrdr.sys) 経由でサーバーに配置されているファイルを要求します。 ミニ リダイレクターは、NFS プロトコルを使用して、TCP/IP 経由で要求を送信します。 サーバーは、TCP/IP 経由のクライアントから複数の要求を受信し、記憶域スタックにアクセスするローカル ファイル システム (Ntfs.sys) に要求をルーティングします。

次の図は、nfs 通信モデルを示します。

![nfs 通信モデル](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>NFS のファイル サーバーのパラメーターのチューニング

次の REG\_DWORD のレジストリ設定の NFS のファイル サーバーのパフォーマンスに影響することができます。

-   **OptimalReads**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    既定値は 0 です。 このパラメーターは、ファイルのファイルを開くかどうかを決定します。\_ランダム\_アクセスまたはファイルの\_シーケンシャル\_I/O ワークロードの特性によってのみ。 1 ファイル用に開かれるファイルを強制的にこの値を設定\_ランダム\_アクセスします。 ファイル\_ランダム\_プリフェッチをファイル システムとキャッシュ マネージャーができません。

    >[!NOTE]
    > この設定は、拡張システム ファイル キャッシュの潜在的な影響する可能性がありますので、慎重に評価する必要があります。


-   **RdWrHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    既定は 5 です。 このパラメーターは、ファイル ハンドル キャッシュでの NFS キャッシュ エントリの有効期間を制御します。 パラメーターは、関連付けられている NTFS ファイルを開く処理を持つキャッシュ エントリを参照します。 実際の有効期間は、RdWrHandleLifeTime とほぼ等しくなりますを掛けた値にします。 最小値は 1、最大値は 60 です。

-   **RdWrNfsHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    既定は 5 です。 このパラメーターは、ファイル ハンドル キャッシュでの NFS キャッシュ エントリの有効期間を制御します。 パラメーターは、関連付けられている NTFS ファイルを開く処理がないキャッシュ エントリを参照します。 NFS 用サービスでは、これらのキャッシュ エントリを使用して、ファイル システムで開いているハンドルを保持することがなく、ファイルのファイル属性を格納します。 実際の有効期間は、RdWrNfsHandleLifeTime とほぼ等しくなりますを掛けた値にします。 最小値は 1、最大値は 60 です。

-   **RdWrNfsReadHandlesLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    既定は 5 です。 このパラメーターは、ファイル ハンドル キャッシュでキャッシュ エントリを読み取り、NFS の有効期間を制御します。 実際の有効期間は、RdWrNfsReadHandlesLifeTime とほぼ等しくなりますを掛けた値にします。 最小値は 1、最大値は 60 です。

-   **RdWrThreadSleepTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    既定は 5 です。 このパラメーターは、ファイル ハンドル キャッシュでクリーンアップ スレッドを実行する前に、待機間隔を制御します。 値はティック単位であり、非決定的です。 1 ティックは約 100 ナノ秒に相当します。 最小値は 1、最大値は 60 です。

-   **FileHandleCacheSizeinMB**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    既定値は 4 です。 このパラメーターは、ファイル ハンドル キャッシュ エントリが消費する最大メモリ量を指定します。 最小値は 1、最大値は 1\*1024\*1024\*1024 (1073741824)。

-   **LockFileHandleCacheInMemory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    既定値は 0 です。 このパラメーターは、FileHandleCacheSizeInMB で指定されたキャッシュ サイズに割り当てられている物理ページがメモリ内にロックされているかどうかを指定します。 この値を 1 に設定すると、このアクティビティが有効になります。 メモリ (ディスクにページングされない)、ファイル ハンドル、解決のパフォーマンスが向上しますが、アプリケーションで使用可能なメモリを削減するには、ページがロックされています。

-   **MaxIcbNfsReadHandlesCacheSize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    既定値は、64 です。 このパラメーターは、読み取りデータ キャッシュのボリュームごとのハンドルの最大数を指定します。 読み取りキャッシュ エントリは、1 GB を超えるメモリを搭載したシステムでのみ作成されます。 最小値は 0、最大値は 0 xffffffff です。

-   **HandleSigningEnabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    既定値は 1 です。 このパラメーターは、NFS のファイル サーバー与えられているハンドルが暗号署名かどうかを制御します。 0 に設定するには、ハンドルの署名が無効にします。

-   **RdWrNfsDeferredWritesFlushDelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    既定値は 60 です。 このパラメーターは、NFS V3 不安定な書き込みデータのキャッシュの期間を制御する論理的なタイムアウトです。 最小値は 1 であり、最大値は 600。 実際の有効期間は、約 RdWrNfsDeferredWritesFlushDelay とほぼ等しくなりますを掛けた値です。

-   **CacheAddFromCreateAndMkDir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    既定では 1 (有効です)。 このパラメーターは、NFS V2 および V3 を作成し、MKDIR RPC プロシージャ ハンドラーは、ファイルに保持される時に開いているハンドルがキャッシュを処理するかどうかを制御します。 この値の作成と MKDIR コード パス内のキャッシュに追加するエントリを無効にするには 0 に設定します。

-   **AdditionalDelayedWorkerThreads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    指定された作業をキューの作成は遅延のワーカー スレッドの数が増えます。 遅延するワーカー スレッド作業項目を処理しては見なされずタイム クリティカルのメモリ スタックを作業項目の待機中にページ アウトすることがあります。 スレッド数が不足して削減率をどの作業アイテムのサービスです。大きすぎる値では、システム リソースが不必要に消費されます。

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Windows Server 2012 および Windows Server 2012 R2 の既定の設定には 2 です。 Windows Server 2012 より前のリリースでは、既定値は 0 です。 このパラメーターは、NTFS が、8dot3 で短い名前を生成するかどうかを決定します。 長いファイル名と、拡張文字セットの文字を含むファイル名 (MSDOS) の名前付け規則。 このエントリの値が 0 の場合も、ファイルには 2 つの名前があります。 ユーザーが指定した名前とは NTFS が生成するための短い名前。 ユーザーが指定した名前は、8dot3 名前付け規則に従って、NTFS は短い名前を生成しません。 ボリュームごとにこのパラメーターを構成する 2 つの手段の値。

    >[!NOTE]
    > システム ボリュームには、既定で有効になっている 8dot3 があります。 Windows Server 2012 および Windows Server 2012 R2 での他のすべてのボリュームがある 8dot3 が既定で無効になっています。 この値を変更しても、ファイルの内容は変更されませんが、NTFS の表示し、管理、ファイルも変更すると、ファイルの短い名前属性の作成を回避できます。 ほとんどのファイル サーバーでは、推奨設定値は 1 (無効です)。


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    既定値は 1 です。 このシステム グローバルのスイッチは、最後のファイルまたはディレクトリのアクセスの日付と時刻のスタンプの更新を無効にしてディスク I/O の負荷と待機時間を減少します。

-   **MaxConcurrentConnectionsPerIp**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    MaxConcurrentConnectionsPerIp パラメーターの既定値は、16 です。 最大数は、8192 IP アドレスごとの接続の数を増やすには、この値を増やすことができます。
