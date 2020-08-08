---
title: HYPER-V でサポートされている Oracle Linux 仮想マシン
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
manager: dongill
ms.topic: article
ms.assetid: c02fdb5b-62f3-43cb-a190-ab74b3ebcf77
author: shirgall
ms.author: kathydav
ms.date: 06/05/2020
ms.openlocfilehash: 0e9a11fbff5015037bffa1cad14e70d629fef94b
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989301"
---
# <a name="supported-oracle-linux-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている Oracle Linux 仮想マシン

>適用対象: Windows Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows 10、Windows 8.1

次の機能の配布マップでは、各バージョンに存在する機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

このセクションの内容は次のとおりです。

* [Oracle Linux 2.x シリーズ](#oracle-linux-8x-series)
* [Oracle Linux 2.x シリーズ](#oracle-linux-7x-series)
* [Oracle Linux 6.x シリーズ](#oracle-linux-6x-series)


## <a name="table-legend"></a>表の凡例

* **組み込まれている** に LIS がこの Linux ディストリビューションの一部として含まれています。 組み込みの LIS のカーネル モジュールのバージョン番号 (に示すように **lsmod**, 、たとえば) マイクロソフト提供の LIS のダウンロード パッケージにバージョン番号とは異なります。 組み込みの LIS の項目が古いことに不一致が示されません。

* & #10004 です。の機能使用
* (*空白*) の機能は使用できません
* **RHCK** -Red Hat 互換性カーネル
* **UEK** Enterprise KERNEL (UEK)
   * UEK4-アップストリームの Linux カーネルリリース4.1.12 に構築されています。
   * UEK5-アップストリームの Linux カーネルリリース4.14 で構築
   * UEK6-アップストリームの Linux カーネルリリース5.4 で構築

## <a name="oracle-linux-8x-series"></a>Oracle Linux 2.x シリーズ

|       **機能**     |       **Windows Server のバージョン**      |       **8.0-8.1 (RHCK)** |
|-----------------------|---------------------------------------|-------------------|
|       **可用性**        |   |
|       **[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019、2016、2012 R2 | &#10004; |
|       Windows Server 2016 の正確な時刻       | 2019、2016 | &#10004; |
|       **[ネットワーク](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |
|       Jumbo Frame        | 2019、2016、2012 R2 | &#10004; |
|       VLAN のタグ付けとトランキング       | 2019、2016、2012 R2 | &#10004;  |
|       ライブ マイグレーション      | 2019、2016、2012 R2 | &#10004; |
|       静的 IP インジェクション     |  2019、2016、2012 R2 | & #10004 です。注 2 |
|       vRSS     | 2019、2016、2012 R2 | &#10004; |
|       TCP セグメント化とチェックサムのオフロード | 2019、2016、2012 R2 | &#10004;|
|       SR-IOV  | 2019、2016 |  &#10004;   |
|       **[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |
|       VHDX のサイズ変更  | 2019、2016、2012 R2 | &#10004; |
|       仮想ファイバー チャネル | 2019、2016、2012 R2 | & #10004 です。注 3  |
|       仮想マシンのライブバックアップ  | 2019、2016、2012 R2 | & #10004 です。注 5 |
|       トリムのサポート | 2019、2016、2012 R2 | &#10004;  |
|       SCSI WWN | 2019、2016、2012 R2 | &#10004;  |
|       **[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |
|       PAE カーネルサポート  | 2019、2016、2012 R2 |  該当なし |
|       MMIO ギャップの構成  | 2019、2016、2012 R2 | &#10004; |
|       動的メモリでホット アド | 2019、2016、2012 R2  | & #10004 です。7, 8, 9 に注意してください。 |
|       動的メモリ - バルーニング | 2019、2016、2012 R2 | & #10004 です。7, 8, 9 に注意してください。 |
|       ランタイムのメモリのサイズ変更 | 2019、2016  | &#10004;  |
|       **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | |
|       Hyper-v 固有のビデオデバイス | 2019、2016、2012 R2 | &#10004;   |
|       **[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | |
|       キーと値のペア  | 2019、2016、2012 R2 | &#10004;   |
|       マスクなしの割り込み | 2019、2016、2012 R2 | &#10004;  |
|       ホストからゲストへのファイルのコピー | 2019、2016、2012 R2 | &#10004;  |
|       lsvmbus コマンド | 2019、2016、2012 R2 | &#10004;  |
|       Hyper V ソケット | 2019、2016 | &#10004;  |
|       PCI パススルー/DDA | 2019、2016 | &#10004; |
| **[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       UEFI を使用したブート | 2019、2016、2012 R2 |  & #10004 です。注 12  |
|       セキュア ブート | 2019、2016 |  &#10004; |

## <a name="oracle-linux-7x-series"></a>Oracle Linux 2.x シリーズ

このシリーズでは、64 ビットのカーネルのみができます。

<table width="100%">
<tr height="50px">
<td width="20%" rowspan="2">

機能
</td>
<td width="20%" rowspan="2">

Windows Server のバージョン
</td>
<td width="30%" colspan="3">

7.5-7.8
</td>
<td width="30%" colspan="3">

7.3-7.4
</td>
</tr>
<tr>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK5
</td>
<td width="20%" colspan="2">

RHCK
</td>
<td width="10%">

UEK4
</td>
</tr>
<tr>
<td width="20%">

可用性
</td>
<td width="20%">


</td>
<td width="10%">

LIS 4.3
</td>
<td width="10%">

組み込み
</td>
<td width="10%">

組み込み
</td>
<td width="10%">

LIS 4.3
</td>
<td width="10%">

組み込み
</td>
<td width="10%">

組み込み
</td>
</tr>
<tr height="50px">
<td width="20%">

**[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Windows Server 2016 の正確な時刻
</td>
<td width="20%">

2019、2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

 **[ネットワーク](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Jumbo Frame
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">
VLAN のタグ付けとトランキング
</td>
<td width="20%">
2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

ライブ マイグレーション
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

静的 IP インジェクション
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

& #10004 です。注 2
</td>
<td width="10%">

& #10004 です。注 2
</td>
<td width="10%">

& #10004 です。注 2
</td>
<td width="10%">

& #10004 です。注 2
</td>
<td width="10%">

& #10004 です。注 2
</td>
<td width="10%">

& #10004 です。注 2
</td>
</tr>
<tr height="50px">
<td width="20%">

vRSS
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

TCP セグメント化とチェックサムのオフロード
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SR-IOV
</td>
<td width="20%">

2019、2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

VHDX のサイズ変更
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

仮想ファイバー チャネル
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

& #10004 です。注 3
</td>
<td width="10%">

& #10004 です。注 3
</td>
<td width="10%">

& #10004 です。注 3
</td>
<td width="10%">

& #10004 です。注 3
</td>
<td width="10%">

& #10004 です。注 3
</td>
<td width="10%">

& #10004 です。注 3
</td>
</tr>
<tr height="50px">
<td width="20%">

仮想マシンのライブバックアップ
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

& #10004 です。注 5
</td>
<td width="10%">

& #10004 です。注 4、5
</td>
<td width="10%">

& #10004 です。注 5
</td>
<td width="10%">

& #10004 です。注 5
</td>
<td width="10%">

& #10004 です。注 4、5
</td>
<td width="10%">

& #10004 です。注 5
</td>
</tr>
<tr height="50px">
<td width="20%">

トリムのサポート
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

SCSI WWN
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**
</td>
<td width="20%">


</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

PAE カーネルサポート
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

該当なし
</td>
<td width="10%">

該当なし
</td>
<td width="10%">

該当なし
</td>
<td width="10%">

該当なし
</td>
<td width="10%">

該当なし
</td>
<td width="10%">

該当なし
</td>
</tr>
<tr height="50px">
<td width="20%">

MMIO ギャップの構成
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

ホットアド動的メモリ
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004; メモ7、8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
</tr>
<tr height="50px">
<td width="20%">

動的メモリバルーニング
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004; メモ7、8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
<td width="10%">

&#10004; ノート8、9
</td>
</tr>
<tr height="50px">
<td width="20%">

ランタイムのメモリのサイズ変更
</td>
<td width="20%">

2019、2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper-v 固有のビデオ
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

キーと値のペア
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

マスクなしの割り込み
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

ホストからゲストへのファイルのコピー
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

lsvmbus コマンド
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

Hyper V ソケット
</td>
<td width="20%">

2019、2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">


</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

PCI パススルー/DDA
</td>
<td width="20%">

2019、2016
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
<tr height="50px">
<td width="20%">

**[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**
</td>
<td width="20%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
<td width="10%">

</td>
</tr>
<tr height="50px">
<td width="20%">

UEFI を使用したブート
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

& #10004 です。注 12
</td>
<td width="10%">

& #10004 です。注 12
</td>
<td width="10%">

& #10004 です。注 12
</td>
<td width="10%">

& #10004 です。注 12
</td>
<td width="10%">

& #10004 です。注 12
</td>
<td width="10%">

& #10004 です。注 12
</td>
</tr>
<tr height="50px">
<td width="20%">

セキュア ブート
</td>
<td width="20%">

2019、2016、2012 R2
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
<td width="10%">

&#10004;
</td>
</tr>
</table>


## <a name="oracle-linux-6x-series"></a>Oracle Linux 6.x シリーズ

このシリーズでは、64 ビットのカーネルのみができます。

|       **機能**     |       **Windows Server のバージョン**      |       **6.8-6.10 (RHCK)** |       **6.8-6.10 (UEK4)**     |
|-----------------------|---------------------------------------|-------------------|-------------------|
|       **可用性**     |   | LIS 4.3  | 組み込み  |
|       **[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**      | 2019、2016、2012 R2 | &#10004; | &#10004;
|       Windows Server 2016 の正確な時刻       | 2019、2016 | |
|       **[ネットワーク](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**      |   |  |
|       Jumbo Frame        | 2019、2016、2012 R2 | &#10004; | &#10004;|
|       VLAN のタグ付けとトランキング       | 2019、2016、2012 R2 | & #10004 です。注 1 | & #10004 です。注 1 |
|       ライブ マイグレーション      | 2019、2016、2012 R2 | &#10004; | &#10004;|
|       静的 IP インジェクション     |  2019、2016、2012 R2 | & #10004 です。注 2 | &#10004;|
|       vRSS     | 2019、2016、2012 R2 | &#10004; | &#10004;|
|       TCP セグメント化とチェックサムのオフロード | 2019、2016、2012 R2 | &#10004;|  &#10004; |
|       SR-IOV  | 2019、2016 |    |  |
|       **[Storage](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)** |  |  |
|       VHDX のサイズ変更  | 2019、2016、2012 R2 | &#10004; | &#10004; |
|       仮想ファイバー チャネル | 2019、2016、2012 R2 | & #10004 です。注 3  | & #10004 です。注 3 |
|       仮想マシンのライブバックアップ  | 2019、2016、2012 R2 | & #10004 です。注 5 | & #10004 です。注 5|
|       トリムのサポート | 2019、2016、2012 R2 | &#10004;  | &#10004; |
|       SCSI WWN | 2019、2016、2012 R2 | &#10004;  | &#10004; |
|       **[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)** | |  |
|       PAE カーネルサポート  | 2019、2016、2012 R2 |  該当なし | 該当なし
|       MMIO ギャップの構成  | 2019、2016、2012 R2 | &#10004; | &#10004;  |
|       動的メモリでホット アド | 2019、2016、2012 R2  | & #10004 です。6、8、9 に注意してください。 | & #10004 です。6、8、9 に注意してください。 |
|       動的メモリ - バルーニング | 2019、2016、2012 R2 | & #10004 です。6、8、9 に注意してください。 | & #10004 です。6、8、9 に注意してください。 |
|       ランタイムのメモリのサイズ変更 | 2019、2016  |  | |
|       **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)** | | |
|       Hyper-v 固有のビデオデバイス | 2019、2016、2012 R2 | &#10004;   | &#10004; |
|       **[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)** | | |
|       キーと値のペア  | 2019、2016、2012 R2 | &#10004; メモ10、11   | &#10004; メモ10、11  |
|       マスクなしの割り込み | 2019、2016、2012 R2 | &#10004;  | &#10004; |
|       ホストからゲストへのファイルのコピー | 2019、2016、2012 R2 | &#10004;  | &#10004; |
|       lsvmbus コマンド | 2019、2016、2012 R2 | &#10004;  | &#10004; |
|       Hyper V ソケット | 2019、2016 | &#10004;  | &#10004; |
|       PCI パススルー/DDA | 2019、2016 | &#10004; | &#10004; |
| **[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** | |  |
|       UEFI を使用したブート | 2019、2016、2012 R2 |  & #10004 です。注 12  | & #10004 です。注 12
|       セキュア ブート | 2019、2016 |  |  |



## <a name="notes"></a><a name="BKMK_notes"></a>注

1. この Oracle Linux のリリースでは、VLAN が、動作、VLAN トランクをタグ付けされていません。

2. ネットワーク マネージャーは、仮想マシン上の特定の統合ネットワーク アダプターに対して構成されている場合、静的 IP インジェクションは機能しません。 静的 IP インジェクションの円滑に機能のことを確認して、ネットワーク マネージャーが入っていないか、完全にオフになっている特定のネットワーク アダプターの ifcfg ethX ファイルを使用してください。

3.  Windows Server 2012 R2 で仮想ファイバーチャネルデバイスを使用している場合は、論理ユニット番号 0 (LUN 0) が設定されていることを確認してください。 LUN 0 が設定されていません Linux 仮想マシンは、ファイバー チャネル デバイスをネイティブにマウントすることができません。

4. ビルトイン LIS の場合、この機能のために "hyperv デーモン" パッケージをインストールする必要があります。

5.  仮想マシンのバックアップ操作中に、いくつかのコーナー ケースで開いているファイル ハンドルがある場合、バックアップされる Vhd は、ファイル システムの整合性チェック (fsck) を復元する必要があります。 ライブ バックアップ操作がエラーに何も行わずに、仮想マシンに接続された iSCSI デバイスまたは直接接続ストレージ (パススルー ディスクとも呼ばれます) がある場合。

6. 動的メモリのサポートは、64 ビット仮想マシンで使用できるのみです。

7. ホット アド サポートは、この配布に既定では無効です。 ホット アド サポートを有効にするには、/etc/udev/rules.d/ 下にある udev ルールを次のように追加する必要があります。

   1. ファイルを作成する **/etc/udev/rules.d/100-balloon.rules**します。 ファイルの他の目的の名前を使用することがあります。

   2. 次の内容をファイルに追加します。`SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. ホット アド サポートを有効にするシステムを再起動します。

   Linux Integration Services ダウンロードは、インストールでこのルールを作成するときに、ルールが削除されます LIS がアンインストールされると、ため、アンインストールの後に動的メモリが必要な場合は、ルールを再作成される必要があります。

8. 動的メモリの操作は、ゲスト オペレーティング システムが不足している場合もメモリに失敗することができます。 ベスト プラクティスを次に示します。

   * 起動メモリと最小限のメモリは、ディストリビューションのベンダーが推奨されているメモリ量以上にする必要があります。

   * システム全体の利用可能なメモリを消費する傾向があるアプリケーションは、使用可能なメモリの最大 80% を消費してに制限されます。

9. Windows Server 2016 または Windows Server 2012 R2 オペレーティングシステムで動的メモリを使用している場合は、[**起動メモリ**]、[**最小メモリ**]、[**最大メモリ**] パラメーターを128メガバイト (mb) の倍数で指定します。 そのためにはエラーがホット アドの障害につながるし、ゲスト オペレーティング システムのメモリが表示されない場合があります。

10. キー/値ペア (KVP) インフラストラクチャを有効にするには、Oracle Linux ISO から hypervkvpd または hyperv デーモン rpm パッケージをインストールします。 または、パッケージを Oracle Linux Yum リポジトリから直接インストールすることもできます。

11. Linux ソフトウェア更新プログラムがないは、キー/値ペア (KVP) インフラストラクチャが正しく機能しない可能性があります。 この機能の問題が確認された場合に、ソフトウェア更新プログラムを取得するディストリビューションのベンダーに問い合わせてください。

12. Windows Server 2012 R2 第2世代仮想マシンでは、セキュアブートオプションが無効になっていない限り、既定でセキュアブートが有効になっており、一部の Linux 仮想マシンは起動しません。 **Hyper-v マネージャー**で仮想マシンの設定の [**ファームウェア**] セクションでセキュアブートを無効にするか、Powershell を使用して無効にすることができます。

    ```Powershell
    Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
    ```

    Linux Integration Services ダウンロードは、世代 2 の既存の Vm に適用することができますが、第 2 世代の機能には影響しません。


参照

* [Set-vmfirmware](/powershell/module/hyper-v/set-vmfirmware?view=win10-ps)

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Debian の仮想マシンを HYPER-V でサポートされています。](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Ubuntu 仮想マシン](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)