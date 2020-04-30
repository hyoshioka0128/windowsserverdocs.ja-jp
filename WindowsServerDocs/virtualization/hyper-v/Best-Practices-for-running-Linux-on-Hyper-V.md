---
title: HYPER-V で Linux を実行するためのベスト プラクティス
description: 仮想マシンで Linux を実行するための推奨事項を提供します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 04/15/2020
ms.openlocfilehash: d8861369abe24ea0d34dce209a5d98e854c4c95d
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82072238"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>HYPER-V で Linux を実行するためのベスト プラクティス

>適用対象: Windows Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows Server 2012、Hyper-v Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7。

このトピックには、Hyper-v で Linux 仮想マシンを実行するための推奨事項の一覧が含まれています。

## <a name="tuning-linux-file-systems-on-dynamic-vhdx-files"></a>動的 VHDX ファイルでの Linux ファイルシステムのチューニング

一部の Linux ファイルシステムは、ファイルシステムがほとんど空の場合でも、大量の実際のディスク領域を消費することがあります。 動的な VHDX ファイルの実際のディスク領域の使用量を減らすには、次の推奨事項を考慮してください。

* VHDX を作成するときは、PowerShell で 1 MB のブロック Sizebytes (既定の32MB から) を使用します。次に例を示します。

```Powershell
PS > New-VHD -Path C:\MyVHDs\test.vhdx -SizeBytes 127GB -Dynamic -BlockSizeBytes 1MB
```

* Ext4 形式は、動的な VHDX ファイルを使用する場合に、ext4 は ext3 よりもはるかに効率的であるため、ext3 にお勧めします。

* ファイルシステムを作成するときは、グループの数を4096に指定します。次に例を示します。

```bash
# mkfs.ext4 -G 4096 /dev/sdX1

```

## <a name="grub-menu-timeout-on-generation-2-virtual-machines"></a>第2世代の Grub メニューのタイムアウト Virtual Machines

レガシハードウェアは第2世代仮想マシンのエミュレーションから削除されるので、grub メニューのカウントダウンは短すぎるため、既定のエントリがすぐに読み込まれます。 EFI がサポートされているタイマーを使用するように grub が修正されるまでは、 **/boot/grub/grub.conf**、/**etc/default/grub**を変更するか、それと同等のものを既定の "timeout = 5" ではなく "timeout = 100000" に設定します。

## <a name="pxe-boot-on-generation-2-virtual-machines"></a>第2世代の PxE ブート Virtual Machines

PIT タイマーは第2世代 Virtual Machines には存在しないため、PxE TFTP サーバーへのネットワーク接続が途中で終了し、ブートローダーが Grub 構成を読み取らず、サーバーからカーネルが読み込まれないようにすることができます。

RHEL 6.x では、次に示すように、従来の grub v 0.97 EFI ブートローダーを grub2 の代わりに使用できます。[https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

RHEL 6.x 以外の Linux ディストリビューションでは、同様の手順に従って、PxE サーバーから Linux カーネルを読み込むように grub v 0.97 を構成できます。

さらに、RHEL/CentOS 6.6 キーボードおよびマウス入力は、インストール前のカーネルで機能しません。これにより、メニューにインストールオプションを指定できなくなります。 シリアルコンソールは、インストールオプションの選択を許可するように構成する必要があります。

* PxE サーバーの**efidefault**ファイルで、次のカーネルパラメーター **"console = ttyS1"** を追加します。

* Hyper-v の VM で、次の PowerShell コマンドレットを使用して COM ポートを設定します。

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

Kickstart ファイルをプレインストールカーネルに指定すると、インストール時のキーボード入力とマウス入力の必要もなくなります。

## <a name="use-static-mac-addresses-with-failover-clustering"></a>フェールオーバークラスタリングで静的 MAC アドレスを使用する

フェールオーバークラスタリングを使用してデプロイされる Linux 仮想マシンは、各仮想ネットワークアダプターに対して静的なメディアアクセス制御 (MAC) アドレスを使用して構成する必要があります。 Linux の一部のバージョンでは、新しい MAC アドレスが仮想ネットワークアダプターに割り当てられるため、フェールオーバー後にネットワーク構成が失われる可能性があります。 ネットワーク構成が失われないようにするには、各仮想ネットワークアダプターに静的 MAC アドレスがあることを確認します。 MAC アドレスを構成するには、Hyper-v マネージャーまたはフェールオーバークラスターマネージャーでバーチャルマシンの設定を編集します。

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>レガシネットワークアダプターではなく、Hyper-v 固有のネットワークアダプターを使用する

仮想イーサネットアダプターを構成して使用します。これは、パフォーマンスが向上した Hyper-v 固有のネットワークカードです。 レガシおよび Hyper-v 固有のネットワークアダプターの両方が仮想マシンに接続されている場合、 **ifconfig**の出力に含まれるネットワーク名に、 **_tmp12000801310**などのランダムな値が表示されることがあります。 この問題を回避するには、Linux 仮想マシンで Hyper-v 固有のネットワークアダプターを使用するときに、すべてのレガシネットワークアダプターを削除します。

## <a name="use-io-scheduler-noopnone-for-better-disk-io-performance"></a>ディスク i/o パフォーマンスを向上させるには、i/o scheduler noop/none を使用します。

Linux カーネルには、要求の順序を変更するための2セットのディスク i/o スケジューラが用意されています。  1つは古い ' blk ' サブシステム用で、もう1つは新しい "blk" サブシステム用です。 どちらの場合も、現在のソリッドステートディスクでは、スケジュールの決定を基になる Hyper-v ハイパーバイザーに渡すスケジューラを使用することをお勧めします。 "Blk" サブシステムを使用する Linux カーネルの場合、これは "noop" スケジューラです。 "Blk" サブシステムを使用する Linux カーネルの場合、これは "none" スケジューラです。

特定のディスクの場合、使用可能なスケジューラは、現在選択されているスケジューラが角かっこで囲ま`<diskname>`れた、次のファイルシステムの場所で確認できます。 このファイルシステムの場所に書き込むことで、スケジューラを変更できます。 再起動の間に保持するために、変更を初期化スクリプトに追加する必要があります。 詳細については、Linux ディストリビューションのドキュメントを参照してください。

## <a name="numa"></a>NUMA

2.6.37 未満の Linux カーネル バージョンは、HYPER-V で大きい VM サイズの NUMA をサポートできません。 この問題は、主に、アップストリームの Red Hat 2.6.32 カーネルを使用した古いディストリビューションに影響し、Red Hat Enterprise Linux (RHEL) 6.6 (kernel-2.6.32-504) で修正されました。 2.6.37 より古いカスタム カーネルまたは2.6.32-504 より古い RHEL ベースのカーネルを実行しているシステムでは、grub.conf のカーネル コマンドラインで、ブート パラメーター `numa=off` を設定する必要があります。 詳細については、[Red Hat KB 436883](https://access.redhat.com/solutions/436883) を参照してください。

## <a name="reserve-more-memory-for-kdump"></a>Kdump 用に追加のメモリを予約する

ダンプキャプチャカーネルが起動時にパニックに陥る場合は、カーネル用により多くのメモリを予約します。 たとえば、Ubuntu の grub 構成ファイルで、パラメーター **crashkernel = 384 m-: 128m**を**crashkernel = 384 M-: 256 m**に変更します。

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>VHDX を圧縮したり、VHD および VHDX ファイルを拡張すると、GPT パーティションテーブルにエラーが発生する可能性があります

Hyper-v では、ディスク上に存在する可能性のあるパーティション、ボリューム、またはファイルシステムのデータ構造に関係なく、仮想ディスク (VHDX) ファイルを圧縮できます。 Vhdx がパーティションの最後より前の場所に圧縮されると、データが失われたり、パーティションが破損したり、パーティションが読み取られたときに無効なデータが返されたりする可能性があります。

VHD または VHDX のサイズを変更した後、管理者は、fdisk や parted などのユーティリティを使用して、パーティション、ボリューム、ファイルシステムの構造を更新し、ディスクのサイズの変化を反映する必要があります。 GUID パーティションテーブル (GPT) を持つ VHD または VHDX のサイズを縮小または拡大すると、パーティション管理ツールを使用してパーティションのレイアウトを確認したときに警告が表示され、管理者は1つ目と2番目の GPT ヘッダーを修正するように警告されます。 この手動の手順は、データ損失なしでも安全に実行できます。

## <a name="see-also"></a>関連項目

* [Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [HYPER-V での FreeBSD の実行に関するベスト プラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [Hyper-V クラスターを展開する](https://technet.microsoft.com/library/jj863389.aspx)

* [Azure の Linux イメージを作成する](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)

* [Azure での Linux VM の最適化](https://docs.microsoft.com/azure/virtual-machines/linux/optimization)
