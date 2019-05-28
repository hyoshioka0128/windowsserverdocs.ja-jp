---
title: Windows Server バージョンが 1903 では新機能
description: このトピックでは、半期チャネル リリースである Windows Server バージョンが 1903 年の新機能について説明します。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.openlocfilehash: 2aa84df1ca162cb6e2dfa580b4b0744ff08cc95a
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983442"
---
# <a name="whats-new-in-windows-server-version-1903"></a>新機能については、Windows Server バージョンが 1903

>適用対象:Windows Server (半期チャネル)

このトピックでは、半期チャネル リリースである Windows Server バージョンが 1903 年の新機能について説明します。 これらの機能を実行していると、コンテナー、Server Core インストールで作業を行うのためのツールおよび Linux のデバイスから記憶域を移行する機能を管理するための機能強化が含まれます。

代わりに Windows Server の最新の長期的なサービス チャネル (LTSC) リリースの新機能についてを参照してくださいを参照してください[で Windows Server 2019 新](../get-started-19/whats-new-19.md)します。 参照してください[新機能については、Windows 10 IT Pro コンテンツのバージョンが 1903](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1903)します。

このリリースのシステム要件は同じ Windows Server 2019 です — を参照してください[システム要件](../get-started-19/sys-reqs-19.md)の詳細。 最近削除された内容を表示するには、次を参照してください[Features Removed or 以降では、Windows Server バージョンが 1903 交換の計画。](../get-started-19/removed-features-1903.md)

> [!NOTE]
> Windows コンテナーは、ホスト サーバーと同じバージョンの Windows を使用する必要がありますまたは*以前*バージョン。 たとえば、リリースされたバージョンの Windows Server を実行しているホスト サーバー、バージョン 1903 (18342 をビルドする) ことができます、同じまたはそれ以前のバージョンで Windows Server コンテナーを実行し、(コンテナーでは、Windows の Insider Preview バージョンで使用) 場合でも、ビルド番号。 詳細については、次を参照してください。 [Windows コンテナーのバージョンの互換性](https://docs.microsoft.com/virtualization/windowscontainers/deploy-containers/version-compatibility)します。

## <a name="enhanced-support-for-non-microsoft-container-services"></a>Microsoft 以外のコンテナー サービスのサポートの強化

Azure container services と Microsoft 以外のコンテナー サービスをサポートするためのプラットフォーム機能を拡張します。

- ホスト コンピューティング サービス (HCS) の Windows (LCOW) Azure で Windows コンテナーと Linux コンテナーのポッドをサポートするために、CRI containerd を統合しました。
- Windows コンテナーのサポートを有効にする Kubernetes コミュニティと連携しています。 Kubernetes v1.14 のリリースでは、Windows サーバー ノードのサポートを安定したベータ版から正式に就職しました。 詳細については、次を参照してください。 [Kubernetes で現在サポートされている Windows コンテナー](https://cloudblogs.microsoft.com/opensource/2019/03/25/windows-server-containers-now-supported-kubernetes/)します。
- Windows の Tigera Calico Tigera Essentials サブスクリプションの一部とプランの両方として一般提供が間で相互運用可能な非オーバーレイ ネットワークおよびネットワーク ポリシーは、Linux と Windows 環境を混合します。
- オーバーレイ ネットワークを Windows コンテナーでは、Flannel と Kubernetes v1.14 の最新リリースを通して Kubernetes との統合などのサポートの向上、スケーラビリティの向上を配信しました。 詳細については、次を参照してください。 [Kubernetes での Windows のサポートの概要](https://kubernetes.io/docs/setup/windows/)します。

## <a name="directx-hardware-acceleration-in-containers"></a>コンテナーでの DirectX ハードウェア高速化

ローカルのグラフィカル処理ユニット (GPU) ハードウェアを使用して Machine Learning (ML) の推論など Windows コンテナーの tp のサポートのシナリオでは、DirectX Api のハードウェア アクセラレータのサポートを有効にしています。 詳細については、次を参照してください。 [Windows コンテナーに取り込む GPU アクセラレーション](https://techcommunity.microsoft.com/t5/Containers/Bringing-GPU-acceleration-to-Windows-containers/ba-p/393939)します。

## <a name="updated-container-identity-and-group-managed-service-account-documentation"></a>更新されたコンテナーの id とグループ管理サービス アカウントのドキュメント

例および詳細な互換性情報を追加しました、[グループ管理サービス アカウント](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/manage-serviceaccounts)ドキュメントについては、行われると、[資格情報の仕様の PowerShell モジュール](https://www.powershellgallery.com/packages/CredentialSpec)PowerShell ギャラリーで利用可能です。 詳細については、次を参照してください。、[コンテナーの id の新](https://techcommunity.microsoft.com/t5/Containers/What-s-new-for-container-identity/ba-p/389151)ブログの投稿。

## <a name="add-task-scheduler-and-hyper-v-manager-to-server-core-installations"></a>Server Core インストールにタスク スケジューラと、HYPER-V マネージャーを追加します。

ご存知のように、Windows Server、運用環境で半期チャネルを使用する場合に、Server Core インストール オプションを使用してをお勧めします。 ただし、既定では、Server Core は、多数の便利な管理ツールを省略します。 最も一般的に使われるツール、アプリケーションの互換性機能をインストールすることで、まだがあった一部不足しているツールを追加することです。

このバージョンのアプリケーションの互換性機能を他の 2 つのツールはそのためで追加するお客様からのフィードバックに基づき、しました。タスク スケジューラ (taskschd.msc) と Hyper V マネージャー (virtmgmt.msc)。

詳細については、次を参照してください。 [Server Core アプリの互換性機能](../get-started-19/install-fod-19.md)します。

## <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>記憶域の移行サービスはローカル アカウント、クラスター、および Linux サーバーを移行します。

記憶域の移行サービスでは、Windows Server の新しいバージョンにサーバーを移行するやすくなります。 サーバー上のデータのインベントリを作成し、新しいサーバーにデータと構成を転送するためのグラフィカル ツールを提供します-アプリやユーザーが何も変更することがなく。

このバージョンの Windows Server を使用して、移行を調整する、次の機能が追加されました。

- 新しいサーバーにローカル ユーザーとグループを移行します。
- フェールオーバー クラスターから記憶域を移行します。
- Samba を使用する Linux サーバーから記憶域を移行します。
- Azure File Sync を使用して Azure に移行された共有をより簡単に同期します。
- Azure などの新しいネットワークへの移行します。

記憶域の移行サービスに関する詳細については、次を参照してください。[記憶域の移行サービスの概要](../storage/storage-migration-service/overview.md)します。

## <a name="system-insights-disk-anomaly-detection"></a>システム Insights ディスク異常検出

[システム Insights](../manage/system-insights/overview.md)予測分析機能をローカルで Windows Server システム データを分析し、サーバーの機能に関する洞察を提供します。 さまざまな組み込みの機能が付属しますが、ディスクの異常検出以降 Windows Admin Center を使用して追加の機能をインストールする機能が追加されました。

異常検出のディスクはディスクが動作しているときに強調表示する新機能*異なる*通常よりもします。 異なるは必ずしも中には、システム上の問題のトラブルシューティングを行うこれらの異常な瞬間を表示、悪いが役に立ちます。

この機能も Windows Server 2019 を実行しているサーバーを使用できます。

## <a name="windows-admin-center-enhancements"></a>Windows Admin Center の機能強化

Windows Admin Center の新しいリリースは、Windows Server に新しい機能を追加します。 最新の機能については、次を参照してください。 [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)します。

## <a name="security-baseline-for-windows-10-and-windows-server"></a>Windows 10 および Windows Server 用のセキュリティ ベースライン

ドラフト リリースの[セキュリティ構成ベースライン設定](https://blogs.technet.microsoft.com/secguide/2019/04/24/security-baseline-draft-for-windows-10-v1903-and-windows-server-v1903/)1903 のバージョンが使用可能なバージョンが 1903 年の Windows 10 および Windows Server。

## <a name="setupdiag"></a>SetupDiag
[SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag)バージョン 1.4.1 を利用できます。

SetupDiag は、Windows 更新プログラムが失敗した理由を診断するのに役立つコマンド ライン ツールです。 SetupDiag は、Windows セットアップのログ ファイルを検索することで動作します。 ログ ファイルを検索する際に、SetupDiag は一連のルールを使用して既知の問題と照合します。 SetupDiag rules.xml ファイルに含まれる 53 の規則の現在のバージョンで SetupDiag の実行時に抽出されます。 rules.xml ファイルは、SetupDiag の新しいバージョンが提供されるときに更新されます。

## <a name="update-rollback-improvements"></a>更新のロールバックの機能強化

サーバーできるようになりました自動的にスタートアップして障害から復旧起動時の障害は、最新のドライバーまたは品質更新プログラムのインストール後に導入された場合は、更新プログラムを削除します。 デバイスは、正常なドライバーの更新プログラムの品質の最新のインストール後に起動することが、Windows 自動的にアンインストールされますバックアップ デバイスを取得する更新プログラムと正常に動作しています。

この機能を Server Core インストール オプションを使用するサーバーで要求されて、 [Windows 回復環境](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)パーティション。

## <a name="microsoft-defender-advanced-threat-protection-atp-improvements"></a>Microsoft Defender Advanced Threat Protection (ATP) の機能強化

Windows Server に Microsoft Defender 高度なスレッドの保護が含まれています (詳細については、次を参照してください。 [Windows Server 上で Windows Defender ウイルス対策](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-on-windows-server-2016))。 このリリースには、次の機能強化が含まれています。

- [攻撃対象領域の削減](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/overview-attack-surface-reduction)– IT 管理者が構成できるデバイスを定義できるようにする高度な web の保護を許可リストと拒否の特定の URL と IP アドレスします。
- [次世代の保護](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-antivirus/windows-defender-antivirus-in-windows-10)– コントロールは、ランサムウェア、資格情報の不正使用、およびリムーバブル記憶域経由で転送される攻撃から保護に拡張されています。
    - 整合性の強制機能 – リモート ランタイムの構成証明を有効にします。
    - 改ざんから機能を – OS と攻撃者から ATP の重要なセキュリティ機能を分離する仮想化ベースのセキュリティを使用します。
- Microsoft Defender ATP の次世代の保護テクノロジ:
    - **Machine learning の advanced**:高度な機械学習と AI モデルを有効にすると、革新的な脆弱性の悪用手法、ツール、およびマルウェアを使用して頂点攻撃者に対して保護を強化されました。
    - **緊急の大量感染保護**:新しい大量感染が検出された場合に、新しいインテリジェンスでデバイスを更新に自動的には緊急の大量感染の保護を提供します。
    - **ISO 27001 の認定コンプライアンス**:により、脅威、脆弱性および影響によっては、クラウド サービスが分析して、リスク管理とセキュリティ制御が行われます。
    - **地理的位置情報サポート**:位置情報や構成可能な保持ポリシーと同様にサンプル データの主権をサポートします。