---
title: Azure Site Recovery サービスの統合
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/01/2016
ms.topic: article
ms.assetid: 262701a6-8a97-4c4e-bfbf-9f8007c308d6
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 7c30d99bd1a0019130f7e39f70b289effd6935c4
ms.sourcegitcommit: 04637054de2bfbac66b9c78bad7bf3e7bae5ffb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838251"
---
# <a name="azure-site-recovery-services-integration"></a>Azure Site Recovery サービスの統合

>適用対象: Windows Server 2016 Essentials

[Azure Site Recovery サービス](/azure/site-recovery/)は、Azure のバックアップコンテナーへの仮想マシン (VM) のリアルタイムレプリケーションを可能にする Microsoft Azure によって提供されるサービスです。 ハードウェアやその他の障害によってサーバーまたはサイトがダウンしている場合は、Azure にフェールオーバーできます。この場合、バックアップコンテナーに格納されている VM イメージは、実行中の VM として Azure にプロビジョニングされます。 Azure へのフェールオーバーが発生した場合は、azure Virtual network と組み合わせることで、以前にオンプレミスサーバーに接続していたクライアント Pc は、Azure で実行されているサーバーに透過的に接続します。

Azure Site Recovery サービスと Windows Server Essentials の統合は、 [Azure Virtual network](azure-virtual-network-integration.md)の構成と同じ方法で開始されます。 ダッシュボードの [ **Microsoft Cloud Services 統合**] ページで、ダッシュボードの右側にある [ **Azure Site Recovery Services との統合**] をクリックします。

![Windows Server Essentials ダッシュボードのホームページにある [作業の開始] タブを示すスクリーンショット。 [作業の開始] タブの [サービス] セクションが選択されています。ダッシュボードは、Azure Recovery が現在無効になっている Microsoft Cloud Services 統合の下に表示されます。](media/azure-site-recovery-1.PNG)

Azure Virtual network の統合と Azure Backup 統合と同様に、既存の Azure アカウントを使用して Azure にログインするか、新しいアカウントを作成する必要があります。

![[Azure へのレプリケーションを有効にする] ウィザードの [Microsoft Azure へのサインイン] ページを示すスクリーンショット。 ユーザーがまだ Microsoft Azure にサインインしていないため、[サインイン] ボタンが表示されます。](media/azure-site-recovery-2.PNG)

Azure に正常にログインした後、Azure Site Recovery サービスに関連付けるサブスクリプションと、VM が格納およびホストされる Azure リージョンを確認する画面が表示されます。

![[Azure へのレプリケーションを有効にする] ウィザードの [Microsoft Azure へのサインイン] ページを示すスクリーンショット。 ユーザーが Microsoft Azure にサインインしているため、このページには、サブスクリプション、ストレージアカウント、およびリージョンを選択するためのオプションが表示されます。](media/azure-site-recovery-3.PNG)

サブスクリプションとリージョンを選択すると、 **Azure Recovery**という名前の**Windows Server Essentials ダッシュボード**に新しいタブが表示されます。 ネットワークスキャンは、(Windows Server Hyper-v 2012 R2 以降を実行している) サポートされているホストサーバーだけでなく、個々のホストの下にある仮想マシン (ゲスト) を識別して列挙するために行われます。

![Windows Server Essentials ダッシュボードの Azure 回復ページを示すスクリーンショット。 これらのホストで実行されている仮想マシンと共に、2つの Hyper-v ホストが表示されます。 ホスト RAM 上の ramh157v01 という名前の仮想マシンが選択されており、この仮想マシンの Azure へのレプリケーションは現在無効になっています。](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>ゲスト仮想マシンの保護を有効にする

Azure 回復ウィンドウにある仮想マシンを選択したら、ダッシュボードの右側にある [ **azure へのレプリケーションを有効**にする] をクリックして、仮想マシンのイメージを準備して &trade; azure にコピーできます。

![[Azure へのレプリケーションを有効にする] ダイアログボックスを示すスクリーンショット。 ホストが追加されている間、進行状況バーが表示されます。](media/azure-site-recovery-5.PNG)

このプロセスでは、Azure Site Recovery Service agent がホストサーバーにインストールされ、ゲスト VM のイメージが格納されるバックアップコンテナーが作成され、Azure へのイメージのレプリケーションが開始されます。 レプリケートされる VM のサイズによっては、レプリケーションプロセスの完了に数時間または数日かかることがあります。 VM イメージ全体と最新のデルタが Azure にレプリケートされるまで、フェールオーバータスクは使用できず、VM は保護されません。 レプリケーションが完了すると、[Azure 回復] ウィンドウの [保護の状態] 列の **[レプリケーション]** が [**有効**] に変わります。

![Windows Server Essentials ダッシュボードの Azure 回復ページを示すスクリーンショット。 これらのホストで実行されている仮想マシンと共に、2つの Hyper-v ホストが表示されます。 ホスト RAM-H1-2 で ramh12v02 という名前の仮想マシンが選択され、Azure へのレプリケーションは現在この仮想マシンに対して有効になっています。](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>ゲスト VM の Azure へのフェールオーバー

![Azure へのフェールオーバー VM を示すスクリーンショット。](media/azure-site-recovery-7.PNG)

保護されている仮想マシンに障害が発生した場合、または保護された仮想マシンが実行されているホストサーバーで障害が発生した場合、オンプレミスの仮想マシンまたはホストサーバーが修復されて使用可能になるまで、ビジネスの継続性を維持するために Azure へのフェールオーバーを実行できます。 上の図に示すように、Azure Site Recovery サービスでは次の3種類のフェールオーバーがサポートされています。

-   **テストフェールオーバー** ƒA 良好なディザスターリカバリー計画では、災害をシミュレートして、実際の障害発生時のダウンタイムを最小限に抑えることができます。 テストフェールオーバーは、復旧コンテナーにレプリケートされた VM イメージを取得し、それを Azure 内の実行中の仮想マシンとしてプロビジョニングします。また、サーバーに接続して、ビジネスに適用されるシナリオをテストすることができます。 テストフェールオーバー中は、ディザスターリカバリーテスト中にビジネスを中断しないように、ローカル仮想マシンは中断されずに実行を続けます。 テストフェールオーバーが完了したら、Azure Portal でテストを停止します。これにより、仮想マシンがプロビジョニング解除され、VHD が削除されます。 テストフェールオーバー全体で、復旧コンテナー内の VM イメージは、何も発生していないかのように、オンサイトの VM から引き続きレプリケートされます。

-   **計画外フェール**オーバーƒAn は、保護されたホストサーバーまたはホストサーバーで実行されている VM で実際の障害が発生した場合に発生します。 フェールオーバーは、Windows Server Essentials ダッシュボードから手動でトリガーされます。障害が発生したサーバー自体が、Windows Server Essentials が実行されているサーバーである場合は、Azure Portal から直接トリガーできます。 この場合、計画されていないフェールオーバーは、復旧コンテナーにレプリケートされた VM イメージを取得し、それを Azure 内の実行中の仮想マシンとしてプロビジョニングします。また、サーバーに接続して、ビジネスに適用されるシナリオをテストすることができます。 サーバーがオンプレミスで復元されると、Azure Portal から手動フェールバックをトリガーし、VM イメージをローカルサーバーにコピーして戻すことができます。

-   計画された**フェール**オーバーƒA 計画フェールオーバーは、ハードウェアメンテナンスなどの予定されたアクティビティを実行する必要がある場合に、サーバーを停止する必要がある場合に実行できるアクションです。 計画フェールオーバーが発生した場合、Azure でレプリケートされた VM イメージのプロビジョニングに関して同じプロセスが実行されます。 ただし、これを行う前に、ローカルサーバーは、シャットダウン前にすべての変更が Azure にレプリケートされるように、正しい方法でシャットダウンされます。 計画済みメンテナンスが完了したら、Windows Server Essentials ダッシュボードまたは Azure portal から手動でフェールバックをトリガーできます。これにより、ローカルサーバーが起動し、Azure で VM がプロビジョニング解除され、が削除されます。VHD ファイル。 オンプレミスの VM から Azure へのレプリケーションは、正常に実行され続けます。

上記の3つのケースでは、VM が Azure にフェールオーバーされると、Windows Server Essentials ダッシュボードに、次の図のように、Azure の新しい VM が表示されます。

![Windows Server Essentials ダッシュボードの Azure 回復ページを示すスクリーンショット。 Azure へのレプリケーションは、Essentials という名前のホストに対して有効になっています。また、Azure で実行されている Essentials-Test という名前の仮想マシンは、ホストが Azure にフェールオーバーしたことを示します。](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>関連項目
--------
[Windows Server Essentials の概要](get-started.md)