---
title: Azure ディザスター リカバリーを使用して RDS のディザスター リカバリーを設定する
description: RDS 展開のディザスター リカバリーに Azure ディザスター リカバリーを使用する方法について説明する
ms.author: elizapo
ms.date: 06/12/2017
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 6c0e9b97a436f51babf679d6ce0aa67c09bcfe26
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936907"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Azure Site Recovery を使用して RDS のディザスター リカバリーを設定する

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

Azure Site Recovery を使用して、リモート デスクトップ サービス展開のディザスター リカバリー ソリューションを作成することができます。

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) は仮想マシンのレプリケーション、フェールオーバー、および回復を組み合わせてディザスター リカバリー機能を提供する Azure ベースのサービスです。 Azure Site Recovery では、仮想マシンおよびアプリケーションを一貫してレプリケート、保護、プライベート/パブリック クラウドまたはホスト側のクラウドへシームレスにフェールオーバーするため、多数のレプリケーション テクノロジをサポートしています。

ディザスター リカバリー ソリューションを作成し検証するには、次の情報を使用します。

## <a name="disaster-recovery-deployment-options"></a>ディザスター リカバリーの展開オプション

物理サーバーにも、Hyper-V または VMWare を実行している仮想マシンにも RDS を展開できます。 Azure Site Recovery は、オンプレミスと仮想の両方の展開をセカンダリ サイトか Azure のどちらにでも保護できます。 次の表では、サイト間とサイトと Azure 間のディザスター リカバリー シナリオで、サポートされるさまざまな RDS 展開を示します。

| 展開の種類                          | Hyper-V サイト間 | Hyper-V サイトと Azure 間 | VMWare サイトと Azure 間 | 物理サイトと Azure 間 |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| プールされた仮想デスクトップ (管理対象外)       |はい|いいえ|いいえ|いいえ |
| プールされた仮想デスクトップ (管理対象、UPD なし) | はい|いいえ|いいえ|いいえ|
| RemoteApp とデスクトップ セッション (UPD なし) | はい|はい|はい|はい  |

## <a name="prerequisites"></a>前提条件

お使いの展開に合わせて Azure Site Recovery を構成するには、その前に次の要件を満たしていることを確認します。

- [オンプレミスの RDS 展開](rds-deploy-infrastructure.md)を作成します。
- [Azure Site Recovery Services コンテナー](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault)を Microsoft Azure サブスクリプションに追加します。
- 回復サイトとして Azure を使用する場合は、VM 上で [Azure 仮想マシン準備状況評価ツール](https://azure.microsoft.com/downloads/vm-readiness-assessment/)を実行して、Azure VM および Azure Site Recovery Services と互換性のあることを確認します。

## <a name="implementation-checklist"></a>実装のチェックリスト

RDS 展開に対して Azure Site Recovery Services を有効にするさまざまな手順を詳しく取り上げますが、ここでは高レベルの実装手順を示します。

| **手順 1 - ディザスター リカバリー用に VM を構成する**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hyper-V - Microsoft Azure Site Recovery プロバイダーをダウンロードします。 これを VMM サーバーまたは Hyper-V ホストにインストールします。 詳細については、[Azure Site Recovery を使用した Azure へのレプリケーションの前提条件](/azure/site-recovery/site-recovery-prereq)に関するページを参照してください。                                                                                                                             |
| VMWare - 保護サーバー、構成サーバー、およびマスター ターゲット サーバーを構成します                                                                                                                                                      |
| **手順 2 - リソースの準備する**                                                                                                                                                                                                           |
| [Azure ストレージ アカウント](/azure/storage/storage-create-storage-account)を追加します。                                                                                                                                                                                                              |
| Hyper-V - Microsoft Azure Recovery Services エージェントをダウンロードして、Hyper-V ホスト サーバーにインストールします。                                                                                                                                     |
| VMWare - すべての VM にモビリティ サービスがインストールされていることを確認します。                                                                                                                                                                           |
| [VMM クラウド、Hyper-V サイト、または VMWare サイトで VM の保護を有効にします](rds-enable-dr-with-asr.md)。                                                                                                                                                                    |
| **手順 3 - 復旧計画を設計する。**                                                                                                                                                                                                        |
| リソースのマップ - Azure VNET にオンプレミス ネットワークをマップします。                                                                                                                                                                              |
| [復旧計画を作成します](rds-disaster-recovery-plan.md)。 |
| テスト フェールオーバーを作成して、復旧計画をテストします。 すべての VM が Active Directory などの必要なリソースにアクセスできることを確認します。 ネットワーク リダイレクトが構成され、RDS 用に機能していることを確認します。 復旧計画のテストの詳細な手順については、「[テスト フェールオーバーを実行する](/azure/site-recovery/site-recovery-test-failover-to-azure)」を参照してください|
| **手順 4 - ディザスター リカバリーの演習を実行する。**                                                                                                                                                                                                     |
| 計画されたフェールオーバーと計画外のフェールオーバーを使用してディザスター リカバリーの演習を実行します。 すべての VM が、Active Directory などの必要なリソースにアクセスできることを確認します。 すべての VM が、Active Directory などの必要なリソースにアクセスできることを確認します。 フェールオーバーの詳細な手順と演習の実行方法については、[Site Recovery でのフェールオーバー](/azure/site-recovery/site-recovery-failover)に関するページを参照してください。|


