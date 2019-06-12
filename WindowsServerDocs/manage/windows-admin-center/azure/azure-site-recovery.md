---
title: Azure Site Recovery と Windows Admin Center で HYPER-V 仮想マシンの保護します。
description: Windows Admin Center (Project Honolulu) を使用して Azure Site Recovery で Hyper-V VM を保護します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 66e9b2e23a60d1e4725321e88fc1ac262b9c31fa
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445927"
---
# <a name="protect-your-hyper-v-virtual-machines-with-azure-site-recovery-and-windows-admin-center"></a>Azure Site Recovery と Windows Admin Center で HYPER-V 仮想マシンの保護します。

>適用先:Windows Admin Center Preview、Windows Admin Center

[Azure Windows Admin Center との統合について説明します。](../plan/azure-integration-options.md)

Windows Admin Center を使用すると、仮想マシンを Hyper-V サーバーまたはクラスターにレプリケートするプロセスが合理化され、独自のデータセンターから Azure の機能を簡単に利用できます。 セットアップを自動化するには、Windows Admin Center ゲートウェイを Azure に接続できます。

以下の情報を参考にして、レプリケーション設定を構成し、Azure portal 内から回復の計画を作成します。これにより、Windows Admin Center が VM レプリケーションを開始して VM を保護できるようになります。

## <a name="what-is-azure-site-recovery-and-how-does-it-work-with-windows-admin-center"></a>Azure Site Recovery の概要と Windows Admin Center との連携のしくみ 

**Azure Site Recovery** は、ビジネスに不可欠なインフラストラクチャが障害発生時に保護されるように VM で実行されているワークロードをレプリケートする Azure サービスです。  [Azure Site Recovery の詳細については、こちらを参照してください](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)。

Azure Site Recovery は、**レプリケーション**と**フェールオーバー**の 2 つのコンポーネントで構成されています。 レプリケーションの部分では、障害発生時にターゲット VM の VHD を Azure ストレージ アカウントにレプリケートすることで VM を保護します。 そのため、障害発生時にこれらの VM をフェールオーバーし、Azure で実行することができます。 また、プライマリ VM に影響を与えることなくテスト フェールオーバーを実行し、Azure で回復プロセスをテストすることができます。

障害発生時に VM を保護するには、レプリケーション コンポーネントのセットアップを完了するだけで十分です。 ただし、フェールオーバーの部分を構成するまで Azure で VM を起動することはできません。 フェールオーバーの部分のセットアップは Azure VM にフェールオーバーするときに実行できます。これは初期セットアップの一部として必須ではありません。 ホスト サーバーで障害が発生し、フェールオーバー コンポーネントをまだ構成していない場合は、その時点で構成し、保護された VM のワークロードにアクセスできます。 ただし、障害の前にフェールオーバー関連の設定を構成することをお勧めします。
 

## <a name="prerequisites-and-planning"></a>前提条件と計画

- 保護する VM をホストしている対象サーバーは、Azure にレプリケートするためにインターネットにアクセスできる必要があります。
- [Windows Admin Center ゲートウェイを Azure に接続します](azure-integration.md)。
- [容量計画ツールを確認し、レプリケーションとフェールオーバーが成功するための要件を評価します](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-capacity)。

## <a name="step-1-set-up-vm-protection-on-your-target-host"></a>手順 1:ターゲット ホスト上で VM の保護を設定します。

> [!NOTE] 
> この手順は、保護の対象となる VM を含むホスト サーバーまたはクラスターごとに 1 回実行する必要があります。

1. 保護する VM をホストするサーバーまたはクラスターに移動します (サーバー マネージャーまたはハイパーコンバージド クラスター マネージャーのいずれかを使用します)。
2. **[仮想マシン]**  >  **[インベントリ]** に移動します。
3. 任意の VM を選択します (これは保護する VM である必要はありません)。
4. **[More]** (その他) >  **[Set up VM Protection]** (VM 保護のセットアップ) を選択します。
5. Azure アカウントにサインインします。
6. 次の必要な情報を入力します。

   - **サブスクリプション:** このホスト上の Vm のレプリケーションを使用する Azure サブスクリプション。
   - **場所:** ASR のリソースの作成先となる Azure リージョン。
   - **ストレージ アカウント:** このホスト上のレプリケートされた VM ワークロードの保存先ストレージ アカウント。
   - **資格情報コンテナー:** このホストで保護されている Vm の Azure Site Recovery コンテナーの名前を選択します。

7. **[Setup ASR]** (ASR のセットアップ) を選択します。
8. 通知が表示されるまで待ちます。**Site Recovery の設定が完了した**します。
 
サービスの終了には 10 分かかる場合もあります。 **[通知]** (右上隅のベル アイコン) に移動して進行状況を監視することができます。

>[!NOTE]
> この手順により、(クラスターで構成している場合は) 対象サーバーまたはノードに ASR エージェントが自動的にインストールされ、指定された **[場所]** に **[ストレージ アカウント]** と **[資格情報コンテナー]** を指定して **[リソース グループ]** が作成されます。 また、これによりターゲット ホストが ASR サービスに登録され、既定のレプリケーション ポリシーが構成されます。

## <a name="step-2-select-virtual-machines-to-protect"></a>手順 2:保護する仮想マシンを選択します。

1. 上の手順 2 で構成したサーバーまたはクラスターに戻り、 **[仮想マシン] > [インベントリ]** の順に移動します。
2. 保護する VM を選択します。
3. **[More]** (その他) >  **[VM の保護]** の順に選択します。
4. [VM を保護するための容量の要件](https://docs.microsoft.com/azure/site-recovery/site-recovery-capacity-planner)を確認します。

    Premium ストレージ アカウントを使用する場合は、[Azure portal でアカウントを作成します](https://docs.microsoft.com/azure/storage/common/storage-premium-storage)。 Windows Admin Center ウィンドウに表示される **[新規作成]** オプションでは標準ストレージ アカウントが作成されます。

5. この VM のレプリケーションに使用する **[ストレージ アカウント]** の名前を入力し、 **[VM の保護]** を選択します。 この手順で、選択された仮想マシンのレプリケーションが有効になります。 

6. ASR がレプリケーションを開始します。 **Virtual Machine Inventory** (仮想マシンのインベントリ) グリッドの **[保護]** 列が **[はい]** に変わったら、レプリケーションは完了し、VM が保護されています。 この手順が完了するまで数分かかる場合があります。  

## <a name="step-3-configure-and-run-a-test-failover-in-the-azure-portal"></a>手順 3:構成し、Azure portal でのテスト フェールオーバーの実行

 VM レプリケーションの開始時にこの手順を完了する必要はありませんが (VM はレプリケーションで保護されます)、Azure Site Recovery をセットアップするときにフェールオーバー設定を構成することをお勧めします。 Azure VMに対してフェールオーバーの準備を行うには、次の手順を完了します。

1. [Azure ネットワークを設定](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-prepare-azure)します。フェールオーバーされた VM はこの VNET に接続されます。 リンクされたページに記載されている他の手順は Windows Admin Center によって自動的に完了します。Azure ネットワークを設定することだけが必要です。

2. [テスト フェールオーバーを実行します](https://docs.microsoft.com/azure/site-recovery/hyper-v-site-walkthrough-test-failover)。

## <a name="step-4-create-recovery-plans"></a>手順 4:復旧計画を作成します。

**回復計画**は、VM のコレクションで構成されるアプリケーション全体をフェールオーバーおよび回復できる Azure Site Recovery の機能です。 アプリケーションを構成する VM を回復計画に追加することで、保護された VM を個別に回復することが可能ですが、回復計画を通じてアプリケーション全体をフェールオーバーすることができます。 また、回復計画のテスト フェールオーバー機能を使用してアプリケーションの回復をテストすることもできます。 回復計画により、VM をグループ化し、フェールオーバー時に実行される順序をシーケンス処理し、回復プロセスの一部として実行する追加の手順を自動化することができます。 VM を保護したら、Azure portal の Azure Site Recovery コンテナーに移動し、これらの VM の回復計画を作成します。 [回復計画の詳細については、こちらを参照してください](https://docs.microsoft.com/azure/site-recovery/site-recovery-create-recovery-plans)。

## <a name="monitoring-replicated-vms-in-azure"></a>Azure でのレプリケートされた VM の監視 ##

サーバー登録でエラーがないことを確認するには、 **[Azure portal]**  >  **[すべてのリソース]**  >  **[Recovery Services コンテナー]** (手順 2 で指定したもの) > **[ジョブ]**  >  **[Site Recovery ジョブ]** の順に移動します。

**[Recovery Services コンテナー]**  >  **[レプリケートされたアイテム]** に移動して VM レプリケーションを監視できます。

資格情報コンテナーに登録されているすべてのサーバーを確認するには、 **[Recovery Services コンテナー]**  >  **[Site Recovery インフラストラクチャ]**  >  **[Hyper-V ホスト]** (Hyper-V サイト セクションの下) の順に移動します。

## <a name="known-issue"></a>既知の問題 ##

ノードが ASR のインストールや ASR サービスへの登録に失敗した場合にクラスターを ASR に登録すると、VM が保護されない場合があります。 **[Recovery Services コンテナー]**  >  **[ジョブ]**  >  **[Site Recovery ジョブ]** の順に移動して、クラスター内のすべてのノードが Azure portal に登録されていることを確認します。