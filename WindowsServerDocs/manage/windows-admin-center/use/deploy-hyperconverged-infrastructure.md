---
title: Windows 管理センターを使用してハイパー集約インフラストラクチャを展開する
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.prod: windows-server
ms.technology: manage
ms.date: 11/04/2019
ms.openlocfilehash: 62bf21dd0afcb99aa77cff8a733e80fc4cffe2fb
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73587232"
---
# <a name="deploy-hyperconverged-infrastructure-with-windows-admin-center"></a>Windows 管理センターを使用してハイパー集約インフラストラクチャを展開する

> 適用対象: Windows 管理センター、Windows 管理センタープレビュー

Windows 管理センター[バージョン 1910](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)以降を使用して、2つ以上の適切な windows サーバーを使用してハイパー集約インフラストラクチャを展開することができます。 この新しい機能では、機能のインストール、ネットワークの構成、クラスターの作成、記憶域スペースダイレクトまたはソフトウェアによるネットワーク制御 (SDN) の展開など、選択した場合に役立つマルチステージワークフローの形式を使用します。

![クラスター作成ワークフローのスクリーンショット](../media/deploy-hyperconverged-infrastructure/deployment-workflow-screenshot.png)

  > [!Important]
  > この機能は、アクティブな開発中です。 プレビュー版として提供されているので、早い段階で試して、フィードバックを共有できます。

## <a name="preview-the-workflow"></a>ワークフローのプレビュー

### <a name="1-prerequisites"></a>1. 前提条件

Windows 管理センターのクラスター作成ワークフローでは、ベアメタルオペレーティングシステムのインストールは実行されないため、まず各サーバーに Windows Server をインストールする必要があります。 サポートされているバージョンは、Windows Server 2016、Windows Server 2019、および Windows Server Insider Preview です。 また、ワークフローを開始する前に、Windows 管理センターが実行されているのと同じ Active Directory ドメインに各サーバーを参加させる必要があります。

### <a name="2-install-windows-admin-center"></a>2. Windows 管理センターをインストールする
 
指示に従って、最新バージョンの Windows 管理センターを[ダウンロードしてインストール](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)します。

### <a name="3-install-the-cluster-creation-extension"></a>3. クラスター作成拡張機能をインストールする

クラスター作成ワークフローは、Windows 管理センターの拡張機能フィードによって配信および更新されます。 これは、お客様からのフィードバックに対処し、プレビュー段階で迅速に改善を行うことができるようにするためです。

拡張機能をインストールするには、Windows 管理センターを起動し、次のようにします。

1.  右上にある [設定] アイコンを選択します。
2.  [拡張機能] に移動します。
3.  クラスター作成拡張機能の検索
4.  インストールの選択

![クラスター作成拡張機能をインストールする4つの手順のスクリーンショット](../media/deploy-hyperconverged-infrastructure/how-to-install.png)

インストールが完了したら、左上のドロップダウンからクラスター作成拡張機能を選択します。

![クラスター作成拡張機能の起動のスクリーンショット](../media/deploy-hyperconverged-infrastructure/how-to-launch.png)

## <a name="limitations-of-the-preview-release"></a>プレビューリリースの制限事項

クラスター作成ワークフローは、アクティブな開発の段階にあります。つまり、完了していません。

現在のプレビューリリースには、次のような制限があります。

1.  **ドメインの要件。** 現在、ワークフローでは、追加するすべてのサーバーが、Windows 管理センターが実行されているのと同じ Active Directory ドメインに既に参加している必要があります。
2.  **スクリプトを表示します。** 現在のプレビューリリースでは、Windows 管理センターの [スクリプトの表示] 機能を使用してワークフローが実行するスクリプトは表示されません。また、最後に発生したすべてのものの完全なレポートをダウンロードすることもできません。 これは多くのユーザーにとって重要であることがわかっています。 それまでの間は、以下のコマンドレットを使用し[て、何が起こっているかを確認してください](#see-whats-happening)。
3.  **再開するか、やり直す。** ワークフローの途中で終了することはできますが、現在のプレビューリリースでは、中断した箇所での再開や、作業を開始する前に完全なクリーンアップを行うことはできません。 テスト用に同じサーバーに繰り返しデプロイする場合は、以下のコマンドレットを使用して[元に戻して](#undo-and-start-over)からやり直してください。
4.  **リモートダイレクトメモリアクセス (RDMA)。** 現在のプレビューリリースでは、ハイパー集約インフラストラクチャで一般的に使用される RDMA ネットワークを有効にすることはできません。 ここでは、RDMA を有効にせずにワークフローを完了し、他のツールを使用して、他の方法と同様に RDMA を有効にします。

これらの制限に対処するだけでなく、Windows 更新プログラムの適用、クラスタークォーラムのミラーリング監視サーバーの構成、仮想マシンのインポートなど、今後のリリースで追加される可能性がある、さまざまな機能があります。 必要な機能に優先順位を付けるには、以下に示すように[フィードバックを共有](#feedback)してください。

## <a name="see-whats-happening"></a>何が起こっているかを確認する

これらの Windows PowerShell コマンドレットを使用して、ワークフローの実行内容を確認します。

インストールされている Windows 機能を確認するには、`Get-WindowsFeature` コマンドレットを使用します。 次に、例を示します。

```PowerShell
Get-WindowsFeature "Hyper-V", "Failover-Clustering", "Data-Center-Bridging", "BitLocker"
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-1.png)

  > [!Note]
  > インストールされる機能は、選択したクラスターの種類によって異なります。

ネットワークアダプターとそのプロパティ (名前、IPv4 アドレス、VLAN ID など) を表示するには、次のようにします。

```PowerShell
Get-NetAdapter | Where Status -Eq "Up" | Sort InterfaceAlias | Format-Table Name, InterfaceDescription, Status, LinkSpeed, VLANID, MacAddress
Get-NetAdapter | Where Status -Eq "Up" | Get-NetIPAddress -AddressFamily IPv4 -ErrorAction SilentlyContinue | Sort InterfaceAlias | Format-Table InterfaceAlias, IPAddress, PrefixLength
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-2.png)

Hyper-v 仮想スイッチと、物理ネットワークアダプターのチーミング方法を確認するには、次の手順を実行します。

```PowerShell
Get-VMSwitch
Get-VMSwitchTeam
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-3.png)

ホスト仮想ネットワークアダプターを表示するには、次のように実行します。

```PowerShell
Get-VMNetworkAdapter -ManagementOS | Format-Table Name, IsManagementOS, SwitchName
Get-VMNetworkAdapterTeamMapping -ManagementOS | Format-Table NetAdapterName, ParentAdapter
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-4.png)

現在のフェールオーバークラスターとそのメンバーノードを表示するには、次のように実行します。

```PowerShell
Get-Cluster
Get-ClusterNode
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-5.png)

記憶域スペースダイレクトが有効になっているかどうか、および既定の記憶域プールが自動的に作成されているかどうかを確認するには:

```PowerShell
Get-ClusterStorageSpacesDirect
Get-StoragePool -IsPrimordial $False
```

![PowerShell の出力のスクリーンショット](../media/deploy-hyperconverged-infrastructure/script-out-6.png)

## <a name="undo-and-start-over"></a>元に戻すとやり直す

これらの Windows PowerShell コマンドレットを使用して、ワークフローによって行われた変更を元に戻し、やり直すことができます。

### <a name="remove-virtual-machines-or-other-clustered-resources"></a>仮想マシンまたはその他のクラスター化されたリソースを削除する

ソフトウェアで定義されたネットワーク用のネットワークコントローラーなど、仮想マシンまたはその他のクラスター化されたリソースを作成した場合は、最初にそれらを削除します。

たとえば、名前によってリソースを削除するには、次のように指定します。

```PowerShell
Get-ClusterResource -Name "<NAME>" | Remove-ClusterResource
```

### <a name="undo-the-storage-steps"></a>ストレージの手順を元に戻す

記憶域スペースダイレクトを有効にした場合は、次のスクリプトを使用して無効にします。

> [!Warning]
> これらのコマンドレットは記憶域スペースダイレクトボリューム内のデータを完全に削除します。 これを元に戻すことはできません。

```PowerShell
Get-VirtualDisk | Remove-VirtualDisk
Get-StoragePool -IsPrimordial $False | Remove-StoragePool
Disable-ClusterS2D
```

### <a name="undo-the-clustering-steps"></a>クラスタリングの手順を元に戻す

クラスターを作成した場合は、次のコマンドレットを使用して削除します。

```PowerShell
Remove-Cluster -CleanUpAD
```

クラスター検証レポートも削除するには、クラスターの一部であったすべてのサーバーで次のコマンドレットを実行します。

```PowerShell
Get-ChildItem C:\Windows\cluster\Reports\ | Remove-Item
```

### <a name="undo-the-networking-steps"></a>ネットワークの手順を元に戻す

クラスターに含まれていたすべてのサーバーでこれらのコマンドレットを実行します。

Hyper-v 仮想スイッチを作成した場合は、次のようになります。

```PowerShell
Get-VMSwitch | Remove-VMSwitch
```

> [!Note]
> `Remove-VMSwitch` コマンドレットは、仮想アダプターを自動的に削除し、物理アダプターのスイッチ埋め込みチーミングを元に戻します。

名前、IPv4 アドレス、VLAN ID などのネットワークアダプターのプロパティを変更した場合は、次のようになります。

> [!Warning]
> これらのコマンドレットは、ネットワークアダプターの名前と IP アドレスを削除します。 次のスクリプトから除外された管理用アダプターなど、後で接続するために必要な情報があることを確認します。 また、Windows でのアダプターの名前だけでなく、MAC アドレスなどの物理プロパティに関して、サーバーがどのように接続されているかを確認してください。

```PowerShell
Get-NetAdapter | Where Name -Ne "Management" | Rename-NetAdapter -NewName $(Get-Random)
Get-NetAdapter | Where Name -Ne "Management" | Get-NetIPAddress -ErrorAction SilentlyContinue | Where AddressFamily -Eq IPv4 | Remove-NetIPAddress
Get-NetAdapter | Where Name -Ne "Management" | Set-NetAdapter -VlanID 0
```

これで、ワークフローを開始する準備ができました。

## <a name="feedback"></a>Feedback

このプレビューリリースでは、お客様のご意見をお寄せください。 チームに連絡を取るための方法をいくつか次に示します。

- [UserVoice で機能要求を送信して投票する](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft Tech Community で Windows 管理センターフォーラムに参加する](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- Email hci-展開 [at] microsoft.com
- [@servermgmt](https://twitter.com/servermgmt)にツイート

## <a name="report-an-issue"></a>問題を報告する

上に示したチャネルを使用して、クラスター作成ワークフローの問題を報告します。

可能であれば、問題を迅速に再現して解決するために、次の情報を含めてください。

- 選択したクラスターの種類 (例: *"ハイパー収束"* )
- 問題が発生したステップ (例: *"3.2 クラスターの作成"* )
- クラスター作成拡張機能のバージョン。 **設定** > **拡張**機能 > **インストールされている拡張機能** にアクセスし、**バージョン** 列 (例: *"1.0.30"* ) を参照します。
- エラーメッセージ。画面上またはブラウザーコンソールで、 **F12**キーを押して開くことができます。
- 環境に関するその他の関連情報 

## <a name="see-also"></a>関連項目

- [Hello, Windows 管理センター](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)
- [記憶域スペース ダイレクトの展開](https://docs.microsoft.com/windows-server/storage/storage-spaces/deploy-storage-spaces-direct)
