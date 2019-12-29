---
title: HYPER-V でサポートされている SUSE 仮想マシン
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 45517c1d381ba55c819b09b53ae563092e161b1e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366727"
---
# <a name="supported-suse-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている SUSE 仮想マシン

>適用先:Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows Server 2012、Hyper-v Server の2012、Windows Server 2008 R2、Windows 10、Windows 8.1、windows 8、Windows 7.1、Windows 7

各バージョンの機能を示す機能配布マップを次に示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

SUSE では、HYPER-V 用の組み込みの SUSE Linux Enterprise Service ドライバーが認定されています。 この情報は、構成例を次のように表示できます。[SUSE YES 認定資格情報](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176)。

## <a name="table-legend"></a>表の凡例

* **組み込み**の LIS は、この Linux ディストリビューションの一部として含まれています。Microsoft 提供の LIS ダウンロードパッケージは、この配布では機能しないため、インストールしないでください。組み込み LIS のカーネルモジュールのバージョン番号 (たとえば、 **lsmod**によって示されている) は、Microsoft 提供の lis ダウンロードパッケージのバージョン番号とは異なります。 組み込みの LIS の項目が古いことに不一致が示されません。

* &#10004; です。の機能使用

* (*空白*) の機能は使用できません

SLES12 + は64ビットのみです。

|**機能**|**Windows Server オペレーティングシステムのバージョン**|**SLES 15**|**SLES 12 SP3/SP4**|**SLES 12 SP2**|**SLES 12 SP1**|**SLES 11 SP4**|**SLES 11 SP3**|
|-|-|-|-|-|-|-|-|
|**可用性**||組み込み|組み込み|組み込み|組み込み|組み込み|組み込み|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 の正確な時刻|2019、2016|&#10004;|&#10004;|&#10004;||||
|**[機能](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo Frame|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN のタグ付けとトランキング|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2019、2016、2012 R2、2012|&#10004;メモ1|&#10004;メモ1|&#10004;メモ1|&#10004;メモ1|&#10004;メモ1|&#10004;メモ1|
|vRSS|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|TCP セグメント化とチェックサムのオフロード|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019、2016|&#10004;|&#10004;|&#10004;||||
|**[・](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||||||||
|VHDX のサイズ変更|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|仮想ファイバー チャネル|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|仮想マシンのライブバックアップ|2019、2016、2012 R2|&#10004;です。2、3、8 に注意してください。|&#10004;です。2、3、8 に注意してください。|&#10004;です。2、3、8 に注意してください。|&#10004;です。2、3、8 に注意してください。|&#10004;です。2、3、8 に注意してください。|&#10004;です。2、3、8 に注意してください。|
|トリムのサポート|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SCSI WWN|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;||||
|**[量](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE カーネルサポート|2019、2016、2012 R2、2012、2008 R2|なし|なし|なし|なし|&#10004;|&#10004;|
|MMIO ギャップの構成|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2019、2016、2012 R2、2012|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。4, 5, 6 に注意してください。|&#10004; です。4, 5, 6 に注意してください。|
|動的メモリ - バルーニング|2019、2016、2012 R2、2012|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。4, 5, 6 に注意してください。|&#10004; です。4, 5, 6 に注意してください。|
|ランタイムのメモリのサイズ変更|2019、2016|&#10004; です。注 5、6|&#10004; です。注 5、6|&#10004; です。注 5、6||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|Hyper-v 固有のビデオデバイス|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[な](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|キー/値ペア|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; です。注 7|&#10004; です。注 7|
|マスクなしの割り込み|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ホストからゲストへのファイルのコピー|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|lsvmbus コマンド|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;||||
|Hyper V ソケット|2019、2016|&#10004;|&#10004;|||||
|PCI パススルー/DDA|2019、2016|&#10004;|&#10004;|&#10004;|&#10004;|||
|**[第2世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI を使用したブート|2019、2016、2012 R2|&#10004;です。注 9|&#10004;です。注 9|&#10004;です。注 9|&#10004;です。注 9|&#10004;です。注 9||
|セキュアブート|2019、2016|&#10004;|&#10004;|&#10004;|&#10004;|||

## <a name="BKMK_notes"></a>注記

1. 静的 IP インジェクションが機能しなくなる **ネットワーク マネージャー** が仮想マシン上の指定したハイパー V 固有ネットワーク アダプターに対して構成されています。 静的 IP の円滑に機能することを確認するインジェクションを確認してくださいネットワーク マネージャーが完全にオフや、オフになっているを使って特定のネットワーク アダプターにその **ifcfg ethX** ファイルです。

2. バーチャル マシンのバックアップ操作中に、いくつかのコーナー ケースで開いているファイル ハンドルがある場合、バックアップされる Vhd は、ファイル システムの整合性チェック (fsck) を復元する必要があります。

3. ライブ バックアップ操作がエラーに何も行わずに、仮想マシンに接続された iSCSI デバイスまたは直接接続ストレージ (パススルー ディスクとも呼ばれます) がある場合。

4. 動的メモリの操作は、ゲスト オペレーティング システムが不足している場合もメモリに失敗することができます。 ベスト プラクティスを次に示します。

   * 起動メモリと最小限のメモリは、ディストリビューションのベンダーが推奨されているメモリ量以上にする必要があります。

   * システム全体の利用可能なメモリを消費する傾向があるアプリケーションは、使用可能なメモリの最大 80% を消費してに制限されます。

5. 動的メモリのサポートは、64 ビット仮想マシンで使用できるのみです。

6. Windows Server 2016 または Windows Server 2012 オペレーティング システムを動的メモリを使用している場合は、指定 **起動メモリ**, 、**最小メモリ**, 、および **最大メモリ** 128 mb の倍数でのパラメーターです。 そのためにはエラーはエラーにつながるホット アドとゲスト オペレーティング システムのメモリが表示されない場合があります。

7. Windows Server 2016 または Windows Server 2012 R2 では、キー/値ペアのインフラストラクチャが正しく機能しない Linux ソフトウェア更新プログラムがないです。 この機能の問題が確認された場合に、ソフトウェア更新プログラムを取得するディストリビューションのベンダーに問い合わせてください。

8. 1 つのパーティションで複数回がマウントされている場合、VSS バックアップは失敗します。

9. Windows Server 2012 R2 では、第2世代仮想マシンでセキュアブートオプションが無効になっていない限り、セキュアブートが既定で有効になり、第2世代の Linux 仮想マシンは起動しません。 Hyper-V マネージャーの仮想マシンの設定の **[ファームウェア]** セクションで、または次の Powershell を使用して、セキュア ブートを無効にできます。

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

## <a name="see-also"></a>関連項目

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [サポートされている CentOS と Hyper-v 上の仮想マシンの Red Hat Enterprise Linux](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-V でサポートされている Debian 仮想マシン](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている Oracle Linux の仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている Ubuntu 仮想マシン](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v で Linux を実行するためのベストプラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)
