---
title: Azure での UPD の記憶域の 2 つのノード記憶域スペース ダイレクト SOFS のデプロイします。
description: RDS に関する記憶域スペース ダイレクトを使用する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1099f21d-5f07-475a-92dd-ad08bc155da1
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
manager: scottman
ms.openlocfilehash: 792c9320f6976a4fc7f2ccd235f66daa0cb19b19
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66805193"
---
# <a name="deploy-a-two-node-storage-spaces-direct-scale-out-file-server-for-upd-storage-in-azure"></a>Azure での UPD の記憶域の 2 つのノード記憶域スペース ダイレクト スケール アウト ファイル サーバーを展開します。

>適用対象:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

リモート デスクトップ サービス (RDS) では、ユーザー プロファイル ディスク (Upd) のドメインに参加しているファイル サーバーが必要です。 Azure で高可用性のドメインに参加しているスケール アウト ファイル サーバー (SOFS) を展開するには、Windows Server 2016 で記憶域スペース ダイレクトを使用します。 Upd またはリモート デスクトップ サービスに慣れていない場合はチェック アウト [リモート デスクトップ サービスの開始](welcome-to-rds.md)します。

> [!NOTE] 
> Microsoft が公開され、[記憶域スペース ダイレクト スケール アウト ファイル サーバーをデプロイするための Azure テンプレート](https://azure.microsoft.com/documentation/templates/301-storage-spaces-direct/)! テンプレートを使用して、展開を作成したり、この記事の手順を使用できます。 

DS シリーズ Vm と premium storage データ ディスクと、SOFS を展開することをお勧めが同じ数と各 VM でのデータ ディスクのサイズ。 2 つのストレージ アカウントの最低限を必要になります。 

小規模の展開では、2 ノード クラスターをクラウド ミラーリング監視サーバー、2 つのコピーと、ボリュームをミラー化する場所お勧めします。 データ ディスクを追加することで小規模な展開を拡大します。 (Vm) のノードを追加することで大規模な展開を拡大します。 

これらの手順では、2 つのノードの展開です。 次の表では、お客様のビジネス ユーザーの数の Upd を格納する必要があります、VM とディスクのサイズを示します。 

| Users | 合計 (GB) | VM | 番号ディスク | ディスクの種類 | ディスク サイズ (GB) | 構成   |
|-------|------------|----|---------|-----------|----------------|-----------------|
| 10    | 50         | DS1 | 2       | P10       | 128            | x (DS1 + 2 P10) 2  |
| 25    | 125        | DS1 | 2       | P10       | 128            | x (DS1 + 2 P10) 2  |
| 50    | 250        | DS1 | 2       | P10       | 128            | x (DS1 + 2 P10) 2  |
| 100   | 500        | DS1 | 2       | P20       | 512            | x (ds 1 + 2 P20) 2  |
| 250   | 1250       | DS1 | 2       | P30       | 1024           | x (DS1 + 2 P30) 2  |
| 500   | 2500       | DS2 | 3       | P30       | 1024           | x (DS2 + 3 P30) 2  |
| 1000  | 5000       | DS3 | 5       | P30       | 1024           | x (DS3 + 5 P30) 2  |
| 2500  | 12500      | DS4 | 13      | P30       | 1024           | x (DS4 + 13 P30) 2 |
| 5000  | 25000      | ~ DS5 | 25      | P30       | 1024           | x (~ DS5 + 25 P30) 2 | 

(呼び出しました私たち"my dc"の下) ドメイン コント ローラーと 2 つのノードの Vm ("マイ fsn1"と"マイ fsn2") を作成し、2 つのノードの記憶域スペース ダイレクト SOFS に Vm を構成するには、次の手順を使用します。

1. 作成、 [Microsoft Azure サブスクリプション](https://azure.microsoft.com)します。
2. [Azure ポータル](https://ms.portal.azure.com)することができます。
3. 作成、 [Azure ストレージ アカウント](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/#create-a-storage-account) Azure リソース マネージャーでします。 新しいリソース グループに作成し、次の構成を使用します。
   - デプロイ モデル:Resource Manager
   - ストレージ アカウントの種類です。一般的な用途
   - パフォーマンス レベル:Premium
   - レプリケーション オプション:LRS
4. クイック スタート テンプレートを使用するか、手動でフォレストを展開して、Active Directory フォレストを設定します。 
   - Azure のクイック スタート テンプレートを使用して展開します。
      - [新しい AD フォレストと Azure VM の作成します。](https://azure.microsoft.com/documentation/templates/active-directory-new-domain/)
      - [2 つのドメイン コント ローラーで新しい AD ドメインを作成](https://azure.microsoft.com/documentation/templates/active-directory-new-domain-ha-2-dc/) (の高可用性)
   - 手動で [フォレストを展開](https://azure.microsoft.com/documentation/articles/active-directory-new-forest-virtual-machine/) 以下の構成。
      - ストレージ アカウントと同じリソース グループ内の仮想ネットワークを作成します。
      - 推奨サイズ:DS2 (ドメイン コント ローラーが複数のドメイン オブジェクトをホストする場合、サイズを増やす)
      - 自動的に生成された VNet を使用します。
      - AD DS をインストールする手順に従います。
5. ファイル サーバー クラスターのノードを設定します。 展開することでこれを行う、 [Windows Server 2016 記憶域スペース ダイレクト SOFS クラスター Azure テンプレート](https://azure.microsoft.com/resources/templates/301-storage-spaces-direct/)かに従って手順 6 ~ 11 を手動で展開します。
6. ファイル サーバー クラスターのノードを手動で設定するには。
   1. 最初のノードを作成します。 
      1. Windows Server 2016 のイメージを使用して新しいバーチャル マシンを作成します。 (をクリックして **新しい > 仮想マシン > Windows Server 2016 します。** Select **リソース マネージャー**, 、クリックして **作成**.)
      2. 基本構成を次のように設定します。
         - -Fsn1 名: マイ
         - VM ディスクの種類 SSD
         - 既存のリソース グループ、手順 3. で作成したものを使用します。 
      3. ［サイズ］：DS1、DS2、DS3、DS4、またはユーザーによって ~ DS5 (上記の手順の先頭にある表を参照してください) が必要です。 Premium ディスクのサポートが選択されていることを確認します。
      4. 設定: 
         - ストレージ アカウント:手順 3 で作成したストレージ アカウントを選択します。
         - 高可用性 - 新しい可用性セットを作成します。 (をクリックして **高可用性 > 新規作成**, 、し (たとえば、s2d-クラスター) の名前を入力します。 既定値を使用して **更新ドメイン** と **障害ドメイン**.)
   2. 2 番目のノードを作成します。 次の変更では、上記の手順を繰り返します。
      - -Fsn2 名: マイ
      - 高可用性: 上記で作成した可用性セットを選択します。  
7. [データ ディスクをアタッチ](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-attach-disk-portal/) に従って、ユーザーは、クラスター ノードの Vm (上記の表で説明) と必要があります。 ディスクの作成し、設定、VM にアタッチされているデータの後に**キャッシュ ホスト**に**None**します。
8. すべての Vm の IP アドレスを設定**静的**します。 
   1. リソース グループで、仮想マシンを選択し、 **ネットワーク インターフェイス** (下にある **設定**)。 表示されているネットワーク インターフェイスを選択し、クリックして **IP 構成**します。 指定の IP 構成を選択して、選択 **静的**, 、 をクリックし、 **保存**します。
   2. ドメイン コント ローラー (マイ dc の例) プライベート IP アドレス (10.x.x.x) に注意してください。
9. クラスター ノードの Vm の Nic で、dc サーバーにプライマリ DNS サーバー アドレスを設定します。 VM を選択し、 **ネットワーク インターフェイス > DNS サーバー > カスタム DNS**します。 前述したプライベート IP アドレスを入力し、クリックして**保存**します。
10. 作成、 [Azure ストレージ アカウントをクラウドのミラーリング監視サーバーを設定する](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)です。 (リンクの手順を使用する場合停止"を構成するクラウド ミラーリング監視サーバーをフェールオーバー クラスター マネージャーの GUI"を取得する - その手順を実行します。)
11. 記憶域スペース ダイレクトのファイル サーバーを設定します。 ノード VM に接続し、次の Windows PowerShell コマンドレットを実行します。
    1. 2 つのファイル サーバー クラスター ノードの Vm では、フェールオーバー クラスタ リング機能とファイル サーバーの機能をインストールします。

       ```powershell
       $nodes = ("my-fsn1", "my-fsn2")
       icm $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools} 
       icm $nodes {Install-WindowsFeature FS-FileServer} 
       ```
    2. クラスター ノードの Vm を検証し、2 つのノードの SOFS クラスターを作成します。

       ```powershell
       Test-Cluster -node $nodes
       New-Cluster -Name MY-CL1 -Node $nodes –NoStorage –StaticAddress [new address within your addr space]
       ``` 
    3. クラウドのミラーリング監視サーバーを構成します。 クラウド監視ストレージ アカウント名とアクセス キーを使用します。

       ```powershell
       Set-ClusterQuorum –CloudWitness –AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> 
       ```
    4. 記憶域スペースを直接有効にします。

       ```powershell
       Enable-ClusterS2D 
       ```
      
    5. 仮想ディスクのボリュームを作成します。

       ```powershell
       New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 120GB 
       ```
       SOFS クラスターでクラスターの共有ボリュームに関する情報を表示するには、次のコマンドレットを実行します。

       ```powershell
       Get-ClusterSharedVolume
       ```
   
    6. スケール アウト ファイル サーバー (SOFS) を作成します。

       ```powershell
       Add-ClusterScaleOutFileServerRole -Name my-sofs1 -Cluster MY-CL1
       ```

    7. SOFS クラスター上には、新しい SMB ファイル共有を作成します。

       ```powershell
       New-Item -Path C:\ClusterStorage\Volume1\Data -ItemType Directory
       New-SmbShare -Name UpdStorage -Path C:\ClusterStorage\Volume1\Data
       ```

共有があるようになりました`\\my-sofs1\UpdStorage`、UPD の記憶域に使用できるときにする[UPD を有効にする](https://social.technet.microsoft.com/wiki/contents/articles/15304.installing-and-configuring-user-profile-disks-upd-in-windows-server-2012.aspx)ユーザー向けです。 
