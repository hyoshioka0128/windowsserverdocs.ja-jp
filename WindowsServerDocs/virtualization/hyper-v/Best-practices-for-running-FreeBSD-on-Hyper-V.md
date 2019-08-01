---
title: HYPER-V での FreeBSD の実行に関するベスト プラクティス
description: 仮想マシンでの FreeBSD の実行に関する推奨事項について説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c66f1c8-2606-43a3-b4cc-166acaaf2d2a
author: shirgall
ms.author: kathydav
ms.date: 01/09/2017
ms.openlocfilehash: 598087411b35dde2e4a1cb606fae6a4602fe588e
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544684"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>HYPER-V での FreeBSD の実行に関するベスト プラクティス

>適用先:Windows Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows Server の2012、Hyper-v Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

このトピックでは、Hyper-v 仮想マシンでゲストオペレーティングシステムとして FreeBSD を実行する場合の推奨事項の一覧を示します。

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>Hyper-v で FreeBSD 10.2 の CARP を有効にする

共通アドレス冗長プロトコル (CARP) を使用すると、複数のホストが同じ IP アドレスと仮想ホスト ID (VHID) を共有して、1つ以上のサービスの高可用性を実現するのに役立ちます。 1つまたは複数のホストで障害が発生した場合、他のホストは透過的に処理されるため、ユーザーはサービスの障害に気付くことはありません。FreeBSD 10.2 で CARP を使用するには、 [freebsd ハンドブック](https://www.freebsd.org/doc/en/books/handbook/carp.html)に記載されている手順に従って、hyper-v マネージャーで次の操作を実行します。

* 仮想マシンにネットワークアダプターがあり、仮想スイッチが割り当てられていることを確認します。 仮想マシンを選択し、[**アクション** > の**設定**] を選択します。

![ネットワークアダプターが選択されている仮想マシンの設定のスクリーンショット](media/Hyper-V_Settings_NetworkAdapter.png)

* MAC アドレスのスプーフィングを有効にします。 そのためには、次の手順を実行します。

   1. 仮想マシンを選択し、[**アクション** > の**設定**] を選択します。

   2. **[ネットワークアダプター]** を展開し、 **[高度な機能]** を選択します。

   3. **[MAC アドレスのスプーフィングを有効にする]** を選択します。

## <a name="create-labels-for-disk-devices"></a>ディスクデバイスのラベルを作成する

デバイスノードは、起動時に新しいデバイスが検出されると作成されます。 これは、新しいデバイスを追加したときにデバイス名が変更される可能性があることを意味します。 起動時にルートマウントエラーが発生した場合は、競合や変更を回避するために、各 IDE パーティションのラベルを作成する必要があります。 詳細については、「[ディスクデバイスのラベル付け](https://www.freebsd.org/doc/handbook/geom-glabel.html)」を参照してください。 次に例を示します。 

> [!IMPORTANT]
> Fstab のバックアップコピーを作成してから、変更を加えてください。

1. システムをシングルユーザーモードで再起動します。 これを行うには、FreeBSD 10.3 + のブートメニューオプション 2 (FreeBSD 2.x のオプション 4) を選択するか、ブートプロンプトから ' boot s ' を実行します。

2. シングルユーザーモードで、fstab (root と swap の両方) に一覧表示されている IDE ディスクパーティションごとにジオメトリラベルを作成します。 FreeBSD 10.3 の例を次に示します。

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   ジオメトリラベルの追加情報については、以下を参照してください。[ディスクデバイスにラベル](https://www.freebsd.org/doc/handbook/geom-glabel.html)を付ける。

3. システムはマルチユーザーブートを続行します。 ブートが完了したら、/etc/fstab を編集し、従来のデバイス名をそれぞれのラベルに置き換えます。 最後の/etc/fstab は次のようになります。

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0
   ```

4. システムを再起動できるようになりました。 すべて問題なく実行されると、正常に起動し、mount には次のように表示されます。

   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>ワイヤレスネットワークアダプターを仮想スイッチとして使用する

ホスト上の仮想スイッチがワイヤレスネットワークアダプターに基づいている場合は、次のコマンドで ARP の有効期限を60秒に減らします。 そうしないと、しばらくすると VM のネットワークが動作しなくなる可能性があります。


```
   # sysctl net.link.ether.inet.max_age=60
```


関連項目

* [Hyper-v でサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
