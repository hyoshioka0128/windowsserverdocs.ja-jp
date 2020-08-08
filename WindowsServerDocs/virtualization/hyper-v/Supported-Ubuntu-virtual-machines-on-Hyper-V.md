---
title: HYPER-V でサポートされている Ubuntu 仮想マシン
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
manager: dongill
ms.topic: article
ms.assetid: 95ea5f7c-25c6-494b-8ffd-2a77f631ee94
author: shirgall
ms.author: shirgall
ms.date: 04/08/2020
ms.openlocfilehash: 88d5659bb4732c82cc7ecc5e4a5e806f4b984739
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989314"
---
# <a name="supported-ubuntu-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている Ubuntu 仮想マシン

>適用対象: Windows Server 2019、Hyper-v Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows 10、および Windows 8.1

次の機能の配布マップでは、各バージョンの機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

## <a name="table-legend"></a>表の凡例

* **組み込まれている** に LIS がこの Linux ディストリビューションの一部として含まれています。 インストールされないように、この配布では、Microsoft 提供の LIS のダウンロード パッケージは機能しません。 組み込みの LIS のカーネル モジュールのバージョン番号 (に示すように **lsmod**, 、たとえば) マイクロソフト提供の LIS のダウンロード パッケージにバージョン番号とは異なります。 組み込みの LIS の項目が古いことに不一致が示されません。

* & #10004 です。の機能使用

* (*空白*) の機能は使用できません

|**機能**|**Windows Server オペレーティング システムのバージョン**|**19.10**|**18.04 LTS**|**16.04 LTS**|**14.04 LTS**|
|-|-|-|-|-|-|
|**可用性**||組み込み|組み込み|組み込み|組み込み|
|**[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 の正確な時刻|2019、2016|&#10004;|&#10004;|&#10004;||
|**[ネットワーク](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||
|Jumbo Frame|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN のタグ付けとトランキング|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2019、2016、2012 R2|& #10004 です。注 1|& #10004 です。注 1|& #10004 です。注 1|& #10004 です。注 1|
|vRSS|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|TCP セグメント化とチェックサムのオフロード|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|SR-IOV|2019、2016|&#10004;|&#10004;|&#10004;||
|**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**|||||
|VHDX のサイズ変更|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|仮想ファイバー チャネル|2019、2016、2012 R2|& #10004 です。注 2|& #10004 です。注 2|& #10004 です。注 2|& #10004 です。注 2|
|仮想マシンのライブバックアップ|2019、2016、2012 R2|&#10004; メモ3、4、6|& #10004 です。3, 4, 5 に注意してください。|& #10004 です。3, 4, 5 に注意してください。|& #10004 です。3, 4, 5 に注意してください。|
|トリムのサポート|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|SCSI WWN|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|**[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|||||
|PAE カーネルサポート|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|MMIO ギャップの構成|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2019、2016、2012 R2|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|
|動的メモリ - バルーニング|2019、2016、2012 R2|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|& #10004 です。7, 8, 9 に注意してください。|
|ランタイムのメモリのサイズ変更|2019、2016|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||
|HYPER-V で特定のビデオ デバイス|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|**[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|||||
|キーと値のペア|2019、2016、2012 R2|&#10004; メモ6、10|& #10004 です。注 5、10|& #10004 です。注 5、10|& #10004 です。注 5、10|
|マスクなしの割り込み|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|ホストからゲストへのファイルのコピー|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|lsvmbus コマンド|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|
|Hyper V ソケット|2019、2016|||||
|PCI パススルー/DDA|2019、2016|&#10004;|&#10004;|&#10004;|&#10004;|
|**[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|||||
|UEFI を使用したブート|2019、2016、2012 R2|& #10004 です。注 11、12|& #10004 です。注 11、12|& #10004 です。注 11、12|& #10004 です。注 11、12|
|セキュア ブート|2019、2016|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="notes"></a>メモ

1. 静的 IP インジェクションが機能しなくなる **ネットワーク マネージャー** が仮想マシン上の指定したハイパー V 固有ネットワーク アダプターに対して構成されています。 静的 IP の円滑に機能することを確認するインジェクションを確認してくださいネットワーク マネージャーが完全にオフや、オフになっているを使って特定のネットワーク アダプターにその **ifcfg ethX** ファイルです。

2. 仮想ファイバー チャネル デバイスを使用している論理ユニット番号 (LUN 0) を 0 に設定されていることを確認します。 LUN 0 が設定されていません Linux 仮想マシンは、ファイバー チャネル デバイスをネイティブにマウントすることができません。

3. 開いている場合に、仮想マシンのバックアップ操作中にファイルを処理し、いくつかのコーナー ケースでバックアップされる Vhd は、ファイル システムの整合性チェックを行う必要があります (`fsck`) のサイズに戻す。

4. ライブ バックアップ操作がエラーに何も行わずに、仮想マシンに接続された iSCSI デバイスまたは直接接続ストレージ (パススルー ディスクとも呼ばれます) がある場合。

5. 長期的なサポートでは、(LTS) のリリースは、最新の Linux Integration Services の最新バージョンの仮想ハードウェア支援 (HWE) カーネルを使用します。

   14.04、16.04、および18.04 に Azure でチューニングされたカーネルをインストールするには、root (または sudo) として次のコマンドを実行します。

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

6. Ubuntu 19.10 では、最新の仮想カーネルを使用して最新の Hyper-v 機能を利用できます。

   19.10 に仮想カーネルをインストールするには、ルート (または sudo) として次のコマンドを実行します。

   ```bash
   # apt-get update
   # apt-get install linux-azure
   ```

   カーネルが更新されるたびに、それを使用する、仮想マシンを再起動する必要があります。

7. 動的メモリのサポートは、64 ビット仮想マシンで使用できるのみです。

8. 動的メモリの操作は、ゲスト オペレーティング システムのメモリ不足実行に失敗します。 ベスト プラクティスを次に示します。

   * 起動メモリと最小限のメモリは、ディストリビューションのベンダーが推奨されているメモリ量以上にする必要があります。

   * システム全体の利用可能なメモリを消費する傾向があるアプリケーションは、使用可能なメモリの最大 80% を消費してに制限されます。

9. Windows Server 2019、Windows Server 2016、または Windows Server 2012/2012 R2 のいずれかのオペレーティングシステムで動的メモリを使用している場合は、**起動メモリ**、**最小メモリ**、および**最大メモリ**パラメーターを128メガバイト (mb) の倍数で指定します。 そのためにはエラーはエラーにつながるホット アドとゲスト オペレーティング システムに大きくなるメモリが表示されない場合があります。

10. Windows Server 2019、Windows Server 2016、または Windows Server 2012 R2 では、Linux ソフトウェア更新プログラムがないと、キー/値ペアのインフラストラクチャが正しく機能しない可能性があります。 この機能の問題が確認された場合に、ソフトウェア更新プログラムを取得するディストリビューションのベンダーに問い合わせてください。

11. Windows Server 2012 R2 では、[第 2 世代仮想マシンは、セキュア ブート オプションが無効にしない限り、仮想マシンは起動しません Linux 既定で有効になり、セキュア ブートがあります。 **Hyper-v マネージャー**で仮想マシンの設定の [**ファームウェア**] セクションでセキュアブートを無効にするか、Powershell を使用して無効にすることができます。

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

12. 新しい第 2 世代バーチャル マシンを作成するための既存の世代 2 の VHD の仮想マシンの VHD をコピーする前に、次の手順に従います。

    1. 既存の第 2 世代仮想マシンにログインします。

    2. ブート EFI ディレクトリにディレクトリを変更します。

       ```bash
       # cd /boot/efi/EFI
       ```

    3. Ubuntu ディレクトリを boot という名前の新しいディレクトリにコピーします。

       ```bash
       # sudo cp -r ubuntu/ boot
       ```

    4. 新しく作成したブート ディレクトリにディレクトリを変更します。

       ```bash
       # cd boot
       ```

    5. Shimx64.efi ファイルの名前を変更します。

       ```bash
       # sudo mv shimx64.efi bootx64.efi
       ```

## <a name="see-also"></a>参照

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Debian の仮想マシンを HYPER-V でサポートされています。](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Oracle Linux 仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Set-vmfirmware](/powershell/module/hyper-v/set-vmfirmware?view=win10-ps)

* [ジェネレーション 2 の Ubuntu 14.04 VM - Ben Armstrong の仮想化のブログ](/archive/blogs/virtual_pc_guy/ubuntu-14-04-in-a-generation-2-vm)