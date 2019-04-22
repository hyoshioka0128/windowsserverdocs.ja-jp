---
title: HYPER-V でサポートされている SUSE 仮想マシン
description: Linux integration services オブジェクトと各バージョンに含まれる機能を一覧表示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ec0e14c-4498-4bd9-8fe6-b94260198efc
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 3506c00651951aa2a62637cae6cc4989f9edf1fc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819003"
---
# <a name="supported-suse-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている SUSE 仮想マシン

>適用先:Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

各バージョンの機能を示す機能配布マップを次に示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

SUSE では、HYPER-V 用の組み込みの SUSE Linux Enterprise Service ドライバーが認定されています。 構成の例は、この情報に表示できます。[SUSE はい証明情報](https://www.suse.com/nbswebapp/yesBulletin.jsp?bulletinNumber=144176)します。

## <a name="table-legend"></a>表の凡例

* **組み込みの**-LIS がこの Linux ディストリビューションの一部として含まれています。Microsoft 提供の LIS のダウンロード パッケージは、インストールしないように、この配布は機能しません。組み込みの LIS のカーネル モジュールのバージョン番号 (に示す**lsmod**など)、Microsoft 提供の LIS のダウンロード パッケージにバージョン番号とは異なります。 組み込みの LIS の項目が古いことに不一致が示されません。

* & #10004 です。の機能使用

* (*空白*) の機能は使用できません

SLES12 + は 64 ビットのみです。

|**機能**|**Windows Server オペレーティング システムのバージョン**|**SLES 15**|**SLES 12 SP3 と SP4**|**SLES 12 SP2**|**SLES 12 SP1**|**SLES 11 SP4**|**SLES 11 SP3**|
|-|-|-|-|-|-|-|-|
|**可用性**||組み込み|組み込み|組み込み|組み込み|組み込み|組み込み|
|**[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 の正確な時刻|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[ネットワー キング](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**||||||||
|Jumbo Frame|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN タグ付け、トランキング|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2019、2016、2012 R2、2012|&#10004;注 1|&#10004;注 1|&#10004;注 1|&#10004;注 1|&#10004;注 1|&#10004;注 1|
|vRSS|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|TCP セグメント化およびチェックサム オフロード|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;|&#10004;||||
|**[ストレージ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**||||||||
|VHDX のサイズ変更|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|仮想ファイバー チャネル|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブの仮想マシンのバックアップ|2019、2016、2012 R2|& #10004 です。2、3、8 に注意してください。|& #10004 です。2、3、8 に注意してください。|& #10004 です。2、3、8 に注意してください。|& #10004 です。2、3、8 に注意してください。|& #10004 です。2、3、8 に注意してください。|& #10004 です。2、3、8 に注意してください。|
|TRIM のサポート|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SCSI WWN|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;||||
|**[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**||||||||
|PAE カーネル サポート|2019、2016、2012 R2、2012、2008 R2|なし|なし|なし|なし|&#10004;|&#10004;|
|MMIO の間隔の構成|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2019、2016、2012 R2、2012|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。4, 5, 6 に注意してください。|& #10004 です。4, 5, 6 に注意してください。|
|動的メモリ - バルーニング|2019、2016、2012 R2、2012|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。4, 5, 6 に注意してください。|& #10004 です。4, 5, 6 に注意してください。|
|ランタイムのメモリのサイズ変更|2019, 2016|& #10004 です。注 5、6|& #10004 です。注 5、6|& #10004 です。注 5、6||||
|**[ビデオ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**||||||||
|ハイパー V 固有ビデオ デバイス|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**||||||||
|キー/値ペア|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|& #10004 です。注 7|& #10004 です。注 7|
|マスク不可能割り込み|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ホスト ゲストからファイル コピー|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|lsvmbus コマンド|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;||||
|Hyper V ソケット|2019, 2016|&#10004;|&#10004;|||||
|PCI パススルー/DDA|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||
|**[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**||||||||
|UEFI を使用してブートします。|2019、2016、2012 R2|& #10004 です。注 9|& #10004 です。注 9|& #10004 です。注 9|& #10004 です。注 9|& #10004 です。注 9||
|セキュア ブート|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|||

## <a name="BKMK_notes"></a>ノート

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

9. Windows Server 2012 R2 では、セキュア ブート オプションが無効になっている場合を除き、第 2 世代仮想マシンがあるセキュア ブートが既定と世代 2 の Linux 仮想マシンで有効になっているは起動しません。 Hyper-V マネージャーの仮想マシンの設定の **[ファームウェア]** セクションで、または次の Powershell を使用して、セキュア ブートを無効にできます。

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

## <a name="see-also"></a>関連項目

* [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Debian の仮想マシン](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Oracle Linux 仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Ubuntu 仮想マシンの HYPER-V でサポートされています。](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v のサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux および FreeBSD の仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)
