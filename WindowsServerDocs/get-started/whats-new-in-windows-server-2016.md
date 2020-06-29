---
title: Windows Server 2016 の新機能
description: コンピューティング、ID、管理、自動化、ネットワーク、セキュリティ、記憶域の新機能は何ですか。
ms.prod: windows-server
ms.date: 05/21/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 2827f332-44d4-4785-8b13-98429087dcc7
author: jasongerend
ms.author: jgerend
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: c3eb62d53ef11d5531590e1a6d46cd6cacaf2e4a
ms.sourcegitcommit: 5bc5aaf341c711113ca03d1482f933b05b146007
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85094536"
---
# <a name="whats-new-in-windows-server-2016"></a>Windows Server 2016 の新機能

>適用先:Windows Server 2016

![新聞を示すアイコン](media/whats-new.png) Windows の最新の機能については、「[Windows Server の新機能](whats-new-in-windows-server.md)」を参照してください。 ここでは、Windows Server&reg; 2016 の新機能および変更された機能について説明します。 ここに記載されている新機能と変更された機能は、このリリースを使う際に影響が最も大きいと思われるものです。

## <a name="compute"></a>[Compute](../virtualization/virtualization.md)

仮想領域には、Windows Server を設計、展開、および保守する IT プロフェッショナル向けの仮想化製品と機能が含まれます。  

### <a name="general"></a>全般  
物理マシンと仮想マシンは、Win32 の時刻と Hyper-V の時刻同期サービスが向上したことによる時刻の精度の向上を享受できます。 Windows Server では、UTC に対して 1 ミリ秒の精度を必要とする今後の規制に準拠しているサービスをホストできるようになりました。  

### <a name="hyper-v"></a>Hyper-V  
-   [Windows Server 2016 の Hyper-V の新機能](../virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows.md)。 このトピックでは、Windows Server 2016 の Hyper-V の役割、Windows 10 で実行されているクライアント Hyper-V、および Microsoft Hyper-V Server 2016 で追加および変更された機能について説明します。  

-   [Windows コンテナー](https://msdn.microsoft.com/virtualization/windowscontainers/containers_welcome): Windows Server 2016 コンテナーのサポートによって、Windows 10 でパフォーマンスの向上、ネットワーク管理の簡素化、および Windows コンテナーのサポートが実現しています。 コンテナーの詳細については、「[Containers: Docker, Windows and Trends](https://azure.microsoft.com/blog/2015/08/17/containers-docker-windows-and-trends/)」(コンテナー: Docker、Windows、および傾向) を参照してください。  

### <a name="nano-server"></a>Nano Server  
[Nano Server](getting-started-with-nano-server.md) の新機能。 Nano Server には、物理ホストとゲスト仮想マシンの機能の分離の強化と、Windows Server のさまざまなエディションのサポートなど、Nano Server イメージを構築するための更新されたモジュールがあります。   

回復コンソールにも、受信と送信のファイアウォール ルールの分離、WinRM の構成を修復する機能などの機能強化があります。  

### <a name="shielded-virtual-machines"></a>シールドされた仮想マシン  
Windows Server 2016 には、不正に使用されているファブリックから 第 2 世代仮想マシンを保護することを目的として、Hyper-V ベースのシールドされた仮想マシンが用意されています。 Windows Server 2016 で導入された機能を次に示します。  

- 通常の仮想マシンよりも強化された保護を提供する一方で「シールド」モードよりは弱い新しい「暗号化のサポート」モード。vTPM、ディスクの暗号化、ライブ マイグレーション トラフィックの暗号化、およびその他の機能 (仮想マシンのコンソール接続や Powershell ダイレクトなどの便利な直接ファブリック管理機能を含む) を引き続きサポートします。  

- 自動化されたディスクの暗号化を含め、既存のシールドされていない第 2 世代仮想マシンからシールドされた仮想マシンへの変換を完全にサポートします。

- Hyper-V Virtual Machine Manager では、シールドされた仮想マシンの実行が許可された時点でファブリックを表示できるようになりました。このため、ファブリック管理者がシールドされた仮想マシンのキーの保護機能 (KP) を開き、仮想マシンの実行を許可されているファブリックを表示するための方法になります。  

- 実行中のホスト ガーディアン サービスの構成証明モードを切り替えることができます。 安全性が低い一方で単純な Active Directory ベースの構成証明と、TPM ベースの構成証明をその場で切り替えることができるようになりました。  

- 保護された Hyper-V ホストとホスト ガーディアン サービスの両方の構成で誤りやエラーを検出できる Windows PowerShell ベースのエンド ツー エンドの診断ツール。  

- シールドされた仮想マシン自体と同じレベルの保護機能を提供しながら、通常実行されるファブリック内のシールドされた仮想マシンを安全にトラブルシューティングし、修復をするための手段を提供する回復環境。

- ホスト ガーディアン サービスによる既存の安全な Active Directory のサポート。独自の Active Directory インスタンスを作成するのではなく、既存の Active Directory フォレストを Active Directory として使用するようにホスト ガーディアン サービスに対して指示できます。

シールドされた仮想マシンを使用するための詳細および手順については、[シールドされた VM と保護されたファブリックの検証ガイド: Windows Server 2016 (TPM)](https://aka.ms/shieldedvms) に関する記事を参照してください。  

## <a name="identity-and-access"></a>[ID およびアクセス](../identity/Identity-and-Access.yml)  
ID での新機能では、組織が Active Directory 環境をセキュリティで保護する機能が強化され、クラウドのみの展開およびハイブリッドの展開に移行するために役立ちます。ハイブリッドの展開では、一部のアプリケーションとサービスはクラウドでホストされ、残りはオンプレミスでホストされます。  

### <a name="active-directory-certificate-services"></a>Active Directory 証明書サービス  
Windows Server 2016 の Active Directory 証明書サービス (AD CS) では、TPM キーの構成証明のサポートが強化されます。キーの構成証明にスマート カード KSP を使用でき、ドメインに参加していないデバイスで NDES の登録を使用して、TPM にあるキーを証明できる証明書を取得できるようになりました。  

### <a name="active-directory-domain-services"></a>[Active Directory Domain Services]  
Active Directory ドメイン サービスでは、Active Directory 環境をセキュリティで保護し、会社と個人の両方のデバイスの優れた ID 管理環境を実現するのに役立つ機能強化が図られています。 詳細については、[Windows Server 2016 の Active Directory Domain Services (AD DS) の新機能](../identity/whats-new-active-directory-domain-services.md)に関するページを参照してください。   

### <a name="active-directory-federation-services"></a>Active Directory フェデレーション サービス  
Active Directory フェデレーション サービスの新機能。 Windows Server 2016 の Active Directory フェデレーション サービス (AD FS) には、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) ディレクトリに格納されているユーザーを認証するよう AD FS を構成できる新機能が追加されています。 詳細については、[Windows Server 2016 の AD FS の新機能](../identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server.md)に関する記事を参照してください。  

### <a name="web-application-proxy"></a>Web アプリケーション プロキシ  
Web アプリケーション プロキシの最新バージョンでは、より多くのアプリケーションの発行と事前認証を可能にする新機能に力を入れており、ユーザー エクスペリエンスの向上が図られています。 新機能の一覧をご覧ください。新機能には、Exchange ActiveSync などのリッチ クライアント アプリの事前認証や、SharePoint アプリの発行を容易にするワイルドカード ドメインなどがあります。 詳細については、「[Web Application Proxy in Windows Server 2016 (Windows Server 2016 の Web アプリケーション プロキシ)](../remote/remote-access/web-application-proxy/web-application-proxy-windows-server.md)」を参照してください。  

##  <a name="administration"></a>[管理](../administration/manage-windows-server.yml)  
管理と自動化の領域では、Windows PowerShell など Windows Server 2016 を実行および管理する IT プロフェッショナル向けのツールとリファレンス情報に力を入れています。

Windows PowerShell 5.1 に追加された重要な新機能には、クラスを使った開発のサポートや新しいセキュリティ機能があります。それらの機能により、用途が広がり、使いやすさが向上し、Windows ベースの環境をより簡単かつ包括的に制御して管理できます。 詳細については、「[WMF 5.1 の新しいシナリオと機能](https://docs.microsoft.com/powershell/wmf/5.1/scenarios-features)」を参照してください。

Windows Server 2016 には、Nano Server で PowerShell.exe を実行する機能 (リモートのみではなくなりました)、GUI に代わる新しいローカル ユーザーとグループのコマンドレット、PowerShell デバッグのサポートの追加、セキュリティ ログとトランスクリプションおよび JEA に対するサポートの Nano Server への追加など、新しい追加機能があります。

次に、その他の新しい管理機能を示します。

### <a name="powershell-desired-state-configuration-dsc-in-windows-management-framework-wmf-5"></a>Windows Management Framework (WMF) 5 の PowerShell Desired State Configuration (DSC)
Windows Management Framework 5 には、Windows PowerShell Desired State Configuration (DSC)、Windows リモート管理 (WinRM)、および Windows Management Instrumentation (WMI) に対する更新が含まれています。

Windows Management Framework 5 の DSC 機能のテストに関する詳細については、[PowerShell DSC の機能の検証](https://blogs.msdn.microsoft.com/powershell/2015/07/06/validate-features-of-powershell-dsc/)に関する一連のブログ記事を参照してください。 ダウンロードするには、[Windows Management Framework 5.1](https://docs.microsoft.com/powershell/scripting/wmf/setup/install-configure) に関するページを参照してください。

### <a name="packagemanagement-unified-package-management-for-software-discovery-installation-and-inventory"></a>PackageManagement 統合パッケージ管理によるソフトウェアの検出、インストール、およびインベントリ
Windows Server 2016 および Windows 10 には、新しい PackageManagement 機能 (旧称 OneGet) が含まれています。この機能により、IT 技術者や DevOps は、インストーラーのテクノロジやソフトウェアの配置場所にかかわらず、ソフトウェアの検出、インストール、およびインベントリ (SDII) をローカルまたはリモートで自動化できます。 

詳細については、[https://github.com/OneGet/oneget/wiki](https://github.com/OneGet/oneget/wiki) を参照してください。

### <a name="powershell-enhancements-to-assist-digital-forensics-and-help-reduce-security-breaches"></a>デジタル法科学を支援し、セキュリティ侵害の減少に役立つ PowerShell の機能強化
セキュリティが侵害されたシステムの調査を担当するチーム ("ブルー チーム" とも呼ばれます) を支援するために、PowerShell にログおよびその他の法科学機能が追加されたほか、スクリプトの脆弱性を減らし (制約付きの PowerShell など)、CodeGeneration API をセキュリティで保護するのに役立つ機能が追加されました。

詳しくは、「[PowerShell とブルー チーム](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)」を参照してください。

## <a name="networking"></a>[ネットワーク](../networking/index.yml)  
この領域には、IT プロフェッショナルが Windows Server 2016 を設計、展開、保守するためのネットワーク製品と機能が含まれています。  

### <a name="software-defined-networking"></a>ソフトウェアによるネットワーク制御
新規または既存の仮想アプライアンスにトラフィックをミラーすることとルート指定することの両方ができるようになりました。 分散型のファイアウォールとネットワーク セキュリティ グループと合わせて、これにより、Azure と同様の方法でワークロードを動的にセグメント化し、セキュリティで保護できます。 次に、System Center Virtual Machine Manager を使用して、ソフトウェアによるネットワーク制御 (SDN) スタック全体を展開および管理できます。 さらに、Docker を使用して、Windows Server コンテナー ネットワーキングを管理し、仮想マシンとだけでなくコンテナーとも SDN ポリシーを関連付けできます。 詳細については、「[ソフトウェア定義ネットワーク インフラストラクチャを計画する](../networking/sdn/plan/plan-a-software-defined-network-infrastructure.md)」を参照してください。

### <a name="tcp-performance-improvements"></a>TCP パフォーマンスの向上
既定の初期輻輳ウィンドウ (ICW) が 4 から 10 に増加し、TCP Fast Open (TFO) が実装されました。 TFO により TCP 接続の確立に必要な時間が短縮されるほか、ICW の増加により、初期バーストでさらに大きなオブジェクトを転送できるようになりました。 この組み合わせにより、クライアントとクラウドの間でインターネット オブジェクトを転送するのに必要な時間をさらに短くできます。

パケット損失から回復する際の TCP 動作を改善するために、TCP Tail Loss Probe (TLP) と Recent Acknowledgement (RACK) が実装されました。 TLP は、再転送タイムアウト (RTO) を高速回復に変換する際に役立ちます。また、RACK は高速回復の所要時間を短縮し、損失パケットを再転送します。 

## <a name="security-and-assurance"></a>[セキュリティおよび保証](../security/Security-and-Assurance.md)  
IT プロフェッショナルがデータ センターとクラウド環境に展開するためのセキュリティ ソリューションと機能が含まれます。 Windows Server 2016 でのセキュリティについては、「[セキュリティおよび保証](../security/Security-and-Assurance.md)」を参照してください。  

### <a name="just-enough-administration"></a>Just Enough Administration  
Windows Server 2016 の Just Enough Administration は、Windows PowerShell で管理可能なすべての対象について代理管理を実現するセキュリティ テクノロジです。 機能には、ネットワーク ID での実行、PowerShell ダイレクト経由での接続、JEA エンドポイントとの間での安全なファイル コピー、既定で JEA コンテキストで起動する PowerShell コンソールの構成のサポートが含まれます。 詳細については、[GitHub での JEA](https://aka.ms/JEA) に関する記事を参照してください。

### <a name="credential-guard"></a>Credential Guard
Credential Guard は、特権を持つシステム ソフトウェアだけがシークレットにアクセスできるように、仮想化ベースのセキュリティを使用してシークレットを分離します。 「[Credential Guard によるドメインの派生資格情報の保護](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)」を参照してください。

###  <a name="remote-credential-guard"></a>Remote Credential Guard
Credential Guard では RDP セッションがサポートされるため、ユーザーの資格情報はクライアント側に保持されたままで、サーバー側では公開されません。 また、リモート デスクトップにシングル サインオンも提供します。 「[Windows Defender Credential Guard によるドメインの派生資格情報の保護](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)」を参照してください。   

### <a name="device-guard-code-integrity"></a>Device Guard (コードの整合性)
Device Guard は、サーバーで実行できるコードを指定するポリシーを作成することで、カーネル モードのコードの整合性 (KMCI) とユーザー モードのコードの整合性 (UMCI) を提供します。 「[Windows Defender Device Guard の概要: 仮想化ベースのセキュリティとコードの整合性ポリシー](https://docs.microsoft.com/windows/device-security/device-guard/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)」を参照してください。


### <a name="windows-defender"></a>Windows Defender  
[Windows Server 2016 用 Windows Defender の概要](../security/windows-defender/windows-defender-overview-windows-server.md)。 Windows Server 2016 では既定で Windows Server Antimalware がインストールされ、有効になりますが、Windows Server Antimalware のユーザー インターフェイスはインストールされません。 ただし、ユーザー インターフェイスがなくても、Windows Server Antimalware により、マルウェア対策の定義が更新され、コンピューターが保護されます。 Windows Server Antimalware のユーザー インターフェイスが必要な場合は、オペレーティング システムのインストール後に役割と機能の削除ウィザードを使ってインストールできます。

### <a name="control-flow-guard"></a>制御フロー ガード
制御フロー ガード (CFG) は、メモリ破損の脆弱性に対処するために作成されたプラットフォームのセキュリティ機能です。 詳細については、「[Control Flow Guard (制御フロー ガード)](https://msdn.microsoft.com/library/windows/desktop/mt637065(v=vs.85).aspx)」を参照してください。


## <a name="storage"></a>[ストレージ](../storage/storage.yml)

Windows Server 2016 の記憶域には、ソフトウェアによる記憶域と従来のファイル サーバーに対する新機能と強化機能が含まれています。 新機能のいくつかを以下に示します。強化機能および詳細情報については、「[What's New in Storage in Windows Server 2016 (Windows Server 2016 の記憶域の新機能)](../storage/whats-new-in-storage.md)」を参照してください。

### <a name="storage-spaces-direct"></a>記憶域スペース ダイレクト

記憶域スペース ダイレクトでは、ローカル記憶域を持つサーバーを使用して高可用性を備えた拡張性の高い記憶域を作成できます。 ソフトウェア定義ストレージ システムの展開と管理を簡素化し、SATA SSD や NVMe ディスク デバイスなどの新しいクラスのディスク デバイスを使用できるようにします。これは、共有ディスクを使用したクラスター記憶域スペースによるこれまでの環境では実現できませんでした。

詳細については、[記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)に関する記事を参照してください。

### <a name="storage-replica"></a>記憶域レプリカ

記憶域レプリカでは、サイト間でフェールオーバー クラスターを拡大できるだけでなく、障害復旧用に、サーバー間またはクラスター間で記憶域にとらわれずにブロックレベルで同期レプリケーションを行うことができます。 同期レプリケーションは、クラッシュ前後の整合性が維持されるボリュームを使用した物理サイト内のデータのミラーリングを実現して、ファイル システム レベルでデータがまったく失われないようにします。 非同期レプリケーションでは、データが失われる可能性はありますが、大都市圏の範囲を超えてサイトを拡張できます。

詳細については、[記憶域レプリカ](../storage/storage-replica/storage-replica-overview.md)に関する記事を参照してください。

### <a name="storage-quality-of-service-qos"></a>記憶域のサービスの品質 (QoS)

記憶域のサービスの品質 (QoS) を使用して、Windows Server 2016 でエンド ツー エンドの記憶域のパフォーマンスを一元的に監視すると共に、Hyper-V クラスターと CSV クラスターを使用してポリシーを作成できるようになりました。

詳細については、「[記憶域のサービスの品質](../storage/storage-qos/storage-qos-overview.md)」を参照してください。

## <a name="failover-clustering"></a>[フェールオーバー クラスタリング](../failover-clustering/whats-new-in-failover-clustering.md)

Windows Server 2016 には、フェールオーバー クラスタリング機能を使用して 1 つのフォールト トレラント クラスターにグループ化される、複数のサーバーに対する新機能と強化機能が多数用意されています。 追加機能のいくつかを以下に紹介します。詳細については、「[What's New in Failover Clustering in Windows Server 2016 (Windows Server 2016 のフェールオーバー クラスタリングの新機能)](../failover-clustering/whats-new-in-failover-clustering.md)」を参照してください。

### <a name="cluster-operating-system-rolling-upgrade"></a>Cluster Operating System Rolling Upgrade (クラスター オペレーティング システムのローリング アップグレード)

クラスター オペレーティング システムのローリング アップグレードを使用すると、管理者は、Hyper-V またはスケールアウト ファイル サーバーのワークロードを停止することなく、クラスター ノードのオペレーティング システムを Windows Server 2012 R2 から Windows Server 2016 にアップグレードできます。 この機能を使用すると、サービス レベル アグリーメント (SLA) でのダウンタイムに対するペナルティを回避できます。

詳細については、「[Cluster Operating System Rolling Upgrade (クラスター オペレーティング システムのローリング アップグレード)](../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)」を参照してください。

### <a name="cloud-witness"></a>クラウド監視

クラウド監視は、Windows Server 2016 の新しい種類のフェールオーバー クラスター クォーラム監視で、Microsoft Azure が判別ポイントとして利用されます。 クラウド監視は、他のクォーラム監視と同様、票を集めるため、クォーラム計算に参加できます。 クラウド監視をクォーラム監視として構成するには、クラスター クォーラムの構成ウィザードを使用します。

詳細については、[クラウド監視の展開](../failover-clustering/deploy-cloud-witness.md)に関する記事を参照してください。

### <a name="health-service"></a>ヘルスサービス

ヘルスサービスにより、記憶域スペース ダイレクト クラスターのクラスター リソースにおける日常的な監視、操作、メンテナンスのエクスペリエンスが向上します。

詳細については、[ヘルス サービス](../failover-clustering/health-service-overview.md)に関する記事を参照してください。

## <a name="application-development"></a>アプリケーションの開発

### <a name="internet-information-services-iis-100"></a>インターネット インフォメーション サービス (IIS) 10.0
Windows Server 2016 の IIS 10.0 Web サーバーにより提供される新機能は以下のとおりです。

- ネットワーク スタックでの HTTP/2 プロトコルのサポート。IIS 10.0 と統合されたため、IIS 10.0 Web サイトはサポートされる構成の HTTP/2 要求を自動的に処理できるようになりました。 これにより、接続の効率的な再利用、待機時間の短縮など、多くの機能強化が HTTP/1.1 に加えられ、Web ページの読み込み時間が短縮されます。 
- Nano Server での IIS 10.0 の実行および管理機能。 「[Nano Server の IIS](iis-on-nano-server.md)」を参照してください。
- ワイルドカード ホスト ヘッダーのサポート。管理者は、ドメイン向けに Web サーバーをセットアップし、Web サーバーが任意のサブドメインの要求を処理するように設定できます。
- IIS を管理するための新しい PowerShell モジュール (IISAdministration)。 

詳細については、「[IIS](https://iis.net/learn)」を参照してください。

### <a name="distributed-transaction-coordinator-msdtc"></a>分散トランザクション コーディネーター (MSDTC)
Microsoft Windows 10 と Windows Server 2016 に 3 つの新機能が追加されました。

- Resource Manager Rejoin の新しいインターフェイスは、データベースがエラーのために再起動された後に未確定トランザクションの結果を調べるために、リソース マネージャーによって使されます。 詳細については、「[IResourceManagerRejoinable::Rejoin](https://msdn.microsoft.com/library/mt203799(v=vs.85).aspx)」を参照してください。

- DSN 名の制限が 256 バイトから 3072 バイトに拡張されました。 詳細については、「[IDtcToXaHelperFactory::Create](https://msdn.microsoft.com/library/ms686861(v=vs.85).aspx)」、「[IDtcToXaHelperSinglePipe::XARMCreate](https://msdn.microsoft.com/library/ms679248(v=vs.85).aspx)」、または「[IDtcToXaMapper::RequestNewResourceManager](https://msdn.microsoft.com/library/ms680310(v=vs.85).aspx)」を参照してください。

- トレースが機能強化され、トレース ログ ファイル名にイメージ ファイルのパスが含まれるようにレジストリ キーを設定して、確認するトレース ログ ファイルを指定できるようになりました。 MSDTC のトレースの構成に関する詳細については、「[Windows ベースのコンピューター上の MS DTC の診断トレースを有効にする方法 ](https://support.microsoft.com/kb/926099)」を参照してください。



## <a name="see-also"></a>参照  
-   [リリース ノート:Windows Server 2016 に関する重要な問題](Windows-Server-2016-GA-Release-Notes.md)  
