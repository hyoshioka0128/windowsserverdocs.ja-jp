---
title: Windows Server の SMB 3 プロトコルを使用したファイル共有の概要
description: Windows Server でのファイル共有とファイルサービスのための SMB 3 プロトコルの使用の概要について説明します。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: b40c179d242a0c48c6eb176db1225979f9e6a123
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402091"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server の SMB 3 プロトコルを使用したファイル共有の概要

>適用対象: Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

このトピックでは、Windows Server®2012、Windows Server 2012 R2、および Windows Server 2016 の SMB 3.0 機能について説明します。この機能の実際の使用方法、このバージョンの新機能または更新された機能については、以前のバージョンと比較してください。必要性.

## <a name="feature-description"></a>機能の説明

サーバー メッセージ ブロック (SMB) プロトコルはネットワーク ファイル共有プロトコルの一種で、コンピューターのアプリケーションがコンピューター ネットワーク上のサーバー プログラムに対してファイルの読み込みや書き込みを実行したり、サービスを要求したりする際に使用されます。 SMB プロトコルは、TCP/IP プロトコルをはじめとするネットワーク プロトコルの上位で使用できます。 SMB プロトコルを使えば、アプリケーション (またはアプリケーションのユーザー) がリモート サーバーにあるファイルなどのリソースにアクセスできます。 これにより、リモート サーバー上でアプリケーションがファイルを読み込み、作成、および更新できるようになります。 また、SMB クライアント リクエストを受け取ることができるように設定された任意のサーバー プログラムと通信できます。 Windows Server 2012 では、SMB プロトコルの新しい3.0 バージョンが導入されています。

## <a name="practical-applications"></a>実際の適用例

このセクションでは、この新しい SMB 3.0 プロトコルの実際の使用法をいくつか説明します。

* **仮想化用のファイル ストレージ (Hyper-V™ over SMB)** 。 Hyper-V では、SMB 3.0 プロトコルを使って構成ファイル、仮想ハード ディスク (VHD) ファイル、スナップショットなどの仮想マシン ファイルをファイル共有に格納できます。 この機能はスタンドアロン型ファイル サーバーで使用できますが、Hyper-V を使っており、かつクラスターに共有ファイル ストレージを使っていれば、クラスター化されたファイル サーバーでも使用できます。
* **Microsoft SQL Server over SMB**。 SQL Server は、SMB を使用するファイル共有にユーザーのデータベース ファイルを格納できます。 この機能は現在、スタンドアロン型 SQL サーバー向けの SQL Server 2008 R2 でサポートされています。 クラスター化された SQL サーバーとシステム データベースのサポートについては、SQL Server の今後のバージョンで追加する予定です。
* **エンド ユーザー データの従来型ストレージ**。 SMB 3.0 プロトコルは、インフォメーション ワーカー (つまりクライアント) の作業効率を改善します。 たとえば、ブランチ オフィスのユーザーがワイド エリア ネットワーク (WAN) 経由でデータにアクセスする際のアプリケーション待ち時間を短縮したり、データの傍受からの保護したりします。

## <a name="new-and-changed-functionality"></a>新機能と変更された機能

Windows Server 2012 R2 の新機能および変更された機能の詳細については、「 [Windows server の SMB の新](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)機能」を参照してください。

Windows Server 2012 および Windows Server 2016 の SMB には、新しい SMB 3.0 プロトコルと、次の表で説明されている多くの新しい機能強化が含まれています。

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>機能</p></th>
<th><p>新規/更新</p></th>
<th><p>概要</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SMB 透過フェールオーバー</p></td>
<td><p>新規</p></td>
<td><p>クラスター化されたファイル サーバーにあるノードのハードウェアやソフトウェアの保守作業を行うときに、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要がありません。 また、クラスター ノードでハードウェアまたはソフトウェアの障害が発生した場合に、SMB クライアントが別のクラスター ノードに透過的に再接続できます。このとき、そのファイル共有にデータを格納しているサーバー アプリケーションを中断する必要はありません。</p></td>
</tr>
<tr class="even">
<td><p>SMB スケールアウト</p></td>
<td><p>新規</p></td>
<td><p>クラスターの共有ボリューム (CSV) バージョン 2 を使って、ファイル サーバー クラスター内のすべてのノードから同時にデータ ファイルにアクセスして直接入出力できるファイル共有を作成できます。 これにより、ネットワーク帯域幅を効率よく利用しながらファイル サーバー クライアントの負荷分散ができるため、サーバー アプリケーションのパフォーマンスを最適化できます。</p></td>
</tr>
<tr class="odd">
<td><p>SMB マルチチャネル</p></td>
<td><p>新規</p></td>
<td><p>SMB 3.0 クライアントと SMB 3.0 サーバーの間に複数のパスがある場合に、ネットワーク帯域幅を集約し、ネットワークのフォールト トレランスを高めることができます。 これにより、サーバー アプリケーションは利用できるすべてのネットワーク帯域幅をフル活用すると共に、ネットワーク障害に対して高い回復力を維持することができます。</p></td>
</tr>
<tr class="even">
<td><p>SMB ダイレクト</p></td>
<td><p>新規</p></td>
<td><p>RDMA 機能を搭載し、遅延がきわめて小さく、CPU をほとんど使用せずに、最高速度で動作できるネットワーク アダプターが使用できます。 Hyper-V や Microsoft SQL Server などのワークロードについては、この機能によってリモート ファイル サーバーをローカル ストレージのように利用することができます。</p></td>
</tr>
<tr class="odd">
<td><p>サーバー アプリケーションのパフォーマンス カウンター</p></td>
<td><p>新規</p></td>
<td><p>SMB の新しいパフォーマンス カウンターでは、スループット、待ち時間、1 秒あたりの I/O (IOPS) に関する情報を共有ごとに詳細に得ることができ、データが格納されている SMB 3.0 ファイル共有のパフォーマンスを解析できます。 このカウンターは、Hyper-V や SQL Server など、リモート環境のファイル共有にファイルを格納するサーバー アプリケーション向けに設計されています。</p></td>
</tr>
<tr class="even">
<td><p>パフォーマンスの最適化</p></td>
<td><p>更新</p></td>
<td><p>SQL Server の OLTP など、サーバー アプリケーションで生じる I/O は、小規模なランダム読み取り/書き込みが一般的です。それに合わせて、SMB 3.0 クライアントおよび SMB 3.0 サーバーが最適化されました。 加えて、大きな最大転送単位 (MTU) が既定で有効にされているため、SQL Server データ ウェアハウス、データベースのバックアップと復元、仮想ハード ディスクの展開とコピーなど、大規模なシーケンシャル転送のパフォーマンスが大幅に向上します。</p></td>
</tr>
<tr class="odd">
<td><p>SMB 用 Windows PowerShell コマンドレット</p></td>
<td><p>新規</p></td>
<td><p>SMB 用 Windows PowerShell コマンドレットを使うと、管理者がコマンド ラインからエンド ツー エンドでファイル サーバーのファイル共有を管理できます。</p></td>
</tr>
<tr class="even">
<td><p>SMB 暗号化</p></td>
<td><p>新規</p></td>
<td><p>SMB データをエンド ツー エンドで暗号化し、信頼できないネットワークで発生する傍受からデータを保護できます。 新たに展開コストが発生することはなく、インターネット プロトコル セキュリティ (IPsec)、専用ハードウェア、WAN アクセラレーターも不要です。 SMB 暗号化は共有ごとでも、ファイル サーバー全体でも構成できます。また、信頼できないネットワークをデータが通過するさまざまな場面で有効にできます。</p></td>
</tr>
<tr class="odd">
<td><p>SMB ディレクトリ リース</p></td>
<td><p>新規</p></td>
<td><p>ブランチ オフィスのアプリケーションの応答時間を改善します。 ディレクトリ リースを使うと、保存期間の長いディレクトリ キャッシュからメタデータを取得するため、クライアントからサーバーへのラウンドトリップが減少します。 サーバーにあるディレクトリ情報に変更があるとクライアントに通知されるので、キャッシュの一貫性を維持できます。 <em>ホーム フォルダー</em> (読み込み/書き込み可、共有なし) と<em>パブリケーション</em> (読み取り専用、共有あり) のどちらにも対応しています。</p></td>
</tr>
</tbody>
</table>

## <a name="hardware-requirements"></a>ハードウェア要件

SMB 透過フェールオーバーには、次の要件があります。

* 少なくとも2つのノードが構成された Windows Server 2012 または Windows Server 2016 を実行しているフェールオーバークラスター。 このクラスターは、検証ウィザードのクラスター検証テストに合格している必要があります。
* ファイル共有が "継続的可用性 (CA)" プロパティで作成されていること。これは既定の設定です。
* SMB のスケールアウトができるように、CSV のボリューム パスにファイル共有を作成していること。
* クライアントコンピューターは、Windows®8または Windows Server 2012 を実行している必要があります。どちらにも、継続的な可用性をサポートする更新された SMB クライアントが含まれています。

>[!NOTE]
>下位クライアントは、CA プロパティが設定されているファイル共有に接続できますが、透過的なフェールオーバーはこれらのクライアントではサポートされません。

SMB マルチチャネルの要件は次のとおりです。

* 少なくとも2台のコンピューターが Windows Server 2012 を実行している必要があります。 追加の機能をインストールする必要はありません。テクノロジは既定でオンになっています。
* 推奨されるネットワーク構成については、この概要トピックの最後にある「関連項目」を参照してください。

SMB ダイレクトの要件は次のとおりです。

* 少なくとも2台のコンピューターが Windows Server 2012 を実行している必要があります。 追加の機能をインストールする必要はありません。テクノロジは既定でオンになっています。
* RDMA 機能搭載のネットワーク アダプター。 ネットワーク アダプターは現在、iWARP、Infiniband、RoCE (RDMA over Converged Ethernet) の 3 種類が使用できます。

## <a name="more-information"></a>詳細情報

次の一覧は、Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 の SMB および関連テクノロジに関する web 上のその他のリソースを示しています。

* [Windows Server の記憶域](../storage.md)
* [アプリケーションデータのスケールアウトファイルサーバー](../../failover-clustering/sofs-overview.md)
* [SMB ダイレクトを使用してファイルサーバーのパフォーマンスを向上させる](smb-direct.md)
* [Hyper-v over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB マルチチャネルを展開する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [サーバーアプリケーション用の高速で効率的なファイルサーバーの展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: トラブルシューティングガイド](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)