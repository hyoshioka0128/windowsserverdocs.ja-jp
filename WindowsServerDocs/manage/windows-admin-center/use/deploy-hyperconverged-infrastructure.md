---
title: Windows 管理センターを使用してハイパー集約インフラストラクチャを展開する
ms.topic: article
author: cosmosdarwin
ms.author: cosdar
ms.date: 11/04/2019
ms.openlocfilehash: 06062f4add54fda3ddcda4d092d6eaf1d692ebf8
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993490"
---
# <a name="deploy-hyperconverged-infrastructure-with-windows-admin-center"></a>Windows 管理センターを使用してハイパー集約インフラストラクチャを展開する

> 適用先:Windows Admin Center、Windows Admin Center Preview

Windows 管理センター[バージョン 1910](../overview.md)以降を使用して、2つ以上の適切な windows サーバーを使用してハイパー集約インフラストラクチャを展開することができます。 この新しい機能では、機能のインストール、ネットワークの構成、クラスターの作成、記憶域スペースダイレクトまたはソフトウェアによるネットワーク制御 (SDN) の展開など、選択した場合に役立つマルチステージワークフローの形式を使用します。

Windows 管理センターバージョン2007以降では、Windows 管理センターでは Azure Stack HCI OS がサポートされています。 [Windows 管理センターでクラスターを展開する方法については、AZURE STACK HCI のドキュメント](/azure-stack/hci/getting-started)を参照してください。このドキュメントでは Azure Stack HCI に焦点を合わせています。この手順は、Windows Server の展開にも適しています。

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
> `Remove-VMSwitch`コマンドレットは、仮想アダプターを自動的に削除し、物理アダプターのスイッチ埋め込みチーミングを元に戻します。

名前、IPv4 アドレス、VLAN ID などのネットワークアダプターのプロパティを変更した場合は、次のようになります。

> [!Warning]
> これらのコマンドレットは、ネットワークアダプターの名前と IP アドレスを削除します。 次のスクリプトから除外された管理用アダプターなど、後で接続するために必要な情報があることを確認します。 また、Windows でのアダプターの名前だけでなく、MAC アドレスなどの物理プロパティに関して、サーバーがどのように接続されているかを確認してください。

```PowerShell
Get-NetAdapter | Where Name -Ne "Management" | Rename-NetAdapter -NewName $(Get-Random)
Get-NetAdapter | Where Name -Ne "Management" | Get-NetIPAddress -ErrorAction SilentlyContinue | Where AddressFamily -Eq IPv4 | Remove-NetIPAddress
Get-NetAdapter | Where Name -Ne "Management" | Set-NetAdapter -VlanID 0
```

これで、ワークフローを開始する準備ができました。

## <a name="additional-references"></a>その他の参照情報

- [Hello, Windows 管理センター](../overview.md)
- [記憶域スペース ダイレクトの展開](../../../storage/storage-spaces/deploy-storage-spaces-direct.md)