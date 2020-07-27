---
title: Windows Server バージョン 1709 の新機能
description: コンピューティング、ID、管理、自動化、ネットワーク、セキュリティ、記憶域の新機能は何ですか。
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: medium
ms.date: 06/03/2019
ms.openlocfilehash: a2e4b17a0f8f38812366dc2913e6c2ee25d4d137
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961154"
---
# <a name="whats-new-in-windows-server-version-1709"></a>Windows Server バージョン 1709 の新機能

>適用先:Windows Server (半期チャネル)

<img src=../media/landing-icons/new.png style='float:left; padding:.5em;' alt=Icon showing a newspaper>&nbsp;Windows の最新の機能については、「[Windows Server の新機能](whats-new-in-windows-server.md)」を参照してください。 ここでは、Windows Server バージョン 1709 の新機能および変更された機能について説明します。 ここに記載されている新機能と変更された機能は、このリリースを使う際に影響が最も大きいと思われるものです。 [Windows Server バージョン 1709 に関するブログの記事](https://cloudblogs.microsoft.com/windowsserver/2017/08/24/sneak-peek-1-windows-server-version-1709/)もご覧ください。

> [!IMPORTANT]
> Windows Server バージョン 1709 は、2019 年 4 月 9 日時点でサポート対象外です。


## <a name="new-cadence-of-releases"></a>新しいリリースのペース

今回のリリース以降、Windows Server の機能更新プログラムを入手するためのオプションは 2 つになります。
- **長期的なサービス チャネル (LTSC)** : これは、通常どおり、5 年間のメインストリーム サポートと 5 年間の延長サポートによるビジネスです。 過去 20 年間サポートされてきた方法と同じ方法で、2 ～ 3 年ごとに次の LTSC リリースにアップグレードするオプションが提供されます。
- **半期チャネル (SAC)** : これは、ソフトウェア アシュアランスの特典であり、実稼働環境で完全にサポートされます。 違いは、サポートされる期間が 18 か月間で、6 か月ごとに新しいバージョンがリリースされる点です。

リリース チャネルについては、以下の表で説明しています。

|   | 半期チャネル | Long Term Servicing チャネル |
| ------------- | ------------- | ------------ |
| リリース サイクル  | 年に 2 回 (春と秋)  | 2 ～ 3 年ごと |
| サポート スケジュール  | 18 か月間のメインストリームの運用サポート  | 5 年間のメインストリーム サポートと 5 年間の延長サポート |
| 可用性  | ソフトウェア アシュアランスまたは Azure (クラウドでホストされている場合)  | すべてのチャンネル |
| 名称に関する規則  | Windows Server バージョン YYMM  | Windows Server YYYY |

詳細については、[サービス チャネルの比較](../get-started-19/servicing-channels-19.md)に関するページを参照してください。

## <a name="application-containers-and-micro-services"></a>アプリケーションのコンテナーとマイクロサービス

- Server Core コンテナー イメージは、リフト アンド シフトのシナリオにさらに最適化されており、既存のコード ベースやアプリケーションを最小限の変更によりコンテナーに移行することができ、サイズも 60% 小さくなります。 
- Nano Server コンテナー イメージは、ほぼ 80% 小さくなっています。
    - Windows Server 半期チャネルでは、コンテナー ベース OS イメージとしての Nano Server が 390 MB から 80 MB に縮小されています。
- Hyper-V の分離による Linux コンテナー 

詳細については、「[Windows Server の次期リリースで Nano Server に加えられる変更](./nano-in-semi-annual-channel.md)」と[開発者向けの Windows Server バージョン 1709 に関するブログの記事](https://cloudblogs.microsoft.com/windowsserver/2017/09/13/sneak-peek-3-windows-server-version-1709-for-developers/)をご覧ください。

## <a name="modern-management"></a>最新の管理機能

IT 管理者によるトラブルシューティング、構成、メンテナンスのコア シナリオを支援する、簡素化、統合され、セキュリティを備えたエクスペリエンスについては、[Project Honolulu に関するページ](../manage/windows-admin-center/overview.md)をご覧ください。  Project Honolulu には、簡易性、統合性、セキュリティ、拡張性を備えたインターフェイスを持つ、次世代ツールが含まれています。
Project Honolulu には、PC、Windows サーバー、フェールオーバー クラスターだけでなく、記憶域スペース ダイレクトに基づくハイパーコンバージド インフラストラクチャを管理できる、まったく新しいの直感的な管理エクスペリエンスが含まれており、運用コストを削減することができます。

## <a name="compute"></a>計算

**Nano コンテナーと Server Core コンテナー**: 何よりもまず、今回のリリースはアプリケーションの革新を推進しています。 Nano Server、つまりホストとしての Nano は推奨されなくなり、Nano コンテナー (コンテナー イメージとして実行される Nano) に置き換えられています。 

コンテナーの詳細については、[コンテナー ネットワークの概要に関するページ](../networking/sdn/technologies/containers/container-networking-overview.md)をご覧ください。

**コンテナーとしての Server Core** (およびインフラストラクチャ) ホストにより、現代化プロセスの途中である既存のアプリケーションの柔軟性、密度、パフォーマンスが向上し、既にクラウド モデルを使用して開発されている新しいアプリがブランド化されます。

**VM スタート順序指定**も、OS とアプリケーションの対応により機能が向上しており、次の VM を起動する前に VM が起動したと見なされるときのトリガーが強化されました。

**VM の記憶域クラス メモリのサポート**により、NTFS フォーマットの直接アクセス ボリュームを、不揮発性 DIMM 上に作成し、Hyper-V VM に公開できるようになりました。 これにより、Hyper-V VM は記憶域クラス メモリ デバイスの低待機時間のパフォーマンスの利点を活用できます。

**仮想永続メモリ (vPMEM)** は、ホスト上の直接アクセス ボリューム上に VHD ファイル (.vhdpmem) を作成し、vPMEM コントローラーを VM に追加して、作成されたデバイス (.vhdpmem) を VM に追加することにより、有効になります。 ホスト上の直接アクセス ボリューム上で vhdpmem ファイルを使って vPMEM をバックアップすることにより、柔軟な割り当てを行い、VM にディスクを追加するための使い慣れた管理モデルを活用できます。

**コンテナー記憶域: クラスター共有ボリューム (CSV) 上の永続データ ボリューム**。 Windows Server バージョン 1709 および最新の更新プログラムが適用された Windows Server 2016 では、記憶域スペース ダイレクト上の CSV を含む、CSV 上にある永続データ ボリュームに、コンテナーからアクセスするためのサポートが追加されました。 これにより、アプリケーションのコンテナーは、コンテナー インスタンスが実行されているクラスター ノードに関係なく、永続的にボリュームにアクセスできます。 詳細については、[クラスター共有ボリューム (CSV)、記憶域スペース ダイレクト (S2D)、SMB グローバル マッピングによるコンテナー記憶域のサポートに関するブログの記事](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering)をご覧ください。

**コンテナー記憶域: SMB グローバル マッピングによる永続データ ボリューム**。 Windows Server バージョン 1709 では、SMB ファイル共有をコンテナー内のドライブ文字にマッピングするためのサポートを追加しました。これは、SMB グローバル マッピングと呼ばれます。 このマッピングされたドライブは、ローカル サーバー上のすべてのユーザーにアクセスできるようになり、データ ボリューム上のコンテナーの I/O は、マウントされたドライブを通じて、基になるファイル共有に対して行われます。 詳細については、[クラスター共有ボリューム (CSV)、記憶域スペース ダイレクト (S2D)、SMB グローバル マッピングによるコンテナー記憶域のサポートに関するブログの記事](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering)をご覧ください。

**仮想マシン構成ファイルの形式の更新**。 構成バージョン 8.2 以降の仮想マシン用に別のファイル (.vmgs) が追加されました。 VMGS は VMゲスト状態 (VM guest state) の略で、以前は VM ランタイム状態ファイルの一部であったデバイス状態を含む新しい内部ファイルです。

## <a name="security-and-assurance"></a>セキュリティおよび保証

**ネットワークの暗号化**によって、セキュリティとコンプライアンスのニーズに合わせて、ソフトウェア定義のネットワーク インフラストラクチャ上のネットワーク セグメントを迅速に暗号化することができます。

**ホスト ガーディアン サービス (HGS)** が、シールドされた VM として有効になっています。 このリリースの前は、3 ノードの物理クラスターを展開することをお勧めしていました。 これにより、管理者によって HGS 環境が侵害されることはありませんが、通常、コストは非常に高くなっていました。

**シールドされた VM としての Linux** がサポートされるようになりました。

詳細については、[保護されたファブリックとシールドされた VM の概要に関するページ](../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md)をご覧ください。

**SMBLoris の脆弱性** サービス拒否を引き起こす可能性がある "SMBLoris" と呼ばれる問題が解決されました。

## <a name="storage"></a>記憶域

**記憶域レプリカ**: Windows Server 2016 の記憶域レプリカによって追加されたディザスター リカバリーによる保護が拡張され、以下の機能が含まれるようになりました。
- **テスト フェールオーバー**: 宛先の記憶域をマウントするオプションが、テスト フェールオーバー機能によって可能になりました。 レプリケートされた記憶域のスナップショットを、宛先ノードで、テストやバックアップの目的で、一時的にマウントすることができます。  詳細については、「[記憶域レプリカについてよく寄せられる質問](https://aka.ms/srfaq)」をご覧ください。 
- **Project Honolulu のサポート**: サーバー間のレプリケーションのグラフィカル管理が、Project Honolulu でサポートされるようになりました。 これによって、一般的な障害対策のワークロードを管理するために PowerShell を使用する必要がなくなります。

**SMB**: 
- **SMB1 とゲスト認証の削除**: Windows Server バージョン 1709 では、SMB1 クライアントとサーバーが既定でインストールされなくなりました。 さらに、SMB2 以降のゲストとして認証する機能は、既定で無効になっています。 詳細については、[Windows 10 バージョン 1709 および Windows Server 1709 のバージョンで、SMBv1 が 既定でインストールされない問題に関するページ](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)をご覧ください。 

- **SMB2/SMB3 のセキュリティと互換性**: レガシ アプリケーションについて SMB2+ の oplock を無効にする機能や、クライアントからの接続ごとに署名や暗号化を要求する機能など、セキュリティやアプリケーションの互換性のための新しいオプションが追加されました。 詳細については、SMBShare PowerShell モジュールのヘルプを確認してください。

**データ重複除去**: 
- **データ重複除去で ReFS をサポート**: ReFS による最新ファイル システムの長所とデータ重複除去のいずれかを選択する必要がなくなりました。ReFS を有効にしているときにいつでもデータ重複除去を有効にできるようになりました。 ReFS によって記憶域の効率が 95% 以上向上します。
- **重複除去されたボリュームへの最適化された送受信のための DataPort API**: 開発者は、データ重複除去によって効率的にデータを保存する方法に関する知識を活用して、ボリューム、サーバー、クラスター間で効率的にデータを移動することができます。

## <a name="remote-desktop-services-rds"></a>リモート デスクトップ サービスの概要

**RDS が Azure AD と統合され**、条件付きアクセス ポリシー、多要素認証、Azure AD を使用した他の SaaS アプリとの統合認証などを活用できます。 詳細については、[RDS 展開と Azure AD Domain Services との統合に関するページ](../remote/remote-desktop-services/rds-azure-adds.md)をご覧ください。

>[!TIP]
>RDS で予定されている他の変更点の概要については、[リモート デスクトップ サービスの更新と今後予定されている新機能](https://techcommunity.microsoft.com/t5/microsoft-security-and/first-look-at-updates-coming-to-remote-desktop-services/ba-p/250320)に関するページを参照してください。

## <a name="networking"></a>ネットワーク

**Docker のルーティング メッシュ**がサポートされています。 入口ルーティング メッシュは、コンテナーに対する Docker の組み込みオーケストレーション ソリューションである [swarm モード](https://docs.docker.com/engine/swarm/)の一部です。 詳細については、[Windows Server バージョン 1709 で利用可能な Docker のルーティング メッシュに関する記事](https://techcommunity.microsoft.com/t5/virtualization/bg-p/Virtualization)をご覧ください。

**Docker 用の新機能**を利用できます。 詳細については、[Windows Server 1709 での Docker 用の新機能に関する記事](https://blog.docker.com/2017/09/docker-windows-server-1709/)を参照してください。

**Kubernetes 用 Linux と同等の Windows ネットワーク**: Windows は、ネットワークの観点で Linux と同等になりました。 お客様は、OS が混在する Kubernetes クラスターを、Azure、オンプレミス、サード パーティ製クラウド スタックなどのあらゆる環境で展開でき、回避策やスイッチ拡張機能を使用することなく、Linux でサポートされているものと同じネットワーク プリミティブおよびトポロジを活用できます。

**コア ネットワーク スタック**: コア ネットワーク スタックのいくつかの機能が強化されています。 これらの機能の詳細については、[Windows 10 の Creators Update の中心的なネットワーク スタック機能に関するページ](https://techcommunity.microsoft.com/t5/networking-blog/bg-p/NetworkingBlog)をご覧ください。
- **TCP Fast Open (TFO)** : TCP の 3 方向ハンドシェイク プロセスを最適化するために TFO のサポートが追加されました。 TFO は、標準的な 3 方向のハンドシェイクを使用して最初の接続でセキュリティで保護された TFO Cookie を確立します。  同じサーバーへの以降の接続では、ラウンド トリップ時間ゼロで接続するために、3 方向のハンドシェイクではなく、TFO Cookie を使用します。
- **CUBIC**: TCP の輻輳制御アルゴリズムである CUBIC の、実験用の Windows ネイティブ実装を使用できます。 次のコマンドはそれぞれ CUBIC を有効または無効にします。

    ```
    netsh int tcp set supplemental template=internet congestionprovider=cubic
    netsh int tcp set supplemental template=internet congestionprovider=compound
    ```

- **受信ウィンドウの自動調整**: TCP の自動調整ロジックは TCP 接続 "受信ウィンドウ" パラメーターを計算します。  高速で遅延の大きい接続で良好なパフォーマンス特性を実現するには、このアルゴリズムが必要です。  このリリースでは、特定の接続の最大受信ウィンドウの値を、ステップ関数を使用して収束させるようにアルゴリズムが変更されています。
- **TCP 統計 API**: SIO_TCP_INFO と呼ばれる新しい API が導入されています。  SIO_TCP_INFO によって、開発者はソケット オプションを使用して個々 の TCP 接続に関する豊富な情報を照会できます。
- **IPv6**: このリリースでは、IPv6 の複数の機能が強化されています。
  - **RFC 6106** のサポート: ルーター アドバタイズ (RA) を通じて DNS を構成できるようにする RFC 6106。 次のコマンドを使用して、RFC 6106 のサポートを有効または無効にすることができます。

    ```
    netsh int ipv6 set interface <ifindex> rabaseddnsconfig=<enabled | disabled>
    ```

  - **フロー ラベル**: Creators Update 以降、IPv6 経由の発信 TCP および UDP パケットでは、このフィールドが 5 タプル (接続元 IP、接続先 IP、接続元ポート、接続先ポート) のハッシュに設定されます。  これにより、IPv6 のみのデータ センターでの負荷分散またはフロー分類がより効率的に実行されます。 フローラベルを有効にするには:

    ```
    netsh int ipv6 set flowlabel=[disabled|enabled] (enabled by default)
    netsh int ipv6 set global flowlabel=<enabled | disabled>
    ```

  - **ISATAP と 6to4**: 将来の使用廃止に向けての一歩として、Creators Update ではこれらのテクノロジは既定で無効になっています。
- **停止しているゲートウェイの検出 (DGD)** : DGD アルゴリズムは、現在のゲートウェイにアクセスできないときに、自動的に別のゲートウェイに接続を移行します。 このリリースでは、ネットワーク環境を定期的に再プローブするようにアルゴリズムが強化されています。
- [Test-NetConnection](/powershell/module/nettcpip/test-netconnection?view=win10-ps) は、さまざまなネットワークの診断を実行する Windows PowerShell の組み込みのコマンドレットです。  このリリースでは、接続元アドレスの選択だけでなく、ルートの選択に関する詳細情報を提供するように、コマンドレットが強化されました。

**ソフトウェア定義ネットワーク**

- **仮想ネットワークの暗号化**は、"暗号化有効" とマークされているサブネット内で相互に通信する仮想マシン間で、仮想ネットワーク トラフィックを暗号化できるようにする新しい機能です。 この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。  DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。
 
**Windows 10 VPN**

- **ログオン前のインフラストラクチャ トンネル**。 既定では、Windows 10 VPN は、ユーザーが自分のコンピューターまたはデバイスにログオンしていない場合、インフラストラクチャ トンネルを自動的に作成しません。 ログオン前のインフラストラクチャ トンネルを自動的に作成するように Windows 10 VPN を構成するには、VPN プロファイルのデバイス トンネル (ログオン前) 機能を使用します。
- **リモート コンピューターおよびデバイスの管理**。  VPN プロファイルでデバイス トンネル (ログオン前) 機能を構成することによって、Windows 10 VPN クライアントを管理できます。 さらに、VPN インターフェイスに割り当てられている IP アドレスを内部の DNS サービスに動的に登録するように VPN 接続を構成する必要があります。
- **ログオン前のゲートウェイの指定**。 VPN プロファイルで、ログオン前のゲートウェイとデバイス トンネル (ログオン前) 機能を指定し、トラフィック フィルターと組み合わせることにより、デバイス トンネルを介して企業ネットワーク上のどの管理システムにアクセスできるかを制御できます。
