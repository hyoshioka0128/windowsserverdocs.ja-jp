---
title: NFS ファイルサーバーのパフォーマンスチューニング
description: NFS ファイルサーバーのパフォーマンスチューニング
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: roopeshb, nedpyle
ms.date: 10/16/2017
ms.openlocfilehash: 9bee396532c3319e43d10012e098533495cf0b03
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851855"
---
# <a name="performance-tuning-nfs-file-servers"></a>NFS ファイルサーバーのパフォーマンスチューニング

## <a name="services-for-nfs-model"></a><a href="" id="servicesnfs"></a>NFS 用サービスモデル


次のセクションでは、クライアントとサーバー間の通信用の Microsoft サービス for Network File System (NFS) モデルについて説明します。 NFS v2 と NFS v3 は、最も広く展開されているバージョンのプロトコルであるため、MaxConcurrentConnectionsPerIp を除くすべてのレジストリキーは NFS v2 と NFS v3 にのみ適用されます。

NFS version 4.1 プロトコルには、レジストリの調整は必要ありません。

### <a name="service-for-nfs-model-overview"></a>NFS 用サービスモデルの概要

Microsoft Services for NFS は、Windows および UNIX 環境が混在している企業向けのファイル共有ソリューションを提供します。 この通信モデルは、クライアントコンピューターとサーバーで構成されています。 クライアント上のアプリケーションは、リダイレクター (Rdbss) および NFS ミニリダイレクター () を介してサーバーにあるファイルを要求します。 ミニリダイレクターは、NFS プロトコルを使用して、TCP/IP 経由で要求を送信します。 サーバーは、TCP/IP を介してクライアントから複数の要求を受信し、ローカルファイルシステム (ntfs.sys) に要求をルーティングして、記憶域スタックにアクセスします。

次の図は、NFS の通信モデルを示しています。

![nfs 通信モデル](../../media/perftune-guide-nfs-model.png)

### <a name="tuning-parameters-for-nfs-file-servers"></a>NFS ファイルサーバーのチューニングパラメーター

次の REG\_DWORD レジストリ設定は、NFS ファイルサーバーのパフォーマンスに影響を与える可能性があります。

-   **最適化した読み取り**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\OptimalReads
    ```

    既定値は 0 です。 このパラメーターでは、ファイルを\_ランダム\_アクセス用に開くか、ファイル\_シーケンシャル\_に開くかを指定します。これは、ワークロードの i/o 特性によって異なります。 この値を1に設定すると、ファイル\_ランダム\_アクセスに対してファイルを強制的に開くことができます。 ファイル\_ランダム\_アクセスによって、ファイルシステムとキャッシュマネージャーがプリフェッチされないようにします。

    >[!NOTE]
    > システムファイルキャッシュの増大に影響する可能性があるため、この設定は慎重に評価する必要があります。


-   **RdWrHandleLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrHandleLifeTime
    ```

    既定値は 5 です。 このパラメーターは、ファイルハンドルキャッシュ内の NFS キャッシュエントリの有効期間を制御します。 パラメーターは、関連付けられている NTFS ファイルハンドルを持つキャッシュエントリを参照します。 実際の有効期間は、RdWrHandleLifeTime と RdWrThreadSleepTime を乗算した値とほぼ同じです。 最小値は1、最大値は60です。

-   **Rdwrシャード Andlelifetime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsHandleLifeTime
    ```

    既定値は 5 です。 このパラメーターは、ファイルハンドルキャッシュ内の NFS キャッシュエントリの有効期間を制御します。 パラメーターは、NTFS ファイルハンドルが関連付けられていないキャッシュエントリを参照します。 NFS 用サービスは、ファイルシステムでハンドルを開いたままにして、ファイルのファイル属性を格納するためにこれらのキャッシュエントリを使用します。 実際の有効期間は、RdwrRdWrThreadSleepTime Shandlelifetime とを乗算した値とほぼ同じです。 最小値は1、最大値は60です。

-   **RdWrNfsReadHandlesLifeTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsReadHandlesLifeTime
    ```

    既定値は 5 です。 このパラメーターは、ファイルハンドルキャッシュ内の NFS 読み取りキャッシュエントリの有効期間を制御します。 実際の有効期間は、RdWrNfsReadHandlesLifeTime と RdWrThreadSleepTime を乗算した値とほぼ同じです。 最小値は1、最大値は60です。

-   **RdWrThreadSleepTime**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrThreadSleepTime
    ```

    既定値は 5 です。 このパラメーターは、ファイルハンドルキャッシュでクリーンアップスレッドを実行するまでの待機時間を制御します。 値はティック単位であり、非決定的です。 ティックは約100ナノ秒に相当します。 最小値は1、最大値は60です。

-   **FileHandleCacheSizeinMB**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\FileHandleCacheSizeinMB
    ```

    既定は 4 です。 このパラメーターは、ファイルハンドルキャッシュエントリによって消費される最大メモリを指定します。 最小値は1、最大値は 1\*1024\*1024\*1024 (1073741824) です。

-   **LockFileHandleCacheInMemory**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\LockFileHandleCacheInMemory
    ```

    既定値は 0 です。 このパラメーターは、FileHandleCacheSizeInMB で指定されたキャッシュサイズに割り当てられている物理ページがメモリ内でロックされているかどうかを指定します。 この値を1に設定すると、このアクティビティが有効になります。 ページはメモリ内でロックされ (ディスクにページングされません)、ファイルハンドルの解決のパフォーマンスが向上しますが、アプリケーションで使用可能なメモリが減少します。

-   **MaxIcbNfsReadHandlesCacheSize**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\MaxIcbNfsReadHandlesCacheSize
    ```

    既定値は64です。 このパラメーターは、読み取りデータキャッシュのボリュームごとのハンドルの最大数を指定します。 読み取りキャッシュエントリは、メモリが 1 GB を超えるシステムでのみ作成されます。 最小値は0、最大値は0xFFFFFFFF です。

-   **HandleSigningEnabled**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\HandleSigningEnabled
    ```

    既定値は 1 です。 このパラメーターは、NFS ファイルサーバーによって指定されたハンドルが暗号方式で署名されているかどうかを制御します。 0に設定すると、ハンドルの署名が無効になります。

-   **RdWrNfsDeferredWritesFlushDelay**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\RdWrNfsDeferredWritesFlushDelay
    ```

    既定値は 60 です。 このパラメーターは、NFS V3 の不安定な書き込みデータキャッシュの期間を制御するソフトタイムアウトです。 最小値は1、最大値は600です。 実際の有効期間は、RdWrNfsDeferredWritesFlushDelay と RdWrThreadSleepTime を乗算した値とほぼ同じです。

-   **CacheAddFromCreateAndMkDir**

    ```
    HKLM\System\CurrentControlSet\Services\NfsServer\Parameters\CacheAddFromCreateAndMkDir
    ```

    既定値は 1 (有効) です。 このパラメーターは、NFS V2 および V3 の CREATE および MKDIR RPC プロシージャハンドラーで開かれたハンドルがファイルハンドルキャッシュに保持されるかどうかを制御します。 CREATE および MKDIR コードパスでキャッシュへのエントリの追加を無効にするには、この値を0に設定します。

-   **AdditionalDelayedWorkerThreads**

    ```
    HKLM\SYSTEM\CurrentControlSet\Control\SessionManager\Executive\AdditionalDelayedWorkerThreads
    ```

    指定されたワークキューに対して作成される遅延ワーカースレッドの数を増やします。 遅延ワーカースレッドは、タイムクリティカルではない作業項目を処理し、作業項目を待機している間にメモリスタックをページアウトすることができます。 スレッド数が不足すると、作業項目の処理速度が低下します。値が大きすぎると、システムリソースが不必要に消費されます。

-   **NtfsDisable8dot3NameCreation**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation
    ```

    Windows Server 2012 および Windows Server 2012 R2 の既定値は2です。 Windows Server 2012 より前のリリースでは、既定値は0です。 このパラメーターは、長いファイル名と拡張文字セットの文字を含むファイル名に対して、NTFS が 8dot3 (MSDOS.SYS) の名前付け規則に短い名前を生成するかどうかを決定します。 このエントリの値が0の場合、ファイルは2つの名前を持つことができます。ユーザーが指定する名前と、NTFS によって生成される短い名前です。 ユーザー指定の名前が8dot3 の名前付け規則に従っている場合、NTFS は短い名前を生成しません。 値が2の場合、このパラメーターはボリュームごとに構成できることを意味します。

    >[!NOTE]
    > システムボリュームでは、既定で8dot3 が有効になっています。 Windows Server 2012 および Windows Server 2012 R2 の他のすべてのボリュームでは、既定で8dot3 が無効になっています。 この値を変更しても、ファイルの内容は変更されませんが、ファイルの短縮名属性の作成が回避されます。これにより、NTFS がファイルを表示および管理する方法も変わります。 ほとんどのファイルサーバーでは、推奨される設定は 1 (無効) です。


-   **NtfsDisableLastAccessUpdate**

    ```
    HKLM\System\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate
    ```

    既定値は 1 です。 このシステムグローバルスイッチでは、最後のファイルまたはディレクトリへのアクセスの日付とタイムスタンプの更新を無効にすることで、ディスク i/o の負荷と待機時間を削減できます。

-   **MaxConcurrentConnectionsPerIp**

    ```
    HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Rpcxdr\Parameters\MaxConcurrentConnectionsPerIp
    ```

    MaxConcurrentConnectionsPerIp パラメーターの既定値は16です。 この値は最大8192まで増やすことで、IP アドレスあたりの接続数を増やすことができます。
