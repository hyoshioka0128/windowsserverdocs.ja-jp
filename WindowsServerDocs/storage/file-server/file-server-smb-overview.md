---
title: Windows Server の SMB 3 プロトコルを使用したファイル共有の概要
description: Windows Server でのファイル共有とファイル サービスに SMB 3 プロトコルを使用する方法の概要について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: aafcfcd4d0f2f14836c5b7dee2bdbccbf99fa887
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "78169622"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server の SMB 3 プロトコルを使用したファイル共有の概要

>適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 の SMB 3 機能 (機能の実際の使用方法、以前のバージョンと比較したこのバージョンの主要な新機能または更新された機能、ハードウェア要件) について説明します。 SMB は、記憶域スペース ダイレクト、記憶域レプリカなどの [ソフトウェア定義データセンター (SDDC)](../../sddc.md) ソリューションで使用されるファブリック プロトコルでもあります。 SMB バージョン 3.0 は Windows Server 2012 で導入され、以降のリリースで段階的に改善されています。

## <a name="feature-description"></a>機能の説明

サーバー メッセージ ブロック (SMB) プロトコルはネットワーク ファイル共有プロトコルの一種で、コンピューターのアプリケーションがコンピューター ネットワーク上のサーバー プログラムに対してファイルの読み込みや書き込みを実行したり、サービスを要求したりする際に使用されます。 SMB プロトコルは、TCP/IP プロトコルをはじめとするネットワーク プロトコルの上位で使用できます。 SMB プロトコルを使えば、アプリケーション (またはアプリケーションのユーザー) がリモート サーバーにあるファイルなどのリソースにアクセスできます。 これにより、リモート サーバー上でアプリケーションがファイルを読み込み、作成、および更新できるようになります。 また、SMB は、SMB クライアント リクエストを受け取ることができるように設定された任意のサーバー プログラムと通信できます。 SMB は、記憶域スペース ダイレクト、記憶域レプリカなどのソフトウェア定義データ センター (SDDC) コンピューティング テクノロジによって使用されるファブリック プロトコルです。 詳細については、「[Windows Server のソフトウェアによるデータセンター](../../sddc.md)」を参照してください。

## <a name="practical-applications"></a>実際の適用例

このセクションでは、この新しい SMB 3.0 プロトコルの実際の使用法をいくつか説明します。

* **仮想化用のファイル ストレージ (Hyper-V™ over SMB)** 。 Hyper-V では、SMB 3.0 プロトコルを使って構成ファイル、仮想ハード ディスク (VHD) ファイル、スナップショットなどの仮想マシン ファイルをファイル共有に格納できます。 この機能はスタンドアロン型ファイル サーバーで使用できますが、Hyper-V を使っており、かつクラスターに共有ファイル ストレージを使っていれば、クラスター化されたファイル サーバーでも使用できます。
* **Microsoft SQL Server over SMB**。 SQL Server は、SMB を使用するファイル共有にユーザーのデータベース ファイルを格納できます。 この機能は現在、スタンドアロン型 SQL サーバー向けの SQL Server 2008 R2 でサポートされています。 クラスター化された SQL サーバーとシステム データベースのサポートについては、SQL Server の今後のバージョンで追加する予定です。
* **エンド ユーザー データの従来型ストレージ**。 SMB 3.0 プロトコルは、インフォメーション ワーカー (つまりクライアント) の作業効率を改善します。 たとえば、ブランチ オフィスのユーザーがワイド エリア ネットワーク (WAN) 経由でデータにアクセスする際のアプリケーション待ち時間を短縮したり、データの傍受からの保護したりします。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

以下のセクションでは、SMB 3 とそれ以降の更新プログラムで追加された機能について説明します。

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>Windows Server 2019 および Windows 10 バージョン 1809 で追加された機能

| 機能  | 新規/更新  | 要約  |
| --------- | --------- | --------- |
| 継続的に使用できないファイル共有上のディスクへの書き込みを必要とする機能 | 新規 | ソフトウェアおよびハードウェア スタックから物理ディスクまでのファイル共有への書き込みが、書き込み操作が完了して戻る前に確実に行われるように、`NET USE /WRITETHROUGH` コマンドまたは `New-SMBMapping -UseWriteThrough` PowerShell コマンドレットを使用してファイル共有でのライトスルーを有効にできます。 ライトスルーを使用すると、パフォーマンスが低下することがあります。詳細については、ブログ記事「[SMB でのライトスルー動作の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677)」を参照してください。 |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>Windows Server バージョン 1709、Windows 10、バージョン 1709 で追加された機能

| 機能  | 新規/更新  | 要約  |
| --------- | --------- | --------- |
| ファイル共有へのゲスト アクセスが無効になりました | 新規 | SMB クライアントでは、次の操作が許可されなくなりました。リモート サーバーに対するゲスト アカウントでのアクセス。無効な資格情報が指定されると、ゲスト アカウントにフォールバックします。 詳細については、「[Windows の既定で無効になっている SMB2 のゲスト アクセス](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)」を参照してください。 | 
| SMB グローバル マッピング | 新規 | リモート SMB 共有を、(コンテナーを含む) ローカル ホスト上のすべてのユーザーがアクセスできるドライブ文字にマップします。 これは、データ ボリューム上のコンテナーの I/O がリモートのマウント ポイントを走査できるようにするために必要です。 コンテナー用に SMB グローバル マッピングを使用している場合、コンテナー ホストのユーザーはすべて、リモート共有にアクセスできることに注意してください。 コンテナー ホストで実行されているすべてのアプリケーションにも、マッピングされたリモート共有へのアクセス権があります。 詳細については、[クラスター共有ボリューム (CSV)、記憶域スペース ダイレクト、SMB グローバル マッピングによるコンテナーストレージのサポートに関するブログの記事](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140)を参照してください。 |
| SMB 言語制御 | 新規 | レジストリ値を設定して、使用される最小 SMB バージョン (言語) と最大 SMB バージョンを制御できるようになりました。 詳細については、「[SMB 言語の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)」を参照してください。 |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>Windows Server 2016 と Windows 10 バージョン 1607 で SMB 3.11 に追加された機能

| 機能  | 新規/更新  | 要約  |
| --------- | --------- | --------- |
| SMB 暗号化     |   更新済み      | Advanced Encryption Standard-Galois/Counter Mode (AES-GCM) による SMB 3.1.1 暗号化は、SMB 署名または AES-CCM を使用した以前の SMB 暗号化よりも高速です。   |
| ディレクトリ キャッシュ | 新規 | SMB 3.1.1 には、ディレクトリ キャッシュの機能強化が含まれています。 Windows クライアントを使って、大量のディレクトリ (約 500,000 エントリ) をキャッシュできるようになりました。 Windows クライアントでは 1 MB のバッファーでディレクトリ クエリが試行されるようになり、ラウンドトリップが減り、パフォーマンスが改善します。 |
| 事前認証の整合性 | 新規 |  SMB 3.1.1 では、事前認証の整合性によって、SMB の接続確立と認証メッセージを改ざんする man-in-the-middle 攻撃からの保護が強化されています。 詳細については、「[Windows 10 での SMB 3.1.1 の事前認証の整合性](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)」を参照してください。 |
| SMB 暗号化の機能強化 | 新規 | SMB 3.1.1 には、接続ごとに暗号アルゴリズムをネゴシエートするメカニズムが用意されており、AES-128-CCM と AES-128-GCM のオプションがあります。 AES-128-GCM は新しいバージョンの Windows では既定値ですが、以前のバージョンでは引き続き AES-128-CCM が使用されます。 |
| クラスターのローリング アップグレードのサポート | 新規 | アップグレードの過程で、SMB がクラスターに対して異なる最大バージョンの SMB をサポートしているように見せることにより、[クラスターのローリング アップグレード](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)を実現します。 SMB が異なるバージョンのプロトコル (言語) を使用して通信できるようにする方法の詳細については、ブログ投稿「[SMB 言語の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)」を参照してください。 |
| Windows 10 での SMB ダイレクト クライアントのサポート | 新規 | Windows 10 Enterprise、Windows 10 Education、Windows 10 Pro for Workstations には、SMB ダイレクト クライアントのサポートが追加されました。 |
| FileNormalizedNameInformation API 呼び出しのネイティブ サポート | 新規 | ファイルの正規化された名前を照会するためのネイティブ サポートを追加します。 詳細については、「[FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6)」を参照してください。 |

詳細については、ブログ投稿「[Windows Server 2016 Technical Preview 2 の SMB 3.1.1 の新機能](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2)」を参照してください。

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>Windows Server 2012 R2 および Windows 8.1 で SMB 3.02 に追加された機能

| 機能  | 新規/更新  | 要約  |
| --------- | --------- | --------- |
| スケールアウト ファイル サーバー クライアントの自動再分配     |   新規      | スケールアウト ファイル サーバーのスケーラビリティと管理容易性が向上しています。 SMB クライアント接続は (サーバーごとではなく) ファイル共有ごとに追跡され、クライアントは、ファイル共有で使用されるボリュームへのアクセスに優れたクラスター ノードにリダイレクトされます。 これにより、ファイル サーバー ノード間のリダイレクト トラフィックが減少し、効率性が向上します。 クライアントがリダイレクトされるのは、初期接続の後、クラスター記憶域が再構成された場合です。    |
| WAN 経由のパフォーマンス   | 更新済み  | Windows 8.1 および Windows 10 では、リモート マシン上のある場所から同じサーバー上の別のコピーへのリモート コピーにエクスプローラーを使用する場合、SMB を介した CopyFile SRV_COPYCHUNK のサポートが向上しています。 ネットワーク経由でコピーするのは少量のメタデータのみです (16 MiB のファイル データあたり 1/2 KiB が送信されます)。 その結果、パフォーマンスが大幅に向上します。 これは、SMB の OS レベルとエクスプローラーレベルの違いです。 |
| SMB ダイレクト     |   更新済み      | 小規模な I/O (仮想マシンのオンライン トランザクション処理 (OLTP) データベースなど) でのワークロードをホストするときの効率を高めることによって、小規模な I/O ワークロードのパフォーマンスを向上させます。 このようなパフォーマンスの向上は、より高速なネットワーク インターフェイス (40 Gbps イーサネットや 56 Gbps InfiniBand など) を使用したときに明確になります。  |
| SMB 帯域幅の制限 | 新規 | [Set-SmbBandwidthLimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit) を使用して、3 つのカテゴリの帯域幅制限を設定できるようになりました。VirtualMachine (SMB 経由の Hyper-V トラフィック)、LiveMigration (SMB 経由の Hyper-V Live Migration トラフィック)、または既定値 (他のすべての種類の SMB トラフィック) です。

Windows Server 2012 R2 での SMB の新機能と変更された機能の詳細については、「[Windows Server での SMB の新機能](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)」を参照してください。

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>Windows Server 2012 と Windows 8 で SMB 3.0 に追加された機能

| 機能  | 新規/更新  | 要約  |
| --------- | --------- | --------- |
| SMB 透過フェールオーバー     |   新規    | クラスター化されたファイル サーバーにあるノードのハードウェアやソフトウェアの保守作業を行うときに、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要がありません。 また、クラスター ノードでハードウェアまたはソフトウェアの障害が発生した場合に、SMB クライアントが別のクラスター ノードに透過的に再接続できます。このとき、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要はありません。        |
| SMB スケールアウト     |   新規      | スケールアウト ファイル サーバーでの複数の SMB インスタンスのサポート。 クラスターの共有ボリューム (CSV) バージョン 2 を使って、ファイル サーバー クラスター内のすべてのノードから同時にデータ ファイルにアクセスして直接入出力できるファイル共有を作成できます。 これにより、ネットワーク帯域幅を効率よく利用しながらファイル サーバー クライアントの負荷分散ができるため、サーバー アプリケーションのパフォーマンスを最適化できます。  |
| SMB マルチチャネル     |   新規      |  SMB クライアントとサーバーの間に複数のパスがある場合に、ネットワーク帯域幅を集約し、ネットワークのフォールト トレランスを高めることができます。 これにより、サーバー アプリケーションは利用できるすべてのネットワーク帯域幅をフル活用すると共に、ネットワーク障害に対して高い回復力を維持することができます。<br><br>SMB 3 の SMB マルチチャネルによって、パフォーマンスは SMB の以前のバージョンよりも大幅に向上します。 |
| SMB ダイレクト     |   新規      | RDMA 機能を搭載し、遅延がきわめて小さく、CPU をほとんど使用せずに、最高速度で動作できるネットワーク アダプターが使用できます。 Hyper-V や Microsoft SQL Server などのワークロードについては、この機能によってリモート ファイル サーバーをローカル ストレージのように利用することができます。<br><br>SMB 3 の SMB ダイレクトによって、パフォーマンスは SMB の以前のバージョンよりも大幅に向上します。  |
| サーバー アプリケーションのパフォーマンス カウンター     |   新規      |  SMB の新しいパフォーマンス カウンターでは、スループット、待ち時間、1 秒あたりの I/O (IOPS) に関する情報を共有ごとに詳細に得ることができます。これで、管理者はデータが格納されている SMB ファイル共有のパフォーマンスを解析できます。 このカウンターは、Hyper-V や SQL Server など、リモート環境のファイル共有にファイルを格納するサーバー アプリケーション向けに設計されています。      |
| パフォーマンスの最適化    |  更新済み   | SQL Server の OLTP など、サーバー アプリケーションで生じる I/O は、小規模なランダム読み取り/書き込みが一般的です。それに合わせて、SMB クライアントとサーバーが最適化されました。 加えて、大きな最大転送単位 (MTU) が既定で有効にされているため、SQL Server データ ウェアハウス、データベースのバックアップと復元、仮想ハード ディスクの展開とコピーなど、大規模なシーケンシャル転送のパフォーマンスが大幅に向上します。 |
| SMB 用 Windows PowerShell コマンドレット     |   新規      |  SMB 用 Windows PowerShell コマンドレットを使うと、管理者がコマンド ラインからエンド ツー エンドでファイル サーバーのファイル共有を管理できます。   |
| SMB 暗号化     |   新規      | SMB データをエンド ツー エンドで暗号化し、信頼できないネットワークで発生する傍受からデータを保護できます。 新たに展開コストが発生することはなく、インターネット プロトコル セキュリティ (IPsec)、専用ハードウェア、WAN アクセラレーターも不要です。 SMB 暗号化は共有ごとでも、ファイル サーバー全体でも構成できます。また、信頼できないネットワークをデータが通過するさまざまな場面で有効にできます。 |
| SMB ディレクトリ リース     |  新規 | ブランチ オフィスのアプリケーションの応答時間を改善します。 ディレクトリ リースを使うと、保存期間の長いディレクトリ キャッシュからメタデータを取得するため、クライアントからサーバーへのラウンドトリップが減少します。 サーバーにあるディレクトリ情報に変更があるとクライアントに通知されるので、キャッシュの一貫性を維持できます。 ディレクトリ リースは、HomeFolder (読み込み/書き込み可、共有なし) と Publication (読み取り専用、共有あり) のどちらのシナリオにも対応しています。    |
| WAN 経由のパフォーマンス   | 新規   | SMB 3.0 では、ディレクトリの便宜的ロック (oplock) と oplock リースが導入されました。 一般的なオフィスおよびクライアントのワークロードでは、oplocks およびリースによってネットワーク ラウンドトリップが約 15% 削減されることが示されています。<br><br>SMB 3 では、SMB の Windows 実装が改良され、クライアントでのキャッシュ動作が改善され、スループットが向上しました。<br><br>SMB 3 では、CopyFile() API に加えて、Robocopy などの関連ツールが改善され、ネットワーク経由でプッシュできるデータの量が大幅に増えました。 |
| セキュリティで保護された言語ネゴシエーション | 新規 | 言語のネゴシエーションのダウングレードを試みる man-in-the-middle を防止するために利用できます。 その目的は、クライアントとサーバーの間で最初にネゴシエートされた言語と機能を盗聴者がダウングレードできないようにすることです。 詳細については、「[SMB3 のセキュリティで保護された言語ネゴシエーション](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation)」を参照してください。 これは、SMB 3.1.1 の「[Windows 10 での SMB 3.1.1 の事前認証の整合性](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)」で置き換えられていることに注意してください。 |


## <a name="hardware-requirements"></a>ハードウェア要件

SMB 透過フェールオーバーには、次の要件があります。

* 少なくとも 2 つのノードが構成された、Windows Server 2012 または Windows Server 2016 を実行しているフェールオーバー クラスター。 このクラスターは、検証ウィザードのクラスター検証テストに合格している必要があります。
* ファイル共有が "継続的可用性 (CA)" プロパティで作成されていること。これは既定の設定です。
* SMB のスケールアウトができるように、CSV のボリューム パスにファイル共有を作成していること。
* クライアント コンピューターは、Windows® 8 または Windows Server 2012 を実行している必要があります。このどちらにも、継続的な可用性をサポートする更新された SMB クライアントが含まれています。

> [!NOTE]
> ダウンレベルのクライアントは、CA プロパティが設定されているファイル共有に接続することができます。ただし、このようなクライアントについては、透過フェールオーバーはサポートされません。

SMB マルチチャネルの要件は次のとおりです。

* 少なくとも 2 台のコンピューターが Windows Server 2012 を実行している必要があります。 これ以外の機能のインストールは不要です。このテクノロジは既定でオンになっています。
* 推奨されるネットワーク構成については、この概要トピックの最後にある「関連項目」を参照してください。

SMB ダイレクトの要件は次のとおりです。

* 少なくとも 2 台のコンピューターが Windows Server 2012 を実行している必要があります。 これ以外の機能のインストールは不要です。このテクノロジは既定でオンになっています。
* RDMA 機能搭載のネットワーク アダプター。 ネットワーク アダプターは現在、iWARP、Infiniband、RoCE (RDMA over Converged Ethernet) の 3 種類が使用できます。

## <a name="more-information"></a>説明を見る

Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB および関連テクノロジに関する Web 上のその他のリソースを次の一覧に示します。

* [Windows Server の記憶域](../storage.md)
* [アプリケーション データ用のスケールアウト ファイル サーバー](../../failover-clustering/sofs-overview.md)
* [SMB ダイレクトを使用してファイル サーバーのパフォーマンスを向上させる](smb-direct.md)
* [Hyper-V over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB マルチチャネルの展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [サーバー アプリケーション用に高速で効率性に優れたファイル サーバーを展開する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB:トラブルシューティング ガイド](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
