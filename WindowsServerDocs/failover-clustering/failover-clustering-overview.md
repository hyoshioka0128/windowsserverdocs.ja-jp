---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: フェールオーバー クラスタリング
ms.prod: windows-server-threshold
layout: LandingPage
ms.topic: landing-page
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 03/08/2019
ms.localizationpriority: high
ms.openlocfilehash: 445de065ff5b68b83481ee5bd83ebf18fdd180a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848653"
---
# <a name="failover-clustering-in-windows-server"></a>Windows Server のフェールオーバー クラスタリング

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<hr />

フェールオーバー クラスターは、互いに連携する個々のコンピューターが集まって形成され、クラスター化された役割 (以前は、クラスター化されたサービス、クラスター化されたアプリケーションと呼ばれていました) の可用性とスケーラビリティを高めます。 クラスター サーバー (ノード) は、物理ケーブルとソフトウェアにより接続されます。 クラスター ノードに障害が発生した場合、他のノードがサービスの提供を開始します。このプロセスを "フェールオーバー" といいます。 また、クラスター化された役割は能動的に監視され、正常に機能しているかどうかが確認されます。 正常に機能していない役割は、再起動されるか、または別のノードに移されます。

フェールオーバー クラスターには、一貫性のある分散名前空間を提供するクラスターの共有ボリューム (CSV) 機能も用意されています。これにより、クラスター化された役割のすべてのノードから共有記憶域にアクセスできます。 フェールオーバー クラスタリング機能により、ユーザーに対するサービスの中断を最小限に抑えることができます。

フェールオーバー クラスタリングには、次のような多くの実用的なアプリケーションがあります。
* Microsoft SQL Server、Hyper-V 仮想マシンなどのアプリケーションを対象とした高可用性 (継続的に使用可能な) ファイル共有記憶域
* 物理サーバー上、または Hyper-V を実行するサーバーにインストールされた仮想マシン上で実行される高可用性のクラスター化された役割

<hr />

<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-whats-new.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h2><a href="whats-new-in-failover-clustering.md">フェールオーバー クラスタ リングの新機能</a></h2>
                                        </div>
                                    </div>
                                </div>
                             </div>
                          </a>
                        </li>
                     </ul>
<HR />

<ul class="cardsF panelContent">

<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>概要</h3>
<HR />
                                        <p><a href="sofs-overview.md">アプリケーション データ用のスケール アウト ファイル サーバー</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/understand-quorum.md">クラスターとプールのクォーラム</a></p>
<HR />
                                        <p><a href="fault-domains.md">障害ドメインの認識</a></p>
<HR />
                                        <p><a href="smb-multichannel.md">簡略化された SMB マルチ チャネルと複数の NIC のクラスター ネットワーク</a></p>
<HR />
                                        <p><a href="vm-load-balancing-overview.md">VM の負荷分散</a></p>
<HR />
                                        <p><a href="../storage/storage-spaces/cluster-sets.md">クラスターの設定</a></p>
<HR />
                                        <p><a href="cluster-affinity.md">クラスターのアフィニティ</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>

<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>計画</h3>
<HR />
                                        <p><a href="clustering-requirements.md">フェールオーバー クラスタ リングのハードウェア要件と記憶域オプション</a></p>
<HR />
                                        <p><a href="failover-cluster-csvs.md">クラスター共有ボリューム (Csv)</a></p>               
<HR />
                                        <p><a href="../storage/storage-spaces/storage-spaces-direct-in-vm.md">仮想マシンのゲスト クラスターを使用して、記憶域スペース ダイレクト</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>展開</a></h3> 
<HR />
                                        <p><a href="prestage-cluster-adds.md">Active Directory Domain Services でクラスター コンピューター オブジェクトを事前設定します。</a></p>
<HR />
                                        <p><a href="create-failover-cluster.md">フェールオーバー クラスターの作成</a></p> 
<HR />
                                        <p><a href="deploy-two-node-clustered-file-server.md">2 ノード ファイル サーバーを展開します。</a></p> 
<HR />
                                        <p><a href="manage-cluster-quorum.md">クォーラムと監視サーバーを管理します。</a></p> 
<HR />
                                        <p><a href="deploy-cloud-witness.md">クラウド監視を展開します。</a></p>
<HR />
                                        <p><a href="file-share-witness.md">ファイル共有監視をデプロイします。</a></p>
<HR />
                                        <p><a href="cluster-operating-system-rolling-upgrade.md">クラスターのオペレーティング システムのローリング アップグレード</a></p> 
<HR />
                                        <p><a href="upgrade-option-same-hardware.md">同じハードウェア上でフェールオーバー クラスターをアップグレードします。</a></p>
<HR />
                                        <p><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\)">Active Directory のデタッチされたクラスターをデプロイします。</a></p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
                     </ul>
<HR />
<ul class="cardsF panelContent">
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>管理</h3>
<HR />
                                        <p><a href="cluster-aware-updating.md">クラスター対応更新</a></p> 
<HR />
                                        <p><a href="health-service-overview.md">ヘルス サービス</a></p>
<HR />
                                        <p><a href="cluster-domain-migration.md">クラスターのドメインの移行</a></p>
<HR />
                                        <p><a href="troubleshooting-using-wer-reports.md">Windows エラー報告を使用したトラブルシューティング</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>ツールと設定</a></h3>
<HR />
                                        <p><a href="https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps">フェールオーバー クラスタ リングの PowerShell コマンドレット</a></p> 
<HR />
                                        <p><a href="https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps">クラスター対応更新の PowerShell コマンドレット</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
<li>
                         <div class="cardSize">
                                <div class="cardPadding">
                                    <div class="card">
                                        <div class="cardImageOuter">
                                            <div class="cardImage">
                                                <img src="../media/i-cluster.svg" alt="" />
                                            </div>
                                        </div>
                                        <div class="cardText">
                                        <h3>コミュニティ リソース</a></h3>
<HR />
                                        <p><a href="https://go.microsoft.com/fwlink/p/?LinkId=230641">高可用性 (クラスタ リング) フォーラム</a></p> 
<HR />
                                        <p><a href="http://blogs.msdn.com/b/clustering/">フェールオーバー クラスタ リングとネットワーク負荷分散のチーム ブログ</a></p> 
                                        </div>
                                    </div>
                                </div>
                            </div>
                          </a>
                        </li>
</ul>
