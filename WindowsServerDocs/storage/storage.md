---
title: ストレージ
description: ''
author: JasonGerend
manager: elizapo
layout: LandingPage
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 6b74bc7c-a58d-4915-af8e-2cc27f2c4726
ms.topic: landing-page
ms.author: jgerend
ms.localizationpriority: medium
ms.date: 03/08/2019
ms.openlocfilehash: d83d51ebf56d38f93c176d403ea5c6c14f625ee2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833803"
---
# <a name="storage"></a>ストレージ

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

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
                                            <p>新機能については、Windows Server 記憶域の新機能</p>
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
                        <p><h3><a href="storage-spaces/storage-spaces-direct-overview.md">記憶域スペース ダイレクト</a></h3> 新しいの物理ディスクを追加した後、ディスク使用量を最適化し、高速仮想ディスクの修復に要する時間、SATA、NVME デバイスなどのローカル ストレージを直接接続されています。 共有 SAS およびスタンドアロンの記憶域スペースについては、「<a href="storage-spaces/overview.md">記憶域スペース</a>」も参照してください。</p>
<HR />
                        <p><h3><a href="storage-replica/storage-replica-overview.md">記憶域レプリカ</a></h3> クラスターの障害対策と復旧、拡大できるだけでなく、フェールオーバー クラスターの高可用性のためサイト間でのサーバー間のレプリケーションの記憶域にとらわれない、ブロック レベルの同期 同期レプリケーションでは、クラッシュ前後の整合性が維持されるボリュームを使用して物理サイト内のデータのミラーリングを実現し、ファイル システム レベルでデータがまったく失われないようにします。</p>
<HR />
                        <p><h3><a href="storage-qos/storage-qos-overview.md">記憶域の品質 (qos)</a></h3> 一元的に監視し、HYPER-V およびスケール アウト ファイル サーバーの役割を自動的に使用して仮想マシンの記憶域のパフォーマンスの管理、同一のファイル サーバー クラスターを使用して複数の仮想マシン間で記憶域リソースの公平性を improveing します。</p>
<HR />
                        <p><h3><a href="data-deduplication/overview.md">データ重複除去</a></h3> 重複のボリューム上のデータを調べることで、ボリューム上の空き領域を最適化します。 特定された場合、ボリューム上のデータセットの重複する部分は、1 回だけ保存され、さらに節減するために (必要に応じて) 圧縮されます。 データ重複除去では、データの正確性や完全性を損なうことなく冗長性を最適化します。</p>
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
                        <p><h3><a href="storage-migration-service/overview.md">記憶域の移行サービス</a></h3>サーバーをサーバー上のデータのインベントリを作成、データと構成を以降のサーバーに転送し、必要に応じて移動、古いサーバーの id、新しいサーバーにそのため、グラフィカルなツールを使用して Windows Server の新しいバージョンに移行するアプリとユーザー何も変更する必要はありません。</p>
<HR />
                        <p><h3><a href="work-folders/work-folders-overview.md">ワーク フォルダー</a></h3> 保存し、アクセスは、パーソナル コンピューターとも呼ば bring your own device (BYOD)、会社の Pc だけでなく、デバイス上のファイルを作業します。 ユーザーは、アクセスしやすい場所に作業ファイルを保存し、そのファイルにはどこからでもアクセスできます。 組織は、一元管理されたファイル サーバーにファイルを格納し、必要に応じてユーザーのデバイス ポリシー (暗号化とロック画面のパスワードなど) を指定することで、企業のデータを管理します。</p>
<HR />
                        <p><h3><a href="folder-redirection/folder-redirection-rup-overview.md">オフライン ファイルとフォルダー リダイレクト</a></h3> 速度の向上と可用性のためにローカルでコンテンツをキャッシュ中に (ドキュメント フォルダー) などのローカル フォルダーのパスをネットワークの場所にリダイレクトします。</p>
<HR />
                        <p><h3><a href="folder-redirection/deploy-roaming-user-profiles.md">移動ユーザー プロファイル</a></h3> ユーザー プロファイルは、ネットワークの場所にリダイレクトします。</p>
<HR />
                        <p><h3><a href="dfs-namespaces/dfs-overview.md">DFS 名前空間</a></h3> 1 つまたは複数の論理的に構造化された名前空間に異なるサーバーに配置されている共有フォルダーをグループ化します。 ユーザーには、各名前空間が一連のサブフォルダーを含む 1 つの共有フォルダーのように見えます。 ただし、実際には、さまざまなサーバーおよび複数のサイトに配置された多数のファイル共有から、名前空間の基礎となる構造が構成されます。</p>
<HR />
                        <p><h3><a href="dfs-replication/dfsr-overview.md">DFS レプリケーション</a></h3> フォルダー (DFS 名前空間パスで参照されるを含む) は、複数のサーバーやサイト間でレプリケートします。 DFS レプリケーションは、RDC (Remote Differential Compression) と呼ばれる圧縮アルゴリズムを使用します。 RDC はファイル内のデータに対する変更を検出し、DFS レプリケーションにより、ファイル全体ではなく、変更されたファイル ブロックのみをレプリケートします。</p>
<HR />
                        <p><h3><a href="fsrm/fsrm-overview.md">ファイル サーバー リソース マネージャー</a></h3> 管理し、ファイル サーバーに格納されているデータを分類します。<p>
<HR />
                        <p><h3><a href="iscsi/iscsi-target-server.md">iSCSI ターゲット サーバー</a></h3> インターネット SCSI (iSCSI) 標準を使って、ネットワーク上の他のサーバーおよびアプリケーションにブロック記憶域を提供します。</p>
<HR />
                       <p><h3><a href="iscsi/iscsi-boot-overview.md">iSCSI ターゲット サーバー</a></h3> 何百もの一元的な場所に格納されている単一のオペレーティング システム イメージからコンピューターを起動できます。 これにより、効率、管理容易性、および可用性が向上し、セキュリティが強化されます。</p>
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
                        <p><h3><a href="refs/refs-overview.md">ReFS</a></h3> データの可用性が最大限回復力のあるファイル システムでは、多様なワークロードで非常に大きなデータ セットを効率的にスケールし、(ソフトウェアまたはハードウェアの障害) に関係なく破損部分の復元を使用してデータの整合性を提供します。<p>
<HR />
                        <p><h3><a href="file-server/file-server-smb-overview.md">サーバー メッセージ ブロック (SMB) プロトコル</a></h3> ネットワーク ファイル共有、コンピューター ネットワークにあるサーバー プログラムからサービスを要求してファイルに読み取りし、書き込みのコンピューターでアプリケーションを使用するプロトコル。 SMB プロトコルは、TCP/IP プロトコルをはじめとするネットワーク プロトコルの上位で使用できます。 SMB プロトコルを使えば、アプリケーション (またはアプリケーションのユーザー) がリモート サーバーにあるファイルなどのリソースにアクセスできます。 これにより、リモート サーバー上でアプリケーションがファイルを読み込み、作成、および更新できるようになります。 また、SMB クライアント リクエストを受け取ることができるように設定された任意のサーバー プログラムと通信できます。<p>
<HR />
                        <p><h3><a href="storage-spaces/Storage-class-memory-health.md">記憶域クラス メモリ</a></h3> 同様のパフォーマンスを提供します (非常に高速)、コンピューターのメモリが通常のストレージ ドライブのデータ永続化します。 Windows では、記憶域クラス メモリは、処理速度が高速である点を除けば通常のドライブと同様に処理されますが、デバイスの正常性管理の仕組みにいくつかの違いがあります。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/cc766295(v=ws.10).aspx">BitLocker ドライブ暗号化</a></h3> やオペレーティング システムが実行されていない場合でも、コンピューターが改ざんされると、暗号化された形式のボリュームにデータを格納します。 この機能により、オフライン攻撃や、インストール済みのオペレーティング システムを無効化または迂回した攻撃、ハード ドライブを物理的に取り外してデータを個別に狙う攻撃を防ぐことができます。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/dn466522(v=ws.11).aspx">NTFS</a></h3> 最近のバージョンの Windows および Windows Server のプライマリ ファイル システム、セキュリティ記述子、暗号化、ディスク クォータ、リッチ メタデータなどの機能の完全なセットし、継続的に提供するクラスター共有ボリューム (CSV) とを使用できますフェールオーバー クラスターの複数のノードから同時にアクセスできる使用可能なボリュームです。<p>
<HR />
                        <p><h3><a href="https://technet.microsoft.com/library/jj592688(v=ws.11).aspx">Network File System (NFS)</a></h3> ファイル共有を Windows と Windows 以外のコンピューターの両方で構成される異種環境を持つ企業向けのソリューションを提供します。<p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>

---


## <a name="in-azure"></a>Azure で

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure StorSimple](https://www.microsoft.com/en-us/cloud-platform/azure-storsimple)
