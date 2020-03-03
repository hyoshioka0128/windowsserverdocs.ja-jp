---
title: Windows Server 2019 の新機能
description: デスクトップ エクスペリエンス、ストレージ移行サービス、システム インサイト、Azure ネットワーク アダプター、記憶域スペース ダイレクトの機能強化、およびその他の変更を含む、Windows Server 2019 での新機能の概要。
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 06/04/2019
ms.openlocfilehash: dd8cd6700323075a380aa062bfa1d208b3e30f83
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465496"
---
# <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019 の新機能

> 適用先:Windows Server 2019

このトピックでは、Windows Server 2019 の新機能の一部について説明します。 Windows Server 2019 は Windows Server 2016 の強力な基盤の上に構築されています。また、次の 4 つの主要テーマに沿って多数の技術革新が組み込まれています: ハイブリッド クラウド、セキュリティ、アプリケーション プラットフォーム、およびハイパー コンバージド インフラストラクチャ (HCI)。

Windows Server 半期チャネル リリースの新機能については、「[Windows Server の新機能](../get-started/whats-new-in-windows-server.md)」を参照してください。

## <a name="general"></a>全般

### <a name="windows-admin-center"></a>Windows Admin Center

Windows Admin Center は、サーバー、クラスター、ハイパーコンバージド インフラストラクチャ、Windows 10 PC を管理するための、ローカルに展開されるブラウザー ベースのアプリです。 Windows 以外の追加費用は必要なく、運用環境で使用できます。

Windows Admin Center は、Windows Server 2019 にも、Windows 10、以前のバージョンの Windows、Windows Server にもインストールすることができます。これを使用すれば、Windows Server 2008 R2 以降を実行しているサーバーおよびクラスターを管理することができます。

詳細については、[Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md) に関するページを参照してください。

### <a name="desktop-experience"></a>デスクトップ エクスペリエンス

Windows Server 2019 は長期サービス チャネル (LTSC) リリースであるため、<b>デスクトップ エクスペリエンス</b>が含まれています。 (半期チャネル \(SAC\) リリースには、設計上、デスクトップ エクスペリエンスは含まれていません。これらのリリースは厳密には Server Core および Nano Server コンテナー イメージ リリースです。)Windows Server 2016 の場合と同様、オペレーティング システムのセットアップ中には Server Core インストールまたはデスクトップ エクスペリエンス搭載サーバーのインストールを選択できます。

### <a name="system-insights"></a>システム インサイト

システム インサイトは、ローカルの予測分析機能を Windows Server にネイティブに導入する、Windows Server 2019 で利用可能な新機能です。 これらの予測機能は、それぞれ機械学習モデルによってサポートされており、パフォーマンス カウンターやイベントなどの Windows Server システム データをローカルで分析して、サーバーの機能に関するインサイトを提供します。これにより、Windows Server 展開での事後対応的な問題解決に関連する運用コストを削減できます。

## <a name="hybrid-cloud"></a>ハイブリッド クラウド

### <a name="server-core-app-compatibility-feature-on-demand"></a>サーバー コア アプリ互換性オンデマンド機能

[Server Core アプリ互換性オンデマンド機能 (FOD)](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19) では、Windows Server Core インストール オプションのアプリ互換性が大幅に向上しています。このオプションでは、Windows Server デスクトップ エクスペリエンスのバイナリとコンポーネントのサブセットが含められ、Windows Server デスクトップ エクスペリエンス グラフィカル環境自体は追加されません。  これは、Server Core をできる限り軽量に維持しつつ機能と互換性を高めるためです。  

このオプションのオンデマンド機能は、独立した ISO で提供され、DISM を使用して Windows Server Core インストールとイメージのみに追加できます。 

## <a name="security"></a>セキュリティ

### <a name="windows-defender-advanced-threat-protection-atp"></a>Windows Defender Advanced Threat Protection (ATP)

ATP のディープ プラットフォーム センサーおよび対応アクションは、メモリとカーネル レベルの攻撃を検出したうえで、対応として悪意のあるファイルを抑制し、悪意のあるプロセスを終了します。

-   Windows Defender ATP の詳細については、「[Windows Defender ATP 機能の概要](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview)」を参照してください。

-   サーバーのオンボーディングの詳細については、「[Windows Defender ATP サービスへのサーバーのオンボーディング](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-server-endpoints-windows-defender-advanced-threat-protection)」を参照してください。

**Windows Defender ATP Exploit Guard** は、新しいホスト侵入防止機能です。 Windows Defender Exploit Guard には 4 つのコンポーネントがあり、セキュリティ リスクと生産性の要件のバランスを取りつつ、さまざまな攻撃経路に対してデバイスをロックダウンし、マルウェアでよく使用される動作をブロックできるように設計されています。

-   [Attack Surface Reduction (ASR)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/attack-surface-reduction-exploit-guard?ocid=cx-blog-mmpc) は、疑わしいファイルおよび悪意のあるファイル (Office ファイルなど)、スクリプト、ラテラル ムーブメント、ランサムウェア動作、メール ベースの脅威をブロックすることにより、企業でコンピューターへのマルウェアの侵入を防止するための一連のコントロールです。

-   [ネットワーク保護](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/network-protection-exploit-guard?ocid=cx-blog-mmpc)では、Windows Defender SmartScreen によって、信頼されていないホスト/IP アドレスへの送信プロセスをデバイスでブロックすることにより、Web ベースの脅威からエンドポイントを保護します。

-   [フォルダー アクセスの制御](https://cloudblogs.microsoft.com/microsoftsecure/2017/10/23/stopping-ransomware-where-it-counts-protecting-your-data-with-controlled-folder-access/?ocid=cx-blog-mmpc?source=mmpc)では、信頼されていないプロセスから保護されたフォルダーへのアクセスをブロックすることで、機密データをランサムウェアから保護します。

-   [Exploit Protection](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-exploit-guard/exploit-protection-exploit-guard) は、脆弱性の悪用に対する軽減策のセット (EMET を置き換える機能) で、システムおよびアプリケーションの保護のために簡単に構成できます。

[Windows Defender アプリケーション制御](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) はコード整合性 (CI) ポリシーとも呼ばれており、Windows Server 2016 でリリースされた機能です。
この機能については、コンセプトは優れているが展開が難しいというフィードバックがお客様から寄せられました。
これに対処するため、すべての Windows インボックス ファイルおよび Microsoft アプリケーション (SQL Server など) を許可し、CI をバイパスできる既知の実行可能ファイルをブロックする、既定の CI ポリシーを作成しました。 

### <a name="security-with-software-defined-networking-sdn"></a>ソフトウェア定義ネットワーク (SDN) によるセキュリティ

[SDN のセキュリティ](https://docs.microsoft.com/windows-server/networking/sdn/security/sdn-security-top)では、オンプレミスまたはクラウドのサービス プロバイダーとして、ワークロードの実行に対するお客様の信頼度を向上するための多数の機能が提供されています。 

これらのセキュリティ強化機能は、Windows Server 2016 で導入された包括的な SDN プラットフォームに統合されています。

SDN の新機能の完全な一覧については、「[Windows Server 2019 の SDN の新機能](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new)」を参照してください。

### <a name="shielded-virtual-machines-improvements"></a>シールドされた仮想マシンの機能強化

- **ブランチ オフィスの機能強化**

    新しい[フォールバック HGS](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#fallback-configuration) 機能と[オフライン モード](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-manage-branch-office#offline-mode) 機能を利用することにより、ホスト ガーディアン サービスへの接続が断続的なコンピューターで、シールドされた仮想マシンを実行できるようになりました。 フォールバック HGS を使用すると、プライマリ HGS サーバーにアクセスできない場合に試すことができるように、Hyper-V の URL のセカンダリ セットを構成できます。

    オフライン モードでは、VM が一度正常に開始されたことがあり、ホストのセキュリティ構成が変更されていない限り、HGS にアクセスできない場合でも、シールドされた VM を継続的に起動できます。

- **トラブルシューティングの機能強化**

    VMConnect 拡張セッション モードと PowerShell ダイレクトのサポートが有効になり、[シールドされた仮想マシンのトラブルシューティング](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms)も容易になりました。 これらのツールは、VM へのネットワーク接続が失われたため構成を更新してアクセスを復元する必要がある場合に特に役立ちます。 

    これらの機能は構成する必要がなく、Windows Server Version 1803 以降を実行している Hyper-V ホストにシールドされた VM が配置されると、自動的に利用可能になります。

- **Linux のサポート**

    OS が混在する環境を使用している場合、Windows Server 2019 では、シールドされた仮想マシンでの Ubuntu、Red Hat Enterprise Linux、および SUSE Linux Enterprise Server の実行がサポートされるようになりました。

### <a name="http2-for-a-faster-and-safer-web"></a>HTTP/2 による高速かつ安全な Web

- 接続の結合機能の強化により、正しく暗号化された中断のない閲覧エクスペリエンスを実現します。

- 接続エラーの自動軽減と展開の容易さを目的として、HTTP/2 サーバー側暗号スイートのネゴシエーションがアップグレードされました。

- 高いスループットを提供するために、既定の TCP 輻輳プロバイダーが Cubic に変更されました。

## <a name="storage"></a>記憶域

Windows Server 2019 でストレージに行った変更の一部を次に示します。 詳細については、「[記憶域の新機能](../storage/whats-new-in-storage.md)」を参照してください。

### <a name="storage-migration-service"></a>ストレージ移行サービス

ストレージ移行サービスは、Windows Server の新しいバージョンにサーバーを移行しやすくする新しいテクノロジです。 このサービスには、データをサーバーにインベントリし、データと構成を新しいサーバーに転送して、必要に応じて古いサーバーの ID を新しいサーバーに移行するツールが用意されているため、アプリとユーザーは何も変更する必要がありません。 詳細については、「[ストレージ移行サービス](../storage/storage-migration-service/overview.md)」を参照してください。

### <a name="storage-spaces-direct"></a>記憶域スペース ダイレクト

記憶域スペース ダイレクトの新機能の一覧を次に示します。 詳細については、「[記憶域スペース ダイレクトの新機能](../storage/whats-new-in-storage.md#storage-spaces-direct)」を参照してください。 また、検証済みの記憶域スペース ダイレクト システムを取得する方法については、[Azure Stack HCI](https://docs.microsoft.com/azure-stack/operator/azure-stack-hci-overview) に関するページを参照してください。

- **ReFS ボリュームの重複除去と圧縮**
- **永続メモリのネイティブ サポート**
- **エッジの 2 ノード ハイパーコンバージド インフラストラクチャに対する入れ子の回復性**
- **監視として USB フラッシュ ドライブを使用した 2 つのサーバー クラスター**
- **Windows Admin Center サポート**
- **パフォーマンス履歴**
- **クラスターごとに 4 PB まで拡張可能**
- **ミラーリングによって高速化されたパリティで 2 倍の速度を実現**
- **ドライブの待機時間に関する外れ値の検出**
- **フォールト トレランスを向上するボリュームの割り当てを手動で区切る**

### <a name="storage-replica"></a>記憶域レプリカ

記憶域レプリカの新機能は次のとおりです。 詳細については、「[記憶域レプリカの新機能](../storage/whats-new-in-storage.md#storage-replica)」を参照してください。

- 記憶域レプリカは、Windows Server 2019 Standard Edition で利用可能になりました。
- テスト フェールオーバーは、レプリケーションまたはバックアップ データを検証するために、宛先の記憶域のマウントを許可する新しい機能です。 詳細については、「[記憶域レプリカについてよく寄せられる質問](../storage/storage-replica/storage-replica-frequently-asked-questions.md)」をご覧ください。
- 記憶域レプリカのログのパフォーマンスの向上
- Windows Admin Center サポート

## <a name="failover-clustering"></a>フェールオーバー クラスタリング

フェールオーバー クラスタリングの新機能の一覧を次に示します。 詳細については、「[フェールオーバー クラスタリングの新機能](../failover-clustering/whats-new-in-failover-clustering.md)」を参照してください。

- **クラスター セット**
- **Azure 対応のクラスター**
- **ドメイン間のクラスター移行**
- **USB 監視**
- **クラスター インフラストラクチャの機能強化**
- **クラスター対応更新による記憶域スペース ダイレクトのサポート**
- **ファイル共有監視の強化**
- **クラスターの強化**
- **フェールオーバー クラスターで使用されなくなった NTLM 認証**

## <a name="application-platform"></a>アプリケーション プラットフォーム

### <a name="linux-containers-on-windows"></a>Windows 上の Linux コンテナー

同じコンテナー ホストで同じ Docker デーモンを使用して、Windows および Linux ベースのコンテナーを実行できるようになりました。 これにより、異種コンテナーのホスト環境を持ちつつ、アプリケーション開発者に柔軟性を提供できます。

### <a name="built-in-support-for-kubernetes"></a>Kubernetes の組み込みサポート

Windows Server 2019 では、Windows で Kubernetes をサポートするために必要な半期チャネル リリースから、計算、ネットワーク、および記憶域への機能強化が続行されます。 詳細は、今後の Kubernetes リリースで公開されます。

- Windows Server 2019 の[コンテナーのネットワーク](https://docs.microsoft.com/windows-server/networking/sdn/technologies/containers/container-networking-overview)により、プラットフォームのネットワーク回復性とコンテナー ネットワーク プラグインのサポートが強化され、Windows での Kubernetes の使いやすさが大幅に向上します。

- Kubernetes に展開されたワークロードでは、ネットワーク セキュリティを使用して、埋め込みツールにより Linux と Windows の両方のサービスを保護できます。

### <a name="container-improvements"></a>コンテナーの機能強化
    
- **統合された ID 機能強化**

    Windows Server の以前のバージョンにあったいくつかの制限に対処し、コンテナー内の統合 Windows 認証の容易さと信頼性が向上しました。

- **アプリケーション互換性の向上**

    Windows ベースのアプリケーションのコンテナー化が簡単になりました。既存の *windowsservercore* イメージに対するアプリの互換性が向上しました。 追加の API 依存関係があるアプリケーション用に、*windows* という 3 つ目の基本イメージが用意されました。

- **サイズの縮小とパフォーマンスの向上**

    基本コンテナー イメージのダウンロード サイズ、ディスク上のサイズ、起動時間が改善されました。 これにより、コンテナー ワークフローの実行速度が向上します。

- **Windows Admin Center \(プレビュー\) を使用した管理エクスペリエンス**

    Windows Admin Center の新しい拡張機能により、これまでより簡単にコンピューターで実行しているコンテナーを表示し、個々のコンテナーを管理できるようになりました。 [Windows Admin Center パブリック フィード](https://docs.microsoft.com/windows-server/manage/windows-admin-center/configure/using-extensions)で "Containers" 拡張機能を探してください。

### <a name="encrypted-networks"></a>暗号化されたネットワーク

[暗号化されたネットワーク](https://docs.microsoft.com/windows-server/networking/sdn/sdn-whats-new) - 仮想ネットワークの暗号化を使用すると、"**暗号化有効**" とマークされているサブネット内で相互に通信する仮想マシン間で、仮想ネットワーク トラフィックの暗号化が有効になります。 また、この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。 DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。

### <a name="network-performance-improvements-for-virtual-workloads"></a>仮想ワークロードに関するネットワーク パフォーマンスの向上

[仮想ワークロードに関するネットワーク パフォーマンスの改善](https://docs.microsoft.com/windows-server/networking/technologies/hpn/hpn-insider-preview)により、仮想マシンへのネットワーク スループットが最大限に向上します。ホストの継続的な調整や過度のプロビジョニングは必要ありません。 これによって、利用可能なホストの密度を高めながら、運用コストとメンテナンス コストを削減できます。 これらの新機能の名前は次のとおりです。

* vSwitch の Receive Segment Coalescing

* 動的仮想マシン マルチキュー (d.VMMQ: Dynamic Virtual Machine Multi-Queue)

### <a name="low-extra-delay-background-transport"></a>Low Extra Delay Background Transport

Low Extra Delay Background Transport (LEDBAT) は、待機時間が最適化された、ネットワーク輻輳制御プロバイダーです。自動的に帯域幅をユーザーおよびアプリケーションに譲り、ネットワークが使用されていなければ使用可能な帯域幅全体を消費するように設計されています。   
このテクノロジは、お客様が直接使用するサービスや関連する帯域幅に影響を与えることなく、重要で大規模な更新プログラムを IT 環境全体に展開する場合に使用することを目的としています。

### <a name="windows-time-service"></a>Windows タイム サービス

[Windows タイム サービス](https://docs.microsoft.com/windows-server/networking/windows-time-service/insider-preview)には、UTC に厳密に準拠したうるう秒サポート、PTP (Precision Time Protocol) と呼ばれる新しい時刻プロトコル、エンド ツー エンドのトレーサビリティが含まれています。


### <a name="high-performance-sdn-gateways"></a>ハイパフォーマンス SDN ゲートウェイ

Windows Server 2019 の[ハイ パフォーマンス SDN ゲートウェイ](https://docs.microsoft.com/windows-server/networking/sdn/gateway-performance)により、IPsec および GRE 接続のパフォーマンスが大幅に向上し、従来よりずっと低い CPU 使用率での超高性能スループットを提供しています。
<br/>

### <a name="new-deployment-ui-and-windows-admin-center-extension-for-sdn"></a>SDN の新しい展開 UI と Windows Admin Center 拡張機能

Windows Server 2019 では、新しい展開 UI と Windows Admin Center 拡張機能により、だれもが SDN の機能を活用して、簡単に展開および管理できるようになりました。 

### <a name="persistent-memory-support-for-hyper-v-vms"></a>Hyper-V VM の永続メモリ サポート

永続メモリ ( 記憶域クラス メモリ) の高いスループットと短い待機時間を仮想マシンで活用するために、直接 VM に投影できるようになりました。 これにより、データベース トランザクションの待機時間を大幅に短縮し、低待機時間メモリ内データベースの障害時に復旧までの時間を短縮できます。

