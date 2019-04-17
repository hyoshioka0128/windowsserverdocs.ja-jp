---
title: "Azure Site Recovery サービスの統合"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 85e681cfc19241941773dd94f05ba59759aaf62a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
#<a name="azure-site-recovery-services-integration"></a>Azure Site Recovery サービスの統合

>Windows Server 2016 Essentials の適用対象:

[Azure Site Recovery サービス](https://azure.microsoft.com/en-us/documentation/services/site-recovery/)、仮想マシン (VM) のリアルタイムのレプリケーションを有効にすると、Microsoft Azure で提供されるサービスを Azure にバックアップ資格情報コンテナーには。 イベントで、サーバーまたはサイトによって、ハードウェアまたはその他の障害が停止して、することができますフェールオーバー、バックアップ コンテナーに格納されている VM イメージが Azure で実行中の VM としてプロビジョニングされる Azure にします。 Azure へのフェールオーバーが発生した場合、Azure の仮想ネットワークと組み合わせるクライアント、内部設置型サーバーに接続されていた Pc は透過的に接続 Azure で実行しているサーバー。

Azure Site Recovery サービスを Windows Server Essentials と統合することがの構成と同じ方法で起動した[Azure の仮想ネットワーク](azure-virtual-network-integration.md)します。 **Microsoft クラウド サービスと統合**、ダッシュ ボード ページで、[ **Azure Site Recovery サービスとの統合**ダッシュ ボードの右側に。

![Windows Server Essentials ダッシュ ボードのホーム ページで、[概要] タブを示すスクリーン ショット。 [概要] タブの [サービス] が選択されているし、Azure Recovery が現在無効になっている Microsoft クラウド サービスの統合サービスで、ダッシュ ボードを示します。](media/azure-site-recovery-1.PNG)

Azure の仮想ネットワークの統合、Azure Backup 統合と同様には、する Azure、既存のアカウントを Azure にログインするか、新しいアカウントを作成する必要があります。

![ログ Azure にレプリケーションを有効にするウィザードの [内に Microsoft Azure] ページを示すスクリーン ショット。 ユーザーがまだ Microsoft Azure にログインしていないために、ボタンのログが表示されます。](media/azure-site-recovery-2.PNG)

Azure に正常にログインするは、Azure サイト回復サービスだけでなく、VM を格納およびホストされているが、Azure の地域に関連付けるしたいサブスクリプションを要求する画面が表示されます。

![ログ Azure にレプリケーションを有効にするウィザードの [内に Microsoft Azure] ページを示すスクリーン ショット。 ユーザーは、Microsoft Azure にログインが、ために、このページは、サブスクリプション、ストレージ アカウント、および地域を選択するためのオプションを提供します。](media/azure-site-recovery-3.PNG)

サブスクリプションと地域の選択、新しいタブに表示されます、**Windows Server Essentials ダッシュ ボード**と呼ばれる**Azure Recovery**します。 ネットワークのスキャンを実行を特定し、サポートされているホスト サーバーを列挙 (Windows Server Hyper-V 2012 R2 を実行している以降) 個々 のホストの仮想マシン (ゲスト) および。

![Windows Server Essentials ダッシュ ボードの Azure Recovery] ページを示すスクリーン ショット。 これらのホストで実行されている仮想マシンとは、次の 2 つの Hyper-V ホストが表示されます。 RAM-H1-7 を選択すると、ホスト上の ramh157v01 をという名前のバーチャル マシンと Azure へのレプリケーションはこのバーチャル マシンの現在無効です。](media/azure-site-recovery-4.PNG)

### <a name="enabling-guest-virtual-machines-for-protection"></a>ゲストの仮想マシンの保護を有効にします。

Azure Recovery 枠に仮想マシンの選択した場合、時にクリックして**Azure へのレプリケーションの有効化**準備し、仮想マシンをコピーするダッシュ ボードの右側にある™ を Azure のイメージ。

![Azure にレプリケーションを有効にする] ダイアログを示すスクリーン ショット。 ホストが追加されると、進行状況バーが表示されます。](media/azure-site-recovery-5.PNG)

このプロセス中に、ホスト サーバーで、ここで VM は保存されているゲストのイメージが作成され、Azure するイメージのレプリケーションが開始し、バックアップ コンテナー Azure サイト回復サービス エージェントをインストールします。 レプリケートされている VM のサイズ、によって、レプリケーション プロセスの完了は、数時間から数日かかる場合があります。 全体の VM イメージと最新のデルタが Azure にレプリケートされるまでフェールオーバー タスク利用できず、VM が保護されていません。 Azure Recovery] ウィンドウで [保護の状態] 列をから変更は、レプリケーションが完了すると、**複製**に**有効**:

![Windows Server Essentials ダッシュ ボードの Azure Recovery] ページを示すスクリーン ショット。 これらのホストで実行されている仮想マシンとは、次の 2 つの Hyper-V ホストが表示されます。 RAM-H1-2 を選択すると、ホスト上の ramh12v02 をという名前のバーチャル マシンと Azure へのレプリケーションが、このバーチャル マシンの現在有効です。](media/azure-site-recovery-6.PNG)

### <a name="failover-of-a-guest-vm-to-azure"></a>ゲストを Azure VM のフェールオーバー

![Azure のページにフェールオーバー VM を示すスクリーン ショット。](media/azure-site-recovery-7.PNG)

ときに保護が失敗した場合、またはまでのビジネス継続性を維持するために、保護された仮想マシンがで実行されるが失敗した場合、Azure へのフェールオーバーを実行できるホスト サーバーである仮想マシンに内部設置型仮想マシンまたはホスト サーバーを修復し、利用可能です。 として表示上の図では、Azure Site Recovery サービスでサポートされているフェールオーバーの 3 つの種類があります。

-   **テスト フェールオーバー** ƒA 適切な障害回復計画にして、最小限のダウンタイムを実際に障害が発生した場合の障害をシミュレートする機能が組み込まれています。 テスト フェールオーバーは、回復の資格情報コンテナーにレプリケートされた、Azure で実行中の仮想マシンとしてそれをプロビジョニングし、ビジネスに適用されているシナリオをテストするサーバーに接続することができる VM イメージを取得します。 テスト フェールオーバー、時にローカルの仮想マシンは引き続き実行のない中断を災害復旧のテスト中にビジネスを妨害しないしたりします。 テスト フェールオーバーが完了するとは、Azure ポータルで、バーチャル マシンをプロビジョニング解除し、VHD を削除するテストを停止します。 全体のテスト フェールオーバー、時に、回復の資格情報コンテナーに VM イメージは、何も、これが発生しなかった場合、オンサイトの VM から複製を取得するのには続行されます。

-   **計画外のフェールオーバー** ƒAn、保護されたホスト サーバーまたはホスト サーバー上で実行されている VM と実際の障害がある場合に、計画外のフェールオーバーが発生します。 フェールオーバーは、いずれかの Windows Server Essentials ダッシュ ボードから手動でトリガーは、または場合は、障害が発生したサーバー自体は、Windows Server Essentials を実行するサーバーをトリガーできます、Azure ポータルから直接します。 この場合は、計画外のフェールオーバーは、回復の資格情報コンテナーにレプリケートされた、Azure では、実行中の仮想マシンとしてそれをプロビジョニングし、ビジネスに適用されているシナリオをテストするサーバーに接続することができる VM イメージを取得します。 内部設置型で、サーバーが復元されると、手動のフェールバックがローカル サーバーに戻す VM イメージをコピーして、Azure ポータルからトリガーできます。

-   **計画フェールオーバー** ƒA 計画フェールオーバーは計画的なアクティビティ、ハードウェア メンテナンスなど必要がありますを実行するサーバーがダウン必要があり、実行できるアクションです。 同じプロセスでは、計画フェールオーバーが発生した場合、Azure でレプリケートされた VM イメージのプロビジョニングに関するが行われます。 ただし、これを実行する前に、ローカル サーバーをシャット ダウン見やすくするすべての変更は、シャット ダウンする前に Azure にレプリケートすることを確認します。 計画されたメンテナンスが完了すると、Windows Server Essentials ダッシュ ボードまたは bring アップ、ローカル サーバーと Azure と削除内の仮想マシンのプロビジョニング解除し、Azure ポータルからのフェールバックを手動で開始することができます、します。VHD ファイルです。 内部設置型の VM から Azure へのレプリケーションは、引き続き発生もう一度通常どおりします。

上記の 3 つのケースで、Azure、Windows Server Essentials ダッシュ ボードにバーチャル マシン フェールオーバーと表示されます、新しい VM で、次の図に示すように実行されている Azure。

![Windows Server Essentials ダッシュ ボードの Azure Recovery] ページを示すスクリーン ショット。 Essentials、および名前付き Essentials テスト Azure で実行されているできなかったことを示す、ホストが経由で Azure 仮想マシンをという名前のホストに Azure へのレプリケーションを有効になっています。](media/azure-site-recovery-8.PNG)

<a name="see-also"></a>参照してください。
--------
[Windows Server Essentials を使ってみる](get-started.md)
