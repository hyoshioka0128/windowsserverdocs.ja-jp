---
title: HYPER-V での FreeBSD の実行に関するベスト プラクティス
description: 仮想マシンを FreeBSD を実行するための推奨事項を提供します。
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
ms.openlocfilehash: 6320ceb86093146592a54ab34b013f334f43ddb4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447774"
---
# <a name="best-practices-for-running-freebsd-on-hyper-v"></a>HYPER-V での FreeBSD の実行に関するベスト プラクティス

>適用先:Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

このトピックには、ゲスト オペレーティング システムとして、HYPER-V 仮想マシンを FreeBSD を実行するための推奨事項の一覧が含まれています。

## <a name="enable-carp-in-freebsd-102-on-hyper-v"></a>HYPER-V で FreeBSD 10.2 で CARP を有効にします。

一般的なアドレス冗長性プロトコル (CARP) は、同じ IP アドレスを共有する複数のホストと仮想ホスト ID (v. 付録) 1 つまたは複数のサービスの高可用性を確保するために使用できます。 1 つまたは複数のホストが失敗した場合、他のホストに透過的に引き継ぐため、ユーザーは、サービスのエラーを確認できません。FreeBSD 10.2 で CARP を使用する手順については、 [FreeBSD ハンドブック](https://www.freebsd.org/doc/en/books/handbook/carp.html)HYPER-V マネージャーでは、次の操作を行います。

* 仮想マシンがネットワーク アダプターと仮想スイッチが割り当てられていることを確認します。 仮想マシンを選択し、選択**アクション** > **設定**します。

![ネットワーク アダプターが選択された状態の仮想マシンの設定のスクリーン ショット](media/Hyper-V_Settings_NetworkAdapter.png)

* MAC アドレスのスプーフィングを有効にします。 そのためには、次の手順を実行します。

   1. 仮想マシンを選択し、選択**アクション** > **設定**します。

   2. 展開**ネットワーク アダプター**選択**高度な機能**します。

   3. 選択**を有効にする MAC アドレスのスプーフィング**します。

## <a name="create-labels-for-disk-devices"></a>ディスク デバイスのラベルを作成します。

起動時に、新しいデバイスが検出されると、デバイス ノードが作成されます。 これにより、新しいデバイスが追加されたときに、デバイス名を変更できることを意味します。 スタートアップ中に、ルートのマウント エラーが発生した場合は、競合と変更を回避するために IDE パーティションごとにラベルを作成する必要があります。 学習する方法についてを参照してください[ディスク デバイスのラベル付け](https://www.freebsd.org/doc/handbook/geom-glabel.html)します。 次の例に示します。 

> [!IMPORTANT]
> 変更を加える前に、fstab のバックアップ コピーを作成します。

1. シングル ユーザー モードには、システムを再起動します。 FreeBSD 10.3 以降のブート メニュー オプション 2 を選択してこれを実現することができます (FreeBSD のオプション 4 8.x)、または 'ブート-s' のブート プロンプトから実行します。

2. シングル ユーザー モードでは、各 fstab (ルートとスワップ) で表示されている IDE ディスク パーティションのジオメトリのラベルを作成します。 FreeBSD 10.3 の例を次に示します。

   ```bash
   # cat  /etc/fstab
   # Device           Mountpoint      FStype  Options   Dump   Pass#
   /dev/da0p2         /               ufs     rw        1       1
   /dev/da0p3         none            swap    sw        0       0

   # glabel  label rootfs  /dev/da0p2
   # glabel  label swap   /dev/da0p3
   # exit
   ```

   ジオメトリのラベルの詳細についてにあります。[ディスク デバイスをラベル付け](https://www.freebsd.org/doc/handbook/geom-glabel.html)します。

3. システムについては、マルチ ユーザー ブートに進みます。 起動が完了したら後、は、/etc/fstab を編集しますし、従来のデバイス名をそれぞれのラベルに置き換えます。 最終的な/etc/fstab は、次のようになります。

   ```
   # Device                Mountpoint      FStype  Options         Dump    Pass#
   /dev/label/rootfs       /               ufs     rw              1       1
   /dev/label/swap         none            swap    sw              0       0
   ```

4. システムを再起動するようになりましたことができます。 すべてがうまく場合は、通常ものがマウントが表示されます。

   ```
   # mount
   /dev/label/rootfs on / (ufs, local, journaled soft-updates)
   devfs on /dev (devfs, local, mutilabel)
   ```

## <a name="use-a-wireless-network-adapter-as-the-virtual-switch"></a>ワイヤレス ネットワーク アダプターを仮想スイッチとして使用します。

ホスト上の仮想スイッチは、ワイヤレス ネットワーク アダプターに基づいている場合は、次のコマンドで 60 秒に ARP 有効期限時間を短縮します。 それ以外の場合、VM のネットワー キングは、しばらくすると動作を停止する可能性があります。


```
   # sysctl net.link.ether.inet.max_age=60
```


関連項目

* [Hyper-v のサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)
