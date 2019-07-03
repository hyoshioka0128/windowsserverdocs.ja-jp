---
title: Windows Server バージョン 1903 の新機能
description: このトピックでは、半期チャネル リリースである Windows Server バージョン 1903 の一部の新機能について説明します。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: 0ec6a7ec624818b92fb306089f3dea3c786c0827
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280316"
---
# <a name="whats-new-in-windows-server-version-1903"></a>Windows Server バージョン 1903 の新機能

>適用対象:Windows Server (半期チャネル)

このトピックでは、半期チャネル リリースである Windows Server バージョン 1903 の一部の新機能について説明します。 それらの機能には、コンテナーを実行および管理する拡張機能、コア インストールで作業を行うためのツールおよび Linux デバイスから記憶域を移行する機能が含まれます。

代わりに Windows Server の長期サービス チャネル (LTSC) リリースの新機能について調べるには、「[Windows Server 2019 の新機能](../get-started-19/whats-new-19.md)」を参照してください。 [Windows 10 バージョン 1903 の IT 技術者向けコンテンツの新機能](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903)に関するページも参照してください。

このリリースのシステム要件は、Windows Server 2019 と同じです。詳細については、[システム要件](../get-started-19/sys-reqs-19.md)を参照してください。 最近削除された機能については、[Windows Server バージョン 1903 以降で削除された機能および置換が計画されている機能](../get-started-19/removed-features-1903.md)に関するページを参照してください。

> [!NOTE]
> Windows コンテナーでは、ホスト サーバーと同じ Windows バージョン、または*以前の*バージョンを使用する必要があります。 たとえば、Windows Server バージョン 1903 (ビルド 18342) のリリース済みのバージョンを実行しているホスト サーバーは、(コンテナーで Windows の Insider Preview バージョンを使用している場合でも) 同じまたは以前のバージョンとビルド番号の Windows Server コンテナーを実行できます。 詳細については、[Windows コンテナーのバージョンの互換性](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility)に関するページを参照してください。

## <a name="enhanced-support-for-non-microsoft-container-services"></a>Microsoft 以外のコンテナー サービスのサポートの強化

プラットフォーム機能が強化され、Azure コンテナー サービスと Microsoft 以外のコンテナー サービスがサポートされるようになりました。

- CRI-containerd をホスト コンピューティング サービス (HCS) に統合したことにより、Azure の Windows コンテナーのポッドおよび Windows 上の Linux コンテナー (LCOW) がサポートされるようになりました。
- Kubernetes のコミュニティと共同作業を行い、Windows コンテナーがサポートされるようになりました。 Kubernetes v1.14 のリリースでは、Windows Server ノードのサポートがベータから安定に正式に変わりました。 詳細については、[Kubernetes で現在サポートされている Windows コンテナー](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/)を参照してください。
- 現在、Tigera Essentials サブスクリプションの一部として Windows 向けの Tigera Calico が一般提供されています。これでは、非オーバーレイ ネットワークおよび Linux や Windows が混在する環境でのネットワーク ポリシーの相互運用が可能です。
- Microsoft では、Flannel と Kubernetes v1.14 の最新のリリースを使用した Kubernetes との統合を含む、Windows コンテナーのオーバーレイ ネットワーク サポートを強化するスケーラビリティの向上を実現しました。 詳細については、[Kubernetes での Windows のサポートの概要](https://kubernetes.io/docs/setup/windows/)に関するページを参照してください。

## <a name="directx-hardware-acceleration-in-containers"></a>コンテナーでの DirectX ハードウェア アクセラレータ

ローカルの GPU (グラフィックス プロセッシング ユニット) ハードウェアを使用した機械学習 (ML) での推定などのシナリオをサポートするために、Windows コンテナーで DirectX の API のハードウェア アクセラレータがサポートされるようになりました。 詳細については、[Windows コンテナーへの GPU アクセラレータの導入](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939)に関するページを参照してください。

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>コンテナー ID とグループ管理サービス アカウント ドキュメントの更新

[グループ管理サービス アカウント](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts)のドキュメントにさらに例と互換性に関する情報が追加され、PowerShell ギャラリーで [Credential Spec PowerShell モジュール](https://www.powershellgallery.com/packages/CredentialSpec)が使用できるようになりました。 詳細については、[コンテナー ID の新機能](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151)に関するブログ投稿を参照してください。

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>コア インストールへのタスク スケジューラと Hyper-V マネージャーの追加

ご存じのとおり、運用環境で Windows Server の半期チャンネルを使用する場合、コア インストール オプションの使用をお勧めしています。 ただし、Server Core では多数の便利な管理ツールが既定で省かれています。 アプリ互換性機能をインストールすると、最もよく使用されているツールが多数追加されますが、それでもそこにはないツールがいくつかあります。

したがって、お客様のフィードバックに基づき、このバージョンではアプリ互換性機能にさらに 2 つツールを追加しています。タスク スケジューラ (taskschd.msc) と Hyper-V マネージャー (virtmgmt.msc) です。

詳細については、[Server Core アプリ互換性機能](../get-started-19/install-fod-19.md)に関するページを参照してください。

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>ストレージ移行サービスでローカル アカウント、クラスターおよび Linux サーバーの移行が可能

ストレージ移行サービスでは、Windows Server の新しいバージョンにサーバーを簡単に移行できます。 これには、アプリやユーザーが何も変更を行わずに、サーバー上のデータのインベントリを作成し、そのデータと構成が新しいサーバーに転送されるグラフィカル ツールがあります。

移行の調整にこのバージョンの Windows Server を使用するときのために、次の機能が追加されています。

- 新しいサーバーへのローカル ユーザーとローカル グループの移行
- フェールオーバー クラスターからの記憶域の移行
- Samba を使用する Linux サーバーからの記憶域の移行
- Azure File Sync を使用した Azure へ移行された共有のより簡単な同期
- Azure などの新しいネットワークへの移行

記憶域移行サービスの詳細については、「[ストレージ移行サービスの概要](../storage/storage-migration-service/overview.md)」を参照してください。

## <a name="system-insights-disk-anomaly-detection"></a>システム インサイトでのディスク異常の検出

[システム インサイト](../manage/system-insights/overview.md)は、ローカルで Windows Server のシステム データを分析し、サーバーの機能の分析情報を提供する予測分析機能です。 これには多数の機能が組み込まれていますが、ディスク異常の検出を初めとする追加機能を Windows Admin Center を使用してインストールできるようになりました。

ディスク異常の検出は、ディスクが通常とは*異なる*動作をしたとき、それを浮き彫りにする新機能です。 異なるということが必ずしも悪いということではありませんが、これらの異常な瞬間を確認することによって、お使いのシステムの問題の解決に役立つことがあります。

この機能は、Windows Server 2019 を実行するサーバーでも利用できます。

## <a name="windows-admin-center-enhancements"></a>Windows Admin Center の機能強化

Windows Admin Center の新しいリリースがリリースされ、Windows Server に新機能が追加されました。 最新の機能の詳細については、[Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)に関するページを参照してください。

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Windows 10 および Windows Server のセキュリティ ベースライン

Windows 10 バージョン 1903 および Windows Server バージョン 1903 用の[セキュリティ ベースラインの構成設定](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/)のドラフト リリースが利用可能になりました。

## <a name="setupdiag"></a>SetupDiag
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) バージョン 1.4.1 が利用可能になりました。

SetupDiag は、Windows の更新が失敗した理由の診断に役立つコマンド ライン ツールです。 SetupDiag は、Windows セットアップのログ ファイルを検索することで動作します。 ログ ファイルを検索する際に、SetupDiag は一連のルールを使用して既知の問題と照合します。 現在のバージョンの SetupDiag には、rules.xml ファイルに 53 のルールが含まれており、SetupDiag の実行時に抽出されます。 rules.xml ファイルは、SetupDiag の新しいバージョンが提供されるときに更新されます。

## <a name="update-rollback-improvements"></a>更新プログラムのロールバックの機能強化

最近ドライバーや品質更新プログラムをインストールしたため起動に失敗するようになった場合、更新プログラムを削除することにより、起動の障害からサーバーを自動的に復旧できるようになりました。 品質更新プログラムまたはドライバーの更新プログラムを最近インストールしたことにより、デバイスを正常に起動できなくなった場合、Windows が更新プログラムを自動的にアンインストールして、デバイスの動作を正常に戻します。

この機能では、サーバーは [Windows 回復環境](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)パーティションでコア インストール オプションを使用している必要があります。

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Microsoft Defender Advanced Threat Protection (ATP) の機能強化

Windows Server には Microsoft Defender Advanced Thread Protection (詳細は、[Windows Server での Windows Defender ウイルス対策](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016)に関するページを参照) が含まれています。 このリリースには、次の機能強化があります。

- [攻撃範囲の縮小](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction): IT 管理者は、高度な Web 保護機能でデバイスを構成し、特定の URL や IP アドレスに対して許可および拒否リストを定義できます。
- [次世代の保護](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10): ランサムウェアからの保護、資格情報の誤用、リムーバブル記憶域からの攻撃も制御できるように強化されています。
    - 整合性の強制機能: リモート ランタイム構成証明を有効にします。
    - 改ざん防止機能: OS と攻撃者から重要な ATP セキュリティ機能を分離する仮想化ベースのセキュリティを使用しています。
- Microsoft Defender ATP の次世代の保護テクノロジ:
    - **高度な機械学習モデル**:高度な機械学習および AI モデルに強化されたことにより、脆弱性を悪用する革新的な手法、ツール、マルウェアを使用する Apex 攻撃者から保護できます。
    - **緊急の大量感染保護**:新しい大量感染が検出されると、新しいインテリジェンスでデバイスが自動的に更新され、緊急の大量感染から保護されます。
    - **ISO 27001 準拠の認定**:クラウド サービスを分析して脅威、脆弱性、影響を特定し、リスク管理およびセキュリティ制御が行われるようにします。
    - **位置情報のサポート**:サンプル データの位置情報、データ主権、構成可能なアイテム保持ポリシーがサポートされました。