---
title: ストレージ
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: 5c8e6831e7e424896722c65d2ca6f34b3cc15e8d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820916"
---
# <a name="storage"></a>ストレージ

>適用対象: Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<hr />
Windows Server の記憶域では、仮想化されたワークロードに重点を置いて、ソフトウェア定義型データセンター (SDDC) ユーザー向けの新機能の追加と機能改善が行われました。 また、Windows Server では、既存のワークロードでファイル サーバーを使用する企業ユーザー向けに幅広いサポートも提供しています。

<hr />
<ul class="cardsF panelContent">
<li>
 <a href="whats-new-in-storage.md">
                            <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                            <h2>最新情報</h2>
                                            <p>Windows Server ストレージの新機能を確認する</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
<hr />
<ul class="cardsF panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>仮想化されたワークロード用のソフトウェア定義記憶域</h3>
<HR />
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">記憶域スペース ダイレクト</a></h3> SATA および NVME デバイスを含む直接接続されたローカルストレージ。新しい物理ディスクを追加した後のディスク使用量を最適化し、仮想ディスクの修復時間を短縮します。 共有 SAS およびスタンドアロンの記憶域スペースについては、「<a href="storage-spaces/overview.md">記憶域スペース</a>」も参照してください。</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">記憶域レプリカ</a></h3> ディザスターリカバリーと復旧のためのクラスターまたはサーバー間のストレージに依存しないブロックレベルの同期レプリケーション、および高可用性を実現するためのサイト間でのフェールオーバークラスターの拡張。 同期レプリケーションでは、クラッシュ前後の整合性が維持されるボリュームを使用して物理サイト内のデータのミラーリングを実現し、ファイル システム レベルでデータがまったく失われないようにします。</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">記憶域のサービスの品質 (QoS)</a></h3> Hyper-v とスケールアウトファイルサーバーの役割を使用して仮想マシンの記憶域のパフォーマンスを一元的に監視および管理し、同じファイルサーバークラスターを使用している複数の仮想マシン間で記憶域リソースの公平性を自動的に improveing します。</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">データ重複除去</a></h3> ボリューム上の重複するデータを調べて、ボリューム上の空き領域を最適化します。 特定された場合、ボリューム上のデータセットの重複する部分は、1 回だけ保存され、さらに節減するために (必要に応じて) 圧縮されます。 データ重複除去では、データの正確性や完全性を損なうことなく冗長性を最適化します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>汎用ファイル サーバー</h3>
<HR />
                        <p><h3><a href="storage-migration-service/overview.md">記憶域移行サービス</a></h3>サーバー上のデータをインベントリするグラフィカルツールを使用してサーバーを新しいバージョンの Windows Server に移行し、データと構成を新しいサーバーに転送してから、必要に応じて古いサーバーの id を新しいサーバーに移動します。これにより、アプリとユーザーは何も変更する必要がなくなります。</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">ワーク フォルダー</a></h3> 会社の Pc に加えて、個人のコンピューターやデバイス (BYOD) とも呼ばれる、仕事用ファイルを保存してアクセスします。 ユーザーは、アクセスしやすい場所に作業ファイルを保存し、そのファイルにはどこからでもアクセスできます。 組織は、一元管理されたファイル サーバーにファイルを格納し、必要に応じてユーザーのデバイス ポリシー (暗号化とロック画面のパスワードなど) を指定することで、企業のデータを管理します。</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">オフラインファイルとフォルダーのリダイレクト</a></h3> ローカルフォルダー (ドキュメントフォルダーなど) のパスをネットワーク上の場所にリダイレクトし、速度と可用性を向上させるためにコンテンツをローカルにキャッシュします。</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">移動ユーザープロファイル</a></h3> ユーザープロファイルをネットワーク上の場所にリダイレクトします。</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS 名前空間</a></h3> 異なるサーバー上にある共有フォルダーを、論理的に構造化された1つ以上の名前空間にグループ化します。 ユーザーには、各名前空間が一連のサブフォルダーを含む 1 つの共有フォルダーのように見えます。 ただし、実際には、さまざまなサーバーおよび複数のサイトに配置された多数のファイル共有から、名前空間の基礎となる構造が構成されます。</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">DFS レプリケーション</a></h3> 複数のサーバーおよびサイト間でフォルダーをレプリケートする (DFS 名前空間パスで参照されるフォルダーを含む)。 DFS レプリケーションは、RDC (Remote Differential Compression) と呼ばれる圧縮アルゴリズムを使用します。 RDC はファイル内のデータに対する変更を検出し、DFS レプリケーションにより、ファイル全体ではなく、変更されたファイル ブロックのみをレプリケートします。</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">ファイル サーバー リソース マネージャー</a></h3> ファイルサーバーに格納されているデータを管理および分類します。<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">iSCSI ターゲット サーバー</a></h3> インターネット SCSI (iSCSI) 標準を使って、ネットワーク上の他のサーバーおよびアプリケーションにブロック記憶域を提供します。</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI ターゲット サーバー</a></h3> は、1か所に格納されている単一のオペレーティングシステムイメージから数百台のコンピューターを起動できます。 これにより、効率、管理容易性、および可用性が向上し、セキュリティが強化されます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-store.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>ファイル システムやプロトコルなど</h3>
<HR />
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> データの可用性を最大化し、多様なワークロードの非常に大きなデータセットに効率よく拡張し、ソフトウェアまたはハードウェアの障害に関係なく、破損に対する回復性によってデータの整合性を確保する、回復力のあるファイルシステム。<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">サーバーメッセージブロック (SMB) プロトコル</a></h3> コンピューター上のアプリケーションがファイルの読み取りと書き込みを実行し、コンピューターネットワークのサーバープログラムからサービスを要求できるようにするネットワークファイル共有プロトコル。 SMB プロトコルは、TCP/IP プロトコルをはじめとするネットワーク プロトコルの上位で使用できます。 SMB プロトコルを使えば、アプリケーション (またはアプリケーションのユーザー) がリモート サーバーにあるファイルなどのリソースにアクセスできます。 これにより、リモート サーバー上でアプリケーションがファイルを読み込み、作成、および更新できるようになります。 また、SMB クライアント リクエストを受け取ることができるように設定された任意のサーバー プログラムと通信できます。<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">ストレージクラスのメモリ</a></h3> は、コンピューターメモリ (非常に高速) と同様にパフォーマンスを提供しますが、通常の記憶域ドライブのデータは永続化されます。 Windows では、記憶域クラス メモリは、処理速度が高速である点を除けば通常のドライブと同様に処理されますが、デバイスの正常性管理の仕組みにいくつかの違いがあります。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker ドライブ暗号化</a></h3> は、コンピューターが改ざんされた場合や、オペレーティングシステムが実行されていない場合でも、暗号化された形式でデータを保存します。 この機能により、オフライン攻撃や、インストール済みのオペレーティング システムを無効化または迂回した攻撃、ハード ドライブを物理的に取り外してデータを個別に狙う攻撃を防ぐことができます。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> Windows および Windows Server の最新バージョンのプライマリファイルシステムでは、セキュリティ記述子、暗号化、ディスククォータ、豊富なメタデータを含むすべての機能が提供されており、クラスター共有ボリューム (CSV) と共に使用して、フェールオーバークラスターの複数のノードから同時にアクセスできる継続的に使用可能なボリュームを提供できます。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">ネットワークファイルシステム (NFS)</a></h3> は、Windows コンピューターと Windows 以外のコンピューターの両方で構成される異種環境を持つ企業向けのファイル共有ソリューションを提供します。<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## <a name="in-azure"></a>Azure の場合

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/cloud-platform/azure-storsimple)
