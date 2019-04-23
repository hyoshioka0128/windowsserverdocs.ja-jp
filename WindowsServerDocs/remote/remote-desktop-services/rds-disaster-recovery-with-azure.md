---
title: Azure のディザスター リカバリーを使用して RDS のディザスター リカバリーを設定します。
description: RDS のデプロイのディザスター リカバリーに Azure のディザスター リカバリーを使用する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 06/12/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 561a515e23d12cc3397c40fd885550e735ed4d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878173"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Azure Site Recovery を使用して RDS のディザスター リカバリーを設定します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

Azure Site Recovery を使用して、リモート デスクトップ サービス展開のディザスター リカバリー ソリューションを作成することができます。 

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview)はレプリケーション、フェールオーバー、および仮想マシンの回復を調整することでディザスター リカバリー機能を提供する Azure ベースのサービスです。 Azure Site Recovery では、さまざまな一貫したレプリケート、保護、レプリケーション テクノロジとシームレスにフェールオーバー仮想マシンとプライベート/パブリック クラウドまたはホスト側のクラウドへのアプリケーションをサポートします。 

作成し、ディザスター リカバリーのソリューションを検証するには、次の情報を使用します。

## <a name="disaster-recovery-deployment-options"></a>障害復旧デプロイ オプション

物理サーバーまたは HYPER-V または VMWare を実行する仮想マシンのいずれかで RDS をデプロイできます。 Azure Site Recovery には、オンプレミスと仮想の展開をセカンダリ サイトのいずれかまたは Azure の両方を保護できます。 次の表では、サイト対サイトおよびサイトと Azure の災害 recvoery シナリオでは、さまざまなサポート RDS のデプロイを示します。

| 展開の種類                          | HYPER-V サイト対サイト | HYPER-V サイトから Azure | VMWare から Azure へのサイト | 物理サイト-Azure |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| プールされた仮想デスクトップが (アンマネージ)       |〇|X|いいえ|いいえ |
| プールされた仮想デスクトップ (管理対象、UPD なし) | 〇|X|いいえ|X|
| Remoteapp とデスクトップのセッション (UPD なし) | 〇|〇|〇|〇  |

## <a name="prerequisites"></a>前提条件

Azure Site Recovery を構成するには、展開に、前に、次の要件を満たしていることを確認します。

- 作成、 [、オンプレミスでの RDS デプロイ](rds-deploy-infrastructure.md)します。
- 追加[Azure Site Recovery Services コンテナー](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault) Microsoft Azure サブスクリプションにします。
- 復旧サイトとして Azure を使用する場合は、実行、 [Azure 仮想マシン準備状況評価ツール](https://azure.microsoft.com/downloads/vm-readiness-assessment/)で Vm を Azure Vm と Azure Site Recovery Services と互換性があることを確認します。
 
## <a name="implementation-checklist"></a>実装のチェックリスト

詳細についてで RDS デプロイ用の Azure Site Recovery Services を有効にするさまざまな手順について説明しますが、高レベルの実装手順を示します。

| **手順 1 - Vm のディザスター リカバリーの構成**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hyper-V の Microsoft Azure Site Recovery Provider をダウンロードします。 VMM サーバーまたは HYPER-V ホストにインストールします。 参照してください[Azure Site Recovery を使用して Azure へのレプリケーションの前提条件](/azure/site-recovery/site-recovery-prereq)について。                                                                                                                             |
| VMWare の保護サーバー、構成サーバーとマスター ターゲット サーバーを構成します。                                                                                                                                                      |
| **手順 2 - リソースの準備**                                                                                                                                                                                                           |
| 追加、 [Azure Storage アカウント](/azure/storage/storage-create-storage-account)します。                                                                                                                                                                                                              |
| HYPER-V - は、Microsoft Azure Recovery Services エージェントをダウンロードして、HYPER-V ホスト サーバーにインストールします。                                                                                                                                     |
| VMWare - すべての Vm にモビリティ サービスがインストールされていることを確認します。                                                                                                                                                                           |
| [VMM クラウドで HYPER-V サイト、または VMWare サイトで Vm の保護を有効にする](rds-enable-dr-with-asr.md)します。                                                                                                                                                                    |
| **手順 3 - 復旧計画を設計します。**                                                                                                                                                                                                        |
| リソース - Azure Vnet にオンプレミス ネットワークのマップをマップします。                                                                                                                                                                              |
| [復旧計画の作成](rds-disaster-recovery-plan.md)です。 |
| テスト フェールオーバーを作成して、復旧計画をテストします。 すべての Vm が Active Directory などの必要なリソースにアクセスできることを確認します。 リダイレクトが構成されているネットワークおよび rds. に勤務していることを確認します。 復旧計画のテストに詳細な手順についてを参照してください[テスト フェールオーバーの実行。](/azure/site-recovery/site-recovery-test-failover-to-azure)|
| **手順 4 - ディザスター リカバリーの訓練を実行します。**                                                                                                                                                                                                     |
| 計画フェールオーバーや計画外フェールオーバーを使用してディザスター リカバリーの訓練を実行します。 すべての Vm の Active Directory などの必要なリソースにアクセスできるようにします。 すべての Vm の Active Directory などの必要なリソースにアクセスできるようにします。 フェールオーバーとドリルを実行する方法の詳細な手順は、次を参照してください。 [Site Recovery でフェールオーバー](/azure/site-recovery/site-recovery-failover)します。|


