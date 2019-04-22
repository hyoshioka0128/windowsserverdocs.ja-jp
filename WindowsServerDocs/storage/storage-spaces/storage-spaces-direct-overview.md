---
title: 記憶域スペース ダイレクトの概要
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/06/2019
ms.assetid: 8bd0d09a-0421-40a4-b752-40ecb5350ffd
description: 記憶域スペース ダイレクト、クラスターのサーバーの内部記憶域にソフトウェア定義記憶域ソリューションに使用する Windows Server の機能の概要。
ms.localizationpriority: medium
ms.openlocfilehash: 25de20b398f780f5da07b6b6cf4d396a7d12204a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823893"
---
# <a name="storage-spaces-direct-overview"></a>記憶域スペース ダイレクトの概要

>適用対象:Windows Server 2019、Windows Server 2016

記憶域スペース ダイレクトは、業界標準のサーバーとローカルで接続されているドライブを使用して、従来の SAN や NAS 配列の何分の 1 かのコストで、可用性と拡張性が高いソフトウェア定義の記憶域を作ります。 コンバージドまたはハイパーコンバージド アーキテクチャを大幅に合理化調達と展開の機能の中に、キャッシュ、記憶域階層、イレイジャー コーディング、および RDMA ネットワーク キングや NVMe ドライブなどの最新のハードウェア イノベーションと共に配信など優れた効率性とパフォーマンス。

記憶域スペース ダイレクトに含まれている Windows Server 2019 Datacenter、Windows Server 2016 Datacenter、および[Windows Server Insider Preview ビルド](https://insider.windows.com/for-business-getting-started-server/)します。 

記憶域スペースのスタンドアロン サーバー、共有 SAS クラスターなどの他のアプリケーションを参照してください。[記憶域スペースの概要](overview.md)します。 必要な場合の詳細について、Windows 10 PC で記憶域スペースを使用して、参照してください。 [Windows 10 での記憶域スペース](https://support.microsoft.com/help/12438/windows-10-storage-spaces)します。

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>理解します。</a></strong>
            <ul>
              <li>概要 (このページ)</li>
              <li><a href="understand-the-cache.md">キャッシュを理解します。</a></li>
              <li><a href="storage-spaces-fault-tolerance.md">フォールト トレランスと記憶域の効率性</a></li>
              <li><a href="drive-symmetry-considerations.md">ドライブの対称性に関する考慮事項</a></li>
              <li><a href="understand-storage-resync.md">理解し、記憶域の再同期の監視</a></li>
              <li><a href="understand-quorum.md">クラスターとプールのクォーラムを理解します。</a></li>
              <li><a href="cluster-sets.md">クラスターの設定</a></li>
            </ul>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>プラン</a></strong>
            <ul>
              <li><a href="storage-spaces-direct-hardware-requirements.md">ハードウェア要件</a></li>
              <li><a href="csv-cache.md">インメモリ CSV を使用してキャッシュを読み取る</li>
              <li><a href="choosing-drives.md">ドライブを選択します。</a></li>
              <li><a href="plan-volumes.md">ボリュームを計画します。</a></li>
              <li><a href="storage-spaces-direct-in-vm.md">ゲスト VM のクラスターを使用します。</a></li>
              <li><a href="storage-spaces-direct-disaster-recovery.md">ディザスター リカバリー</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>展開</a></strong>
            <ul>
                    <li><a href="deploy-storage-spaces-direct.md">記憶域スペースを直接デプロイします。</a></li>
                    <li><a href="create-volumes.md">ボリュームを作成します。</a></li>
              <li><a href="nested-resiliency.md">入れ子になったの回復性</a></li>
              <li><a href="../../failover-clustering/manage-cluster-quorum.md">クォーラムを構成します。</a></li>
              <li><a href="upgrade-storage-spaces-direct-to-windows-server-2019.md">Windows Server 2019 に記憶域スペース ダイレクト クラスターをアップグレードします。</a></li>
            </ul>
        </td>        
        <td style="padding: 5px; border: 0;">
            <strong>管理します。</a></strong>
            <ul>
              <li><a href="../../manage/windows-admin-center/use/manage-hyper-converged.md">Windows Admin Center で管理します。</a></li>
              <li><a href="add-nodes.md">サーバーまたはドライブを追加します。</a></li>
              <li><a href="maintain-servers.md">メンテナンスのサーバーをオフラインにすること</li>
              <li><a href="remove-servers.md">サーバーを削除します。</a></li>
              <li><a href="resize-volumes.md">ボリュームを拡張します。</a></li>
              <li><a href="../update-firmware.md">ドライブのファームウェアを更新します。</a></li>
              <li><a href="performance-history.md">パフォーマンス履歴</a></li>
              <li><a href="delimit-volume-allocation.md">ボリュームの割り当てを区切る</a></li>
            </ul>
        </td>
    </tr>
    <tr style="border: 0;">
         <td style="padding: 5px; border: 0;">
            <strong>トラブルシューティング</a></strong>
            <ul>
              <li><a href="storage-spaces-states.md">正常性と操作状態をトラブルシューティングします。</a></li>
              <li><a href="data-collection.md">記憶域スペース ダイレクトの診断データを収集します。</a></li>
            </ul>
         <td style="padding: 5px; border: 0;">
            <strong>最近投稿されたブログ</a></strong>
            <ul>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/30/windows-server-2019-and-intel-optane-dc-persistent-memory/">記憶域スペース ダイレクト 13.7 件 IOPS: ハイパー コンバージド インフラストラクチャの新しい業界レコード</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/10/02/hci-the-countdown-clock-starts-now/">Windows Server 2019 - ハイパー コンバージド インフラストラクチャ、カウント ダウンのクロックは今すぐ開始!</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/">Windows Server Summit から 5 つの大きなお知らせ</a></li>
              <li><a href="https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/">10,000 の記憶域スペース ダイレクト クラスターとカウントしています.</a></li>
            </ul>
</table>

## <a name="videos"></a>ビデオ

**簡単なビデオ概要 (5 分)**

<iframe src="https://www.youtube-nocookie.com/embed/raeUiNtMk0E" width="560" height="315" allowfullscreen></iframe>

**記憶域スペース ダイレクトでは、Microsoft Ignite 2018 (1 時間)**

[YouTube に配信されます。](https://www.youtube.com/watch?v=5kaUiW3qo30)

**記憶域スペース ダイレクトでは、Microsoft Ignite 2017 (1 時間)**

[YouTube に配信されます。](https://www.youtube.com/watch?v=YDr2sqNB-3c)

**Microsoft Ignite 2016 (1 時間) のイベントを起動します。**

[YouTube に配信されます。](https://www.youtube.com/watch?v=-LK2ViRGbWs)

## <a name="key-benefits"></a>主な利点

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/simplicity-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>わかりやすくするためです。</b> Windows Server 2016 を実行する業界標準のサーバーから、最初の記憶域スペース ダイレクト クラスターに移行するまでにかかる時間は 15 分未満です。 System Center ユーザーの場合、1 個のチェックボックスのみで展開が完了します。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/performance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>優れたパフォーマンス。</b> 記憶域スペース ダイレクトは、すべてフラッシュでもハイブリッドでも、一貫性があり、低遅延で、<a href="https://blogs.technet.microsoft.com/filecab/2016/07/26/storage-iops-update-with-storage-spaces-direct/">サーバーあたりの混合 4K ランダム IOPS が 150,000 回</a>を軽々と超えます。これは、ハイパーバイザーが組み込まれているアーキテクチャ、その組み込みの読み取り/書き込みキャッシュ、PCIe バスに直接マウントされた最新の NVMe ドライブのサポートの利点です。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/fault-tolerance-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>フォールト トレランス。</b> 組み込みの回復性は、継続的可用性を備えた、ドライブ、サーバー、またはコンポーネントの障害を処理します。 <a href="../../failover-clustering/fault-domains.md">シャーシおよびラックのフォールト トレランス</a>向けに大規模な展開も構成できます。 ハードウェアで障害が発生した場合は、交換するだけで済みます。ソフトウェアは自己修復されるので、複雑な管理手順は必要ありません。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/efficiency-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>リソースの効率。</b> イレイジャー コーディングは、ローカル再構築コードや ReFS リアルタイム階層などの独自の新技術で記憶域の効率を最大 2.4x に向上し、そのメリットをハード ディスク ドライブや混合ホット/コールド ワークロードにまで広げています。さらに、CPU 使用量が最小限に抑えられるので、最もリソースが必要な場所、つまり VM にリソースを戻すことができます。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/manageability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>管理の容易性。</b> <a href="../storage-qos/storage-qos-overview.md">記憶域 QoS 制御</a>で、VM ごとの IOPS の下限値と上限値を使用して、負荷が高い VM を監視します。 <a href="../../failover-clustering/health-service-overview.md">ヘルス サービス</a>は継続的な組み込みの監視機能とアラート機能を提供します。また、新しい API を使用して、高機能でクラスター全体のパフォーマンスおよび容量メトリックを簡単に収集できます。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:100px">
            <img src="media/storage-spaces-direct-in-windows-server-2016/scalability-icon.png" width="100" alt="">
        </td>
        <td style="padding: 10px; border: 0;">
            <b>スケーラビリティです。</b> 最大 16 台のサーバー、400 台を超えるドライブで、クラスターあたり最大 1 ペタバイト (1,000 テラバイト) の記憶域を実現できます。 スケール アウトするには、単にドライブを追加するか、サーバーを追加します。記憶域スペース ダイレクトによって新しいドライブが自動的に追加され、使用されるようになります。 記憶域の効率とパフォーマンスは、規模に応じた予測どおりに改善されます。
        </td>
    </tr>
</table>

## <a name="deployment-options"></a>展開オプション

記憶域スペース ダイレクトは、2 つの異なる展開オプション向けに設定されました。

### <a name="converged"></a>コンバージド

**ストレージとコンピューティングを個別のクラスター。** コンバージド展開オプションは、"非集約型" とも呼ばれ、記憶域スペース ダイレクト上にスケールアウト ファイル サーバー (SoFS) を重ねることで、SMB 3 ファイル共有上のネットワーク接続記憶域を提供します。 これにより、記憶域クラスターとは独立して計算/ワークロードをスケーリングできるので、サービス プロバイダーや大企業向けの Hyper-V IaaS (サービスとしてのインフラストラクチャ) など、大規模な展開には不可欠です。

![記憶域スペース ダイレクトは、スケール アウト ファイル サーバー機能を使用するストレージを別のサーバーまたはクラスター内の Hyper-V VM に提供します。](media/storage-spaces-direct-in-windows-server-2016/converged-minimal.png)

### <a name="hyper-converged"></a>ハイパーコンバージド

**コンピューティングとストレージの 1 つのクラスター。** ハイパーコンバージド展開オプションでは、ローカル ボリュームに記憶域があり、ファイルを格納するサーバー上で、Hyper-V 仮想マシンまたは SQL Server データベースを直接実行します。 この展開では、ファイル サーバーのアクセス権やアクセス許可を構成する必要がないので、中小規模の企業や、リモート オフィスや支社の展開の場合にはハードウェアのコストを削減できます。 参照してください[記憶域スペースを直接デプロイ](deploy-storage-spaces-direct.md)します。

![記憶域スペース ダイレクトが、同じクラスター内の Hyper-V VM にストレージを提供](media/storage-spaces-direct-in-windows-server-2016/hyper-converged-minimal.png)

## <a name="how-it-works"></a>方法

記憶域スペース ダイレクトは、Windows Server 2012 で初めて導入された記憶域スペースが進化したものです。 記憶域スペース ダイレクトは現在の Windows Server でなじみのある多くの機能を利用しています。たとえば、フェールオーバー クラスタリング、クラスター共有ボリューム (CSV) ファイル システム、サーバー メッセージ ブロック (SMB) 3、そして当然ながら記憶域スペースです。 また、ソフトウェア記憶域バスを代表として、新しいテクノロジも導入しています。

ここでは、記憶域スペース ダイレクトのスタックの概要について説明します。

![記憶域スペース ダイレクトのスタック](media/storage-spaces-direct-in-windows-server-2016/converged-full-stack.png)

**ネットワー キング ハードウェア。** 記憶域スペース ダイレクトは、イーサネット上のサーバー間の通信に SMB ダイレクトや SMB マルチチャネルを含む SMB3 を使用しています。 リモートダイレクト メモリ アクセス (RDMA) に対応する 10+ GbE を強くお勧めします (iWARP または RoCE)。

**記憶域ハードウェア。** SATA、SAS、または NVMe ドライブがローカル接続された 2 台から 16 台のサーバー。 各サーバーには 2 台以上のソリッドステート ドライブ、4 台以上の追加ドライブが必要です。 SATA デバイスと SAS デバイスは、ホストバス アダプター (HBA) と SAS エキスパンダーの背後に配置することをお勧めします。 マイクロソフトのパートナー製のプラットフォーム (近日公開予定) は、慎重に設計され、広範囲にわたって検証されているので、強くお勧めします。

**フェールオーバー クラスタ リングします。** サーバーの接続には、Windows Server に組み込まれているクラスタリング機能が使用されます。

**ソフトウェア記憶域バス。** ソフトウェア記憶域バスは、記憶域スペース ダイレクトで導入された新機能です。 ソフトウェア記憶域バスはクラスター全体にまたがり、ソフトウェア定義の記憶域ファブリックを確立するので、すべてのサーバーが相互のローカル ドライブすべてを見ることができます。 コストがかかり、制限が多いファイバー チャネルや共有 SAS ケーブル接続の代替として考えることができます。

**記憶域バス層キャッシュ。** The Software Storage Bus は、サーバー側の読み取り/書き込みの IO を短縮し、スループットを向上するキャッシュを提供する低速のドライブ (Hdd など) に最速のドライブに存在 (SSD など) を動的にバインドします。

**記憶域プール。** 記憶域スペースの基礎となるドライブのコレクションは、記憶域プールと呼ばれます。 記憶域プールは自動的に作成され、対象となるすべてのドライブは自動的に検出され、記憶域プールに追加されます。 既定の設定で、1 クラスターに 1 つのプールを使用することを強くお勧めします。 詳しくは、[記憶域プールの詳細に関するブログの記事](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)を参照してください。

**記憶域スペース。** 記憶域スペースは、[ミラーリング、イレイジャー コーディング、またはその両方](storage-spaces-fault-tolerance.md)を使用して、仮想 "ディスク" にフォールト トレランス機能を提供します。 記憶域スペースは、プール内のドライブを使用する分散型でソフトウェア定義の RAID と考えることができます。 記憶域スペース ダイレクトでは、このような仮想ディスクは、ドライブまたはサーバー エラーが同時に 2 つ発生した場合でも回復できますが (別のサーバーに各データ コピーを持つ 3 方向ミラーリングなど)、シャーシとラックのフォールト トレランスも実装できます。

**Resilient File System (ReFS)。** ReFS は、仮想化に特化して構築された高度なファイルシステムです。 作成、拡張、チェックポイントのマージなどの .vhdx ファイル操作の大幅な高速化、ビット エラーを検出して修正する組み込みのチェックサムなどの機能もあります。 また、使用量に基づき、リアルタイムで、いわゆる "ホット" 記憶域階層と "コールド" 記憶域階層間でデータを回転させる、リアルタイム階層化も導入されています。

**クラスターの共有ボリューム。** CSV ファイル システムは、すべての ReFS ボリュームを任意のサーバーからアクセスできる 1 つの名前空間に統合します。そのため、各サーバーに対して、すべてのボリュームはローカルにマウントされているかのように見え、動作します。

**スケール アウト ファイル サーバー。** この最後の層は、コンバージド展開の場合にのみ必要です。 Hyper-V を実行する別のクラスターなど、クライアントに対して、ネットワーク上で SMB3 アクセス プロトコルを使用したリモート ファイル アクセスを提供します。実質的に、記憶域スペース ダイレクトをネットワーク接続記憶域 (NAS) に変える機能があります。

## <a name="customer-stories"></a>顧客事例

ある[10,000 を超えるクラスター](https://blogs.technet.microsoft.com/filecab/2018/03/27/storage-spaces-direct-momentum/)記憶域スペース ダイレクトを世界中で実行します。 大企業および政府機関の何百ものノードを展開するだけの 2 つのノードを展開する小規模企業から、あらゆる規模の組織はの重要なアプリケーションやインフラストラクチャの記憶域スペース ダイレクトに依存します。

参照してください[Microsoft.com/HCI](https://www.microsoft.com/hci)事例に。

[![お客様のロゴのグリッド](media/storage-spaces-direct-in-windows-server-2016/customer-stories.png)](https://www.microsoft.com/hci)

## <a name="management-tools"></a>管理ツール

次のツールは、管理や監視記憶域スペース ダイレクトを使用できます。

| 名前 | グラフィカルまたはコマンド ラインでしょうか。 | 有料または含まれているでしょうか。 |
|-----------------|----------------------------|-------------------|
| [Windows Admin Center](../../manage/windows-admin-center/overview.md)     | グラフィック    | 含まれる |
| サーバー マネージャーとフェールオーバー クラスター マネージャー                                 | グラフィック    | 含まれる |
| Windows PowerShell                                                        | コマンド ライン | 含まれる |
| [System Center Virtual Machine Manager (SCVMM)](https://technet.microsoft.com/system-center-docs/vmm/manage/manage-storage-spaces-direct-vmm) & [Operations Manager (SCOM)](https://www.microsoft.com/download/details.aspx?id=54700) | グラフィック    | 有料     |

## <a name="get-started"></a>作業開始

[Microsoft Azure で](https://blogs.technet.microsoft.com/filecab/2016/05/05/s2dazuretp5/)記憶域スペース ダイレクトを試すか、「[Windows Server 評価版ソフトウェア](https://go.microsoft.com/fwlink/?linkid=842602)」から 180 日間ライセンスが有効な Windows Server の評価版をダウンロードします。

## <a name="see-also"></a>関連項目

-   [フォールト トレランスと記憶域の効率性](storage-spaces-fault-tolerance.md)
-   [記憶域レプリカ](../storage-replica/storage-replica-overview.md)
-   [At Microsoft のブログのストレージ](https://blogs.technet.microsoft.com/filecab/)
-   [Storage Spaces Direct throughput with iWARP (iWARP を使った記憶域スペース ダイレクトのスループット)](https://blogs.technet.microsoft.com/filecab/2017/03/13/storage-spaces-direct-throughput-with-iwarp) (TechNet ブログ)
-   [新機能では、Windows Server フェールオーバー クラスタ リングの新機能](../../failover-clustering/whats-new-in-failover-clustering.md)  
-   [記憶域サービスの品質](../storage-qos/storage-qos-overview.md)
-   [Windows IT プロフェッショナル向けのサポート](https://www.microsoft.com/itpro/windows/support)
