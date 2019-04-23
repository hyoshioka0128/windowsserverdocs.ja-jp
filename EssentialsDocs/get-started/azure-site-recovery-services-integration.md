---
title: Azure Site Recovery サービスの統合
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/01/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 94894cd9be06485bf842f96517172db709dbe93d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848743"
---
#<a name="azure-site-recovery-services-integration"></a>Azure Site Recovery サービスの統合

>適用先:Windows Server 2016 Essentials

[Azure Site Recovery Services](https://docs.microsoft.com/azure/site-recovery/)仮想マシン (VM) のリアルタイムのレプリケーションを有効にする Microsoft Azure によって提供されるサービスを Azure にバックアップ コンテナーには。 サーバーまたはサイトのハードウェアまたはその他の障害によっては、ことすることができますへのフェールオーバー Azure バックアップ コンテナーに格納されている VM イメージを Azure で実行中の VM としてプロビジョニングされます。 Azure へのフェールオーバーが発生した場合、Azure Virtual network と組み合わせて Azure で実行するサーバーに、オンプレミス サーバーに接続した Pc のクライアントは接続透過的にします。

Windows Server Essentials と Azure Site Recovery Services の統合の構成と同じ方法で起動[Azure 仮想ネットワーク](azure-virtual-network-integration.md)します。 **Microsoft クラウド サービスの統合**ダッシュ ボード] ページで [ **Azure Site Recovery Services との統合**ダッシュ ボードの右側に。

![Windows Server Essentials ダッシュ ボードのホーム ページで、[概要] タブを示すスクリーン ショット。 [概要] タブの [サービス] を選択すると Azure Recovery が現在無効になっている Microsoft クラウド サービスの統合サービスでダッシュ ボードを示します。](media/azure-site-recovery-1.PNG)

Azure Virtual network 統合、Azure Backup 統合では、使用する既存の Azure アカウント、Azure にログインか、新しいアカウントを作成する必要があります。

![Azure にレプリケーションを有効にするウィザードの Microsoft Azure にサインイン ページを示すスクリーン ショット。 ユーザーが Microsoft Azure にまだ署名されていないために、サインイン ボタンが表示されます。](media/azure-site-recovery-2.PNG)

を正常には Azure にログインした後は、VM を保存およびホストされているが、Azure リージョンと同様に、Azure Site Recovery サービスに関連付けるサブスクリプションを要求する画面が表示されます。

![Azure にレプリケーションを有効にするウィザードの Microsoft Azure にサインイン ページを示すスクリーン ショット。 Microsoft Azure にサインインしたユーザー、ために、このページは、サブスクリプション、ストレージ アカウント、およびリージョンを選択するためのオプションを提供します。](media/azure-site-recovery-3.PNG)

サブスクリプションと地域の選択、新しいタブに表示されます、 **Windows Server Essentials ダッシュ ボード**と呼ばれる**Azure Recovery**します。 ネットワークのスキャンを実行を特定し、サポートされているホスト サーバーの列挙 (Windows Server、HYPER-V 2012 R2 を実行している以上) と個々 のホストの仮想マシン (ゲスト)。

![Windows Server Essentials ダッシュ ボードの [Azure の回復] ページを示すスクリーン ショット。 これらのホストで実行されている仮想マシンとは、2 つの HYPER-V ホストが表示されます。 RAM-H1-7 を選択すると、ホスト上の ramh157v01 という名前の仮想マシンと Azure へのレプリケーションは、この仮想マシンは現在無効です。](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>ゲスト仮想マシンの保護を有効にします。

クリックすることができます、Azure Recovery ウィンドウに存在する仮想マシンの選択、 **Azure へのレプリケーションを有効にする**を準備して仮想マシンをコピーするダッシュ ボードの右側にある™ s イメージを Azure:

![Azure にレプリケーションを有効にする ダイアログを示すスクリーン ショット。 ホストが追加されると、進行状況バーが表示されます。](media/azure-site-recovery-5.PNG)

このプロセス中には、Azure Site Recovery サービス エージェントは、ホスト サーバーでバックアップ コンテナーで VM は格納されているゲストのイメージを作成して、イメージを Azure のレプリケーションが開始されますインストールされます。 レプリケートされている VM のサイズに応じてレプリケーション プロセスの完了は、数時間から数日かかる場合があります。 Azure には、全体の VM イメージと最新の差分がレプリケートされた、までフェールオーバー タスクが使用できなくと、VM は保護されていません。 Azure の回復 ウィンドウで、保護の状態列が変更されますレプリケーションが完了すると、**レプリケート**に**有効**:。

![Windows Server Essentials ダッシュ ボードの [Azure の回復] ページを示すスクリーン ショット。 これらのホストで実行されている仮想マシンとは、2 つの HYPER-V ホストが表示されます。 RAM-H1-2 を選択すると、ホスト上の ramh12v02 という名前の仮想マシンと Azure へのレプリケーションは、この仮想マシンが現在有効です。](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>ゲスト VM を Azure のフェールオーバー

![Azure のページへの VM フェールオーバーを示すスクリーン ショット。](media/azure-site-recovery-7.PNG)

仮想マシンが保護されている失敗した場合、または失敗した場合、Azure へのフェールオーバーで保護された仮想マシンの実行までのビジネス継続性を維持するために実行できるホスト サーバーにオンプレミス仮想マシンまたはホスト サーバーは修復された利用できます。 表示上の図、としては、Azure Site Recovery Services でサポートされているフェールオーバーの 3 つの種類があります。

-   **テスト フェールオーバー** ƒA 適切な障害回復計画には、実際に障害が発生した場合、最小限のダウンタイムを確実に障害をシミュレートする機能が組み込まれています。 テスト フェールオーバーは、VM イメージが、recovery コンテナーにレプリケートされる、としては、Azure で実行中の仮想マシンをプロビジョニングし、ビジネスに適用されるシナリオをテストするサーバーに接続することができます。 テスト フェールオーバー中には、ローカルの仮想マシンはディザスター リカバリーのテスト中にビジネスを妨害しないか、ありません中断された実行を続けます。 テスト フェールオーバーが完了すると、仮想マシンのプロビジョニングを解除し、VHD を削除する Azure ポータルでテストを停止します。 テスト全体のフェールオーバー中に、recovery コンテナーで VM イメージをこれまで何かのように、オンサイトの VM からレプリケートが続行されます。

-   **計画外フェールオーバー** ƒAn 計画外のフェールオーバーは、保護されたホスト サーバーまたはホスト サーバーで実行されている VM で実際のエラーがある場合に発生します。 フェールオーバーは、Windows Server Essentials ダッシュ ボードから手動でトリガーされるまたは場合は、障害が発生したサーバー自体は、Windows Server Essentials を実行するサーバー トリガーできる、Azure Portal から直接。 ここでは、計画外のフェールオーバーは、VM イメージが、recovery コンテナーにレプリケートされる、としては、Azure では、実行中の仮想マシンをプロビジョニングし、ビジネスに適用されるシナリオをテストするサーバーに接続することができます。 オンプレミスで、サーバーが復元されると、ローカル サーバーに送れば、VM イメージをコピーして、Azure Portal から、手動でフェールバックをトリガーできます。

-   **計画されたフェールオーバー** ƒA 計画されたフェールオーバーは計画的なアクティビティは、ハードウェアのメンテナンスなど行う必要があります、サーバーがダウン必要があり、実行できるアクションです。 同じプロセスでは、計画的なフェールオーバーが発生した場合、に関して、Azure 内のレプリケートされた VM イメージのプロビジョニングが行われます。 ただし、これを行う前に、ローカル サーバーがシャット ダウンでは、すべての変更は、シャット ダウンする前に Azure にレプリケートされたことを確認する適切な方法です。 計画的メンテナンスが完了すると、Windows Server Essentials ダッシュ ボードで、または Azure ポータルの表示をローカル サーバーとし、Azure、および delete で VM をプロビジョニング解除のいずれかからのフェールバックを手動でトリガーできるのです。VHD ファイル。 後は、オンプレミス VM から Azure へのレプリケーションを継続して再度通常どおりに発生します。

上記の 3 つのケースのような Azure、Windows Server Essentials ダッシュ ボードに VM をフェールオーバー時に表示されます、新しい VM 下の図のように実行されている Azure。

![Windows Server Essentials ダッシュ ボードの [Azure の回復] ページを示すスクリーン ショット。 Essentials、および仮想マシンが Azure で実行されている名前付きの Essentials-テストでは、ホストが Azure にフェールオーバーしていることを示しますという名前のホストに Azure へのレプリケーションを有効になっています。](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>関連項目
--------
[Windows Server Essentials を概要します。](get-started.md)
