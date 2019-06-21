---
title: HYPER-V で Linux を実行するためのベスト プラクティス
description: 仮想マシンで Linux を実行するための推奨事項を提供します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a08648eb-eea0-4e2b-87fb-52bfe8953491
author: shirgall
ms.author: kathydav
ms.date: 3/1/2019
ms.openlocfilehash: a24e2b1a1d79d52c1cc16f9e7c1b253d9b477aae
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284439"
---
# <a name="best-practices-for-running-linux-on-hyper-v"></a>HYPER-V で Linux を実行するためのベスト プラクティス

>適用先:Windows Server 2019、Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

このトピックには、HYPER-V で Linux 仮想マシンを実行するための推奨事項の一覧が含まれています。

## <a name="tuning-linux-file-systems-on-dynamic-vhdx-files"></a>動的な VHDX ファイル上の Linux ファイル システムのチューニング

一部の Linux ファイル システムは、ファイル システムがほぼ空の場合でも、大量の実際のディスク領域を消費する可能性があります。 動的な VHDX ファイルの実際のディスク領域の使用量を減らすためには、次の推奨事項を考慮してください。

* VHDX を作成するときに、たとえば PowerShell では、(既定値は 32 MB である) から 1 MB BlockSizeBytes を使用します。

```Powershell
PS > New-VHD -Path C:\MyVHDs\test.vhdx -SizeBytes 127GB -Dynamic -BlockSizeBytes 1MB
```

* Ext4 形式は、ext4 が ext3 動的 VHDX ファイルで使用する場合よりも容量効率のため、ext3 を優先。

* ときに、ファイル システムを作成するは、4096、たとえばするグループの数を指定します。

```bash
# mkfs.ext4 -G 4096 /dev/sdX1

```

## <a name="grub-menu-timeout-on-generation-2-virtual-machines"></a>第 2 世代仮想マシンの grub メニュー タイムアウト

レガシ ハードウェアのエミュレーションを第 2 世代仮想マシンから削除されるため、grub] メニューの [カウント ダウン タイマー カウント ダウンが早すぎる grub メニューが表示され、すぐに、既定のエントリを読み込みします。 Grub が EFI でサポートされているタイマーを使用する固定されるまで変更 **/boot/grub/grub.conf**、/**など/etc/default/grub**、または同等が"タイムアウト = 100000"、既定ではなく"タイムアウト = 5"。

## <a name="pxe-boot-on-generation-2-virtual-machines"></a>第 2 世代仮想マシン上の PxE ブート

PIT タイマーが Generation 2 Virtual Machines 内に存在しないため、PxE TFTP サーバーへのネットワーク接続が途中で終了して、Grub 構成を読み取って、サーバーからのカーネルの読み込みからブートローダーを防ぐため。

On RHEL 6.x、」の説明に従って、grub2 ではなく従来の grub v0.97 EFI ブート ローダーを使用できます。 [https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/s1-netboot-pxe-config-efi.html)

RHEL 以外の Linux ディストリビューションで 6.x、同様の手順の後に Linux カーネルに PxE サーバーから読み込めません grub v0.97 を構成できます。

さらに、RHEL と CentOS 6.6 キーボードとマウスの入力では機能しませんが原因のインストール前のカーネル、メニューでのインストール オプションを指定します。 シリアル コンソールは、インストール オプションを選択することを許可するように構成する必要があります。

* **Efidefault** 、PxE サーバーのファイルに追加し、次のカーネル パラメーター **"コンソール ttyS1 ="**

* Vm、HYPER-V で、次の PowerShell コマンドレットを使用して COM ポートをセットアップします。

```Powershell
Set-VMComPort -VMName <Name> -Number 2 -Path \\.\pipe\dbg1

```

インストールする前のカーネルに kickstart ファイルを指定すると、キーボードとマウスのインストール時に入力の必要性もしないでください。

## <a name="use-static-mac-addresses-with-failover-clustering"></a>静的 MAC アドレスを使用して、フェールオーバー クラスタ リング

フェールオーバー クラスタ リングを使用して展開される Linux 仮想マシンは、各仮想ネットワーク アダプターの静的メディア アクセス制御 (MAC) アドレスで構成する必要があります。 Linux のいくつかのバージョンでは、ネットワークの構成が失わフェールオーバー後に、新しい MAC アドレスが仮想ネットワーク アダプターに割り当てられるためです。 ネットワーク構成を失うことを回避するには、各仮想ネットワーク アダプターに静的 MAC アドレスがあることを確認します。 MAC アドレスを構成するには、HYPER-V マネージャーまたはフェールオーバー クラスター マネージャーで仮想マシンの設定を編集します。

## <a name="use-hyper-v-specific-network-adapters-not-the-legacy-network-adapter"></a>レガシ ネットワーク アダプターではなく、ハイパー V 固有ネットワーク アダプターを使用します。

構成し、パフォーマンスが向上したハイパー V 固有ネットワーク カードは、仮想イーサネット アダプターを使用します。 レガシとハイパー V 固有ネットワーク アダプターの両方が仮想マシンに接続されている場合、ネットワーク名の出力**ifconfig-a**など、ランダムな値を表示する場合があります **_tmp12000801310**します。 この問題を回避するには、Linux 仮想マシンでのハイパー V 固有ネットワーク アダプターを使用する場合、すべてのレガシ ネットワーク アダプターを削除します。

## <a name="use-io-scheduler-noop-for-better-disk-io-performance"></a>I/O スケジューラが NOOP を使用して、良いディスク I/O パフォーマンス

Linux カーネルでは、さまざまなアルゴリズムの要求の順序を変更する 4 つのさまざまな I/O スケジューラが。 NOOP は、スケジュールの決定、ハイパーバイザーによってを通過する先入れ先出しキューです。 Linux 仮想マシンを HYPER-V で実行されている場合、スケジューラとして NOOP を使用することをお勧めします。 ブート ローダーの構成では、特定のデバイスのスケジューラを変更する (/例については、etc/grub.conf)、追加**エレベーター = noop**カーネル パラメーター、および再起動します。

## <a name="numa"></a>NUMA

Linux カーネルのバージョン以前 2.6.37 よりもサポートされていません NUMA hyper-v で大きい VM サイズ。 これは、問題を主に影響、アップ ストリームを使用した古いディストリビューション Red Hat 2.6.32 カーネルをし、Red Hat Enterprise Linux (RHEL) 6.6 (カーネル 2.6.32 504) が修正されました。 ブート パラメーターを設定する必要があります 2.6.32-504 より 2.6.37 より古いカスタム カーネルまたは古い RHEL ベースのカーネルを実行しているシステム`numa=off`grub.conf のカーネル コマンドラインでします。 詳細については、次を参照してください。 [Red Hat KB 436883](https://access.redhat.com/solutions/436883)します。

## <a name="reserve-more-memory-for-kdump"></a>Kdump のより多くのメモリを予約します。

起動時にパニックと最終的に、ダンプのキャプチャ カーネル、場合に、カーネルのより多くのメモリを予約します。 パラメーターを変更するなど、 **crashkernel = 384M-:128M**に**crashkernel = 384M-:256M** Ubuntu grub の構成ファイルでします。

## <a name="shrinking-vhdx-or-expanding-vhd-and-vhdx-files-can-result-in-erroneous-gpt-partition-tables"></a>VHDX を圧縮または VHD および VHDX ファイルを展開するが、誤った GPT パーティション テーブルで発生します。

HYPER-V は、任意のパーティション、ボリューム、またはディスクに存在するファイル システムのデータ構造に関係なく、仮想ディスク (VHDX) ファイルを圧縮できます。 パーティションの終了前に VHDX の末尾が登場する VHDX を圧縮する場合は、データが失われることができます、パーティションのデータが壊れているか、または無効なことになることが返されること、パーティションは読み取り専用します。

VHD または VHDX のサイズを変更した後は、管理者は、fdisk などのユーティリティを使用する必要があります。 または、パーティション、ボリューム、およびディスクのサイズの変更を反映するようにファイル システムの構造を更新するため。 パーティションの管理ツールを使用して、パーティション レイアウトをチェックし、管理者の最初とセカンダリの GPT ヘッダーを修正する警告が表示されますが圧縮または拡張 VHD または VHDX を GUID パーティション テーブル (GPT) を持つのサイズに警告を発生します。 この手動の手順では、データ損失のない実行にも安全です。

## <a name="see-also"></a>関連項目

* [Windows 上の HYPER-V ではサポートされている Linux および FreeBSD 仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

* [HYPER-V で FreeBSD を実行するためのベスト プラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)

* [HYPER-V クラスターをデプロイします。](https://technet.microsoft.com/library/jj863389.aspx)

* [Azure の Linux イメージを作成します。](https://docs.microsoft.com/azure/virtual-machines/linux/create-upload-generic)

* [Azure で Linux VM を最適化します。](https://docs.microsoft.com/azure/virtual-machines/linux/optimization)
