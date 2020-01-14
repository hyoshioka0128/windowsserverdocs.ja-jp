---
title: Windows Server の SMB 3 プロトコルを使用したファイル共有の概要
description: Windows Server でのファイル共有とファイルサービスのための SMB 3 プロトコルの使用の概要について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 416145a8c4ec20eaf46cf4b5ac88a0cdf38bdf33
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919882"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server の SMB 3 プロトコルを使用したファイル共有の概要

>適用対象: windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012 の SMB 3 機能について説明します。この機能の実際の使用方法、このバージョンの新機能または更新された機能については、以前のバージョンと比較して、ハードウェア要件。 SMB は、記憶域スペースダイレクト、記憶域レプリカなどの[ソフトウェア定義データセンター (SDDC)](../../sddc.md)ソリューションによって使用されるファブリックプロトコルでもあります。 SMB バージョン3.0 は、Windows Server 2012 で導入され、今後のリリースで段階的に改善されています。

## <a name="feature-description"></a>機能の説明

サーバー メッセージ ブロック (SMB) プロトコルはネットワーク ファイル共有プロトコルの一種で、コンピューターのアプリケーションがコンピューター ネットワーク上のサーバー プログラムに対してファイルの読み込みや書き込みを実行したり、サービスを要求したりする際に使用されます。 SMB プロトコルは、TCP/IP プロトコルをはじめとするネットワーク プロトコルの上位で使用できます。 SMB プロトコルを使えば、アプリケーション (またはアプリケーションのユーザー) がリモート サーバーにあるファイルなどのリソースにアクセスできます。 これにより、リモート サーバー上でアプリケーションがファイルを読み込み、作成、および更新できるようになります。 Smb は、SMB クライアント要求を受信するように設定されている任意のサーバープログラムと通信することもできます。 SMB は、記憶域スペースダイレクト、記憶域レプリカなどのソフトウェア定義データセンター (SDDC) コンピューティングテクノロジによって使用されるファブリックプロトコルです。 詳細については、「 [Windows Server ソフトウェアで定義されたデータセンター](../../sddc.md)」を参照してください。

## <a name="practical-applications"></a>実際の適用例

このセクションでは、この新しい SMB 3.0 プロトコルの実際の使用法をいくつか説明します。

* **仮想化用のファイル ストレージ (Hyper-V™ over SMB)** 。 Hyper-V では、SMB 3.0 プロトコルを使って構成ファイル、仮想ハード ディスク (VHD) ファイル、スナップショットなどの仮想マシン ファイルをファイル共有に格納できます。 この機能はスタンドアロン型ファイル サーバーで使用できますが、Hyper-V を使っており、かつクラスターに共有ファイル ストレージを使っていれば、クラスター化されたファイル サーバーでも使用できます。
* **Microsoft SQL Server over SMB**。 SQL Server は、SMB を使用するファイル共有にユーザーのデータベース ファイルを格納できます。 この機能は現在、スタンドアロン型 SQL サーバー向けの SQL Server 2008 R2 でサポートされています。 クラスター化された SQL サーバーとシステム データベースのサポートについては、SQL Server の今後のバージョンで追加する予定です。
* **エンド ユーザー データの従来型ストレージ**。 SMB 3.0 プロトコルは、インフォメーション ワーカー (つまりクライアント) の作業効率を改善します。 たとえば、ブランチ オフィスのユーザーがワイド エリア ネットワーク (WAN) 経由でデータにアクセスする際のアプリケーション待ち時間を短縮したり、データの傍受からの保護したりします。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

以下のセクションでは、SMB 3 とそれ以降の更新で追加された機能について説明します。

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>Windows Server 2019 および Windows 10 バージョン1809で追加された機能

| 機能  | 新規/更新  | 概要  |
| --------- | --------- | --------- |
| 継続的に利用できないファイル共有でディスクへの書き込みを必要とする機能 | 新規 | 書き込み操作が完了として返される前に、ファイル共有への書き込みによって、物理ディスクに対するソフトウェアおよびハードウェアスタックを通じて書き込みを行うことを保証するために、`New-SMBMapping -UseWriteThrough` PowerShell コマンドレットの `NET USE /WRITETHROUGH` コマンドを使用して、ファイル共有での書き込みを有効にすることができます。 ライトスルーを使用すると、パフォーマンスが低下することがあります。詳細については、ブログ記事「 [SMB でのライトスルー動作の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677)」を参照してください。 |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>Windows Server、バージョン1709、Windows 10、バージョン1709で追加された機能

| 機能  | 新規/更新  | 概要  |
| --------- | --------- | --------- |
| ファイル共有へのゲストアクセスが無効になっています | 新規 | SMB クライアントでは、次の操作が許可されなくなりました。 Guest アカウントによるリモートサーバーへのアクセス。無効な資格情報が指定された後に、Guest アカウントにフォールバックします。 詳細については、「 [Windows でのゲストアクセスが既定で無効になっ](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)ている SMB2」を参照してください。 | 
| SMB グローバルマッピング | 新規 | リモート SMB 共有を、ローカルホスト上のすべてのユーザーがアクセスできるドライブ文字 (コンテナーを含む) にマップします。 これは、データボリューム上のコンテナー i/o がリモートマウントポイントを走査できるようにするために必要です。 コンテナーに対して SMB グローバルマッピングを使用する場合、コンテナーホスト上のすべてのユーザーがリモート共有にアクセスできることに注意してください。 コンテナーホストで実行されているすべてのアプリケーションも、マップされたリモート共有にアクセスできます。 詳細については、「[クラスターの共有ボリューム (CSV)、記憶域スペースダイレクト、SMB グローバルマッピングによるコンテナーストレージのサポート」を](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140)参照してください。 |
| SMB 言語制御 | 新規 | レジストリ値を設定して、最小 SMB バージョン (言語) と使用される SMB の最大バージョンを制御できるようになりました。 詳細については、「 [SMB 言語の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)」を参照してください。 |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>SMB 3.11 で追加された機能 (Windows Server 2016 と Windows 10、バージョン 1607)

| 機能  | 新規/更新  | 概要  |
| --------- | --------- | --------- |
| SMB 暗号化     |   更新済み      | Advanced Encryption Standard を使用した SMB 3.1.1 暗号化 (AES-GCM) は、SMB 署名または AES を使用した以前の SMB 暗号化よりも高速です。   |
| ディレクトリキャッシュ | 新規 | SMB 3.1.1 には、ディレクトリキャッシュの機能強化が含まれています。 Windows クライアントは、大量のディレクトリ (約500,000 個エントリ) をキャッシュできるようになりました。 Windows クライアントは、ラウンドトリップを減らしてパフォーマンスを向上させるために、1 MB のバッファーでディレクトリクエリを試行します。 |
| 事前認証の整合性 | 新規 |  SMB 3.1.1 では、事前認証の整合性によって、SMB の接続確立と認証メッセージを改ざんする man-in-the-middle 攻撃からの保護が強化されています。 詳細については、「 [Windows 10 での SMB 3.1.1 事前認証の整合性](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)」を参照してください。 |
| SMB 暗号化の機能強化 | 新規 | SMB 3.1.1 には、接続ごとに暗号アルゴリズムをネゴシエートするメカニズムが用意されています。 AES-128-CCM と AES-128-GCM のオプションがあります。 AES-128-GCM は、新しいバージョンの Windows では既定値ですが、古いバージョンでは引き続き AES-128-CCM を使用します。 |
| ローリングクラスターアップグレードサポート | 新規 | では、アップグレード中のクラスターに対して smb の異なる最大バージョンをサポートするよう SMB を使用して、[クラスターのローリングアップグレード](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)を行うことができます。 プロトコルの異なるバージョン (ダイアレクト) を使用して SMB 通信を行う方法の詳細については、「 [Smb 言語の制御](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)」のブログ記事を参照してください。 |
| Windows 10 での SMB ダイレクトクライアントのサポート | 新規 | Windows 10 Enterprise、Windows 10 の教育、windows 10 Pro のワークステーションには、SMB ダイレクトクライアントのサポートが含まれるようになりました。 |
| FileNormalizedNameInformation API 呼び出しのネイティブサポート | 新規 | ファイルの正規化された名前を照会するためのネイティブサポートを追加します。 詳細については、「 [FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6)」を参照してください。 |

詳細については、 [Windows Server 2016 Technical Preview 2 の SMB 3.1.1 の新機能](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2)に関するブログ記事を参照してください。

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>Windows Server 2012 R2 および Windows 8.1 で SMB 3.02 に追加された機能

| 機能  | 新規/更新  | 概要  |
| --------- | --------- | --------- |
| スケールアウト ファイル サーバー クライアントの自動再分配     |   新規      | では、スケールアウトファイルサーバーのスケーラビリティと管理容易性が向上しています。 SMB クライアント接続は (サーバーごとではなく) ファイル共有ごとに追跡され、クライアントは、ファイル共有で使用されるボリュームへのアクセスに優れたクラスター ノードにリダイレクトされます。 これにより、ファイル サーバー ノード間のリダイレクト トラフィックが減少し、効率性が向上します。 クライアントがリダイレクトされるのは、初期接続の後、クラスター記憶域が再構成された場合です。    |
| WAN 経由のパフォーマンス   | 更新済み  | Windows 8.1 と Windows 10 では、ファイルエクスプローラーを使用して、リモートコンピューター上のある場所から同じサーバー上の別のコピーにリモートコピーを行う場合に、SMB サポートに対する CopyFile SRV_COPYCHUNK が向上しています。 ネットワーク上で少量のメタデータのみをコピーします (ファイルデータが転送される 1/16 Mib につき 1/2KiB)。 その結果、パフォーマンスが大幅に向上します。 これは、SMB の OS レベルとファイルエクスプローラーレベルの区別です。 |
| SMB ダイレクト     |   更新済み      | 小規模な I/O (仮想マシンのオンライン トランザクション処理 (OLTP) データベースなど) でのワークロードをホストするときの効率を高めることによって、小規模な I/O ワークロードのパフォーマンスを向上させます。 これらの改善は、40 Gbps イーサネットや 56 Gbps InfiniBand など、より高速なネットワークインターフェイスを使用する場合に明らかになります。  |
| SMB 帯域幅の制限 | 新規 | [SmbBandwidthLimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit)を使用して、3つのカテゴリの帯域幅制限を設定できるようになりました。 VirtualMachine (HYPER-V over smb traffic)、Livemigration フィルター (hyper-v ライブマイグレーション TRAFFIC over smb)、または既定 (その他のすべての種類の smb トラフィック)。

Windows Server 2012 R2 の SMB の新機能と変更された機能の詳細については、「 [Windows server の smb の新](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)機能」を参照してください。

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>Windows Server 2012 と Windows 8 で SMB 3.0 に追加された機能

| 機能  | 新規/更新  | 概要  |
| --------- | --------- | --------- |
| SMB 透過フェールオーバー     |   新規    | クラスター化されたファイル サーバーにあるノードのハードウェアやソフトウェアの保守作業を行うときに、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要がありません。 また、クラスター ノードでハードウェアまたはソフトウェアの障害が発生した場合に、SMB クライアントが別のクラスター ノードに透過的に再接続できます。このとき、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要はありません。        |
| SMB スケールアウト     |   新規      | スケールアウトファイルサーバーでの複数の SMB インスタンスのサポート。 クラスターの共有ボリューム (CSV) バージョン 2 を使って、ファイル サーバー クラスター内のすべてのノードから同時にデータ ファイルにアクセスして直接入出力できるファイル共有を作成できます。 これにより、ネットワーク帯域幅を効率よく利用しながらファイル サーバー クライアントの負荷分散ができるため、サーバー アプリケーションのパフォーマンスを最適化できます。  |
| SMB マルチチャネル     |   新規      |  SMB クライアントとサーバーの間で複数のパスを使用できる場合は、ネットワーク帯域幅とネットワークフォールトトレランスの集計を有効にします。 これにより、サーバー アプリケーションは利用できるすべてのネットワーク帯域幅をフル活用すると共に、ネットワーク障害に対して高い回復力を維持することができます。<br><br>Smb 3 の SMB マルチチャネルは、smb の以前のバージョンと比較してパフォーマンスの大幅な向上に貢献します。 |
| SMB ダイレクト     |   新規      | RDMA 機能を搭載し、遅延がきわめて小さく、CPU をほとんど使用せずに、最高速度で動作できるネットワーク アダプターが使用できます。 Hyper-V や Microsoft SQL Server などのワークロードについては、この機能によってリモート ファイル サーバーをローカル ストレージのように利用することができます。<br><br>Smb 3 の SMB ダイレクトは、SMB の以前のバージョンと比較してパフォーマンスの大幅な向上に貢献します。  |
| サーバー アプリケーションのパフォーマンス カウンター     |   新規      |  新しい SMB パフォーマンスカウンターは、スループット、待機時間、および1秒あたりの i/o (IOPS) に関する詳細な共有ごとの情報を提供します。管理者は、データが格納されている SMB ファイル共有のパフォーマンスを分析できます。 このカウンターは、Hyper-V や SQL Server など、リモート環境のファイル共有にファイルを格納するサーバー アプリケーション向けに設計されています。      |
| パフォーマンスの最適化    |  更新済み   | SMB クライアントとサーバーはどちらも、小規模なランダム読み取り/書き込み i/o 用に最適化されています。これは、SQL Server OLTP などのサーバーアプリケーションで一般的です。 加えて、大きな最大転送単位 (MTU) が既定で有効にされているため、SQL Server データ ウェアハウス、データベースのバックアップと復元、仮想ハード ディスクの展開とコピーなど、大規模なシーケンシャル転送のパフォーマンスが大幅に向上します。 |
| SMB 用 Windows PowerShell コマンドレット     |   新規      |  SMB 用 Windows PowerShell コマンドレットを使うと、管理者がコマンド ラインからエンド ツー エンドでファイル サーバーのファイル共有を管理できます。   |
| SMB 暗号化     |   新規      | SMB データをエンド ツー エンドで暗号化し、信頼できないネットワークで発生する傍受からデータを保護できます。 新たに展開コストが発生することはなく、インターネット プロトコル セキュリティ (IPsec)、専用ハードウェア、WAN アクセラレーターも不要です。 SMB 暗号化は共有ごとでも、ファイル サーバー全体でも構成できます。また、信頼できないネットワークをデータが通過するさまざまな場面で有効にできます。 |
| SMB ディレクトリ リース     |  新規 | ブランチ オフィスのアプリケーションの応答時間を改善します。 ディレクトリ リースを使うと、保存期間の長いディレクトリ キャッシュからメタデータを取得するため、クライアントからサーバーへのラウンドトリップが減少します。 サーバーにあるディレクトリ情報に変更があるとクライアントに通知されるので、キャッシュの一貫性を維持できます。 ディレクトリリースは、ホームフォルダ (読み取り/書き込み、共有なし) とパブリケーション (読み取り専用、共有あり) のシナリオで使用できます。    |
| WAN 経由のパフォーマンス   | 新規   | SMB 3.0 では、ディレクトリ便宜的ロック (oplock) と oplock リースが導入されました。 一般的なオフィス/クライアントワークロードでは、ネットワークラウンドトリップを約15% 削減するために、oplock/リースが示されています。<br><br>SMB 3 では、クライアントのキャッシュ動作を改善し、より高いスループットをプッシュできるように、SMB の Windows 実装が改良されています。<br><br>SMB 3 では、CopyFile () API が改善され、Robocopy などの関連ツールによってネットワーク経由で大幅にデータがプッシュされるようになりました。 |
| セキュリティで保護された言語ネゴシエーション | 新規 | Man-in-the-middle ネゴシエーションのダウングレードの試行を防止するのに役立ちます。 この考え方は、eavesdropper が、クライアントとサーバーの間で最初にネゴシエートされた言語と機能をダウングレードできないようにすることです。 詳細については、「 [SMB3 Secure Dialect 交渉](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation)」を参照してください。 SMB 3.1.1 の[Windows 10 機能では、smb 3.1.1 事前認証の整合性](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)によって置き換えられていることに注意してください。 |


## <a name="hardware-requirements"></a>ハードウェア要件

SMB 透過フェールオーバーには、次の要件があります。

* 少なくとも2つのノードが構成された Windows Server 2012 または Windows Server 2016 を実行しているフェールオーバークラスター。 このクラスターは、検証ウィザードのクラスター検証テストに合格している必要があります。
* ファイル共有が "継続的可用性 (CA)" プロパティで作成されていること。これは既定の設定です。
* SMB のスケールアウトができるように、CSV のボリューム パスにファイル共有を作成していること。
* クライアントコンピューターは、Windows®8または Windows Server 2012 を実行している必要があります。どちらにも、継続的な可用性をサポートする更新された SMB クライアントが含まれています。

> [!NOTE]
> 下位クライアントは、CA プロパティが設定されているファイル共有に接続できますが、透過的なフェールオーバーはこれらのクライアントではサポートされません。

SMB マルチチャネルの要件は次のとおりです。

* 少なくとも2台のコンピューターが Windows Server 2012 を実行している必要があります。 これ以外の機能のインストールは不要です。このテクノロジは既定でオンになっています。
* 推奨されるネットワーク構成については、この概要トピックの最後にある「関連項目」を参照してください。

SMB ダイレクトの要件は次のとおりです。

* 少なくとも2台のコンピューターが Windows Server 2012 を実行している必要があります。 これ以外の機能のインストールは不要です。このテクノロジは既定でオンになっています。
* RDMA 機能搭載のネットワーク アダプター。 ネットワーク アダプターは現在、iWARP、Infiniband、RoCE (RDMA over Converged Ethernet) の 3 種類が使用できます。

## <a name="more-information"></a>説明を見る

次の一覧は、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB および関連テクノロジに関する web 上のその他のリソースを示しています。

* [Windows Server の記憶域](../storage.md)
* [アプリケーションデータのスケールアウトファイルサーバー](../../failover-clustering/sofs-overview.md)
* [SMB ダイレクトを使用してファイルサーバーのパフォーマンスを向上させる](smb-direct.md)
* [Hyper-v over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB マルチチャネルを展開する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [サーバーアプリケーション用の高速で効率的なファイルサーバーの展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: トラブルシューティングガイド](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
