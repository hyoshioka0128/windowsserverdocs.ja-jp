---
title: Debian の仮想マシンを HYPER-V でサポートされています。
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 04/07/2020
ms.openlocfilehash: e5483b9547e67414bd66b3daad1a4b07c3cb7cfc
ms.sourcegitcommit: 7b1ebc4934998af2472962ca8cce1c872f39946f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/09/2020
ms.locfileid: "80994512"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Debian の仮想マシンを HYPER-V でサポートされています。

>適用対象: Windows Server 2019、Hyper-v Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows 10、および Windows 8.1

次の機能の配布マップでは、各バージョンに存在する機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

## <a name="table-legend"></a>表の凡例

* **組み込まれている** に LIS がこの Linux ディストリビューションの一部として含まれています。 インストールしないように、この配布では、Microsoft 提供の LIS のダウンロード パッケージは機能しません。 組み込みの LIS のカーネル モジュールのバージョン番号 (に示すように **lsmod**, 、たとえば) マイクロソフト提供の LIS のダウンロード パッケージにバージョン番号とは異なります。 不一致では、組み込みの LIS の項目が古いことは示されません。

* & #10004 です。の機能使用

* (*空白*) の機能は使用できません

| **機能**                                                                                                                                  | **Windows Server オペレーティングシステムのバージョン** | **10.0-10.3 (buster)** | **9.0-9.12 (ストレッチ)** | **8.0-8.11 (jessie)** | **7.0-7.11 (wheezy)** |
|----------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------|-----------------------|-----------------------|-----------------------|-----------------------|
| **可用性**                                                                                                                             |                                             | 組み込まれています。              | 組み込まれています。              | 組み込まれています。              | 組み込み (メモ 5)     |
| **[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**                                                   | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| Windows Server 2016 の正確な時刻                                                                                                            | 2019、2016                                  | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| **[機能](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**                                       |                                             |                       |                       |                       |                       |
| Jumbo Frame                                                                                                                                 | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| VLAN のタグ付けとトランキング                                                                                                                    | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| ライブ マイグレーション                                                                                                                               | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| 静的 IP インジェクション                                                                                                                          | 2019、2016、2012 R2                   |                       |                       |                       |                       |
| vRSS                                                                                                                                         | 2019、2016、2012 R2                         | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| TCP セグメント化とチェックサムのオフロード                                                                                                       | 2019、2016、2012 R2          | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| SR-IOV                                                                                                                                       | 2019、2016                                  | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| **[・](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**                                             |                                             |                       |                       |                       |                       |
| VHDX のサイズ変更                                                                                                                                  | 2019、2016、2012 R2                         | & #10004 です。注 1       | & #10004 です。注 1       | & #10004 です。注 1       | & #10004 です。注 1       |
| 仮想ファイバー チャネル                                                                                                                        | 2019、2016、2012 R2                         |                       |                       |                       |                       |
| 仮想マシンのライブバックアップ                                                                                                                  | 2019、2016、2012 R2                         | &#10004;Note2 以降 | &#10004;Note2 以降 | &#10004;Note2 以降 | &#10004;Note2 以降 |
| トリムのサポート                                                                                                                                 | 2019、2016、2012 R2                         | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| SCSI WWN                                                                                                                                     | 2019、2016、2012 R2                         | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| **[量](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**                                               |                                             |                       |                       |                       |                       |
| PAE カーネルサポート                                                                                                                           | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| MMIO ギャップの構成                                                                                                                    | 2019、2016、2012 R2                         | &#10004;              | &#10004;              | &#10004;              | &#10004;              |
| 動的メモリでホット アド                                                                                                                     | 2019、2016、2012 R2                   | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| 動的メモリ - バルーニング                                                                                                                  | 2019、2016、2012 R2                   | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| ランタイムのメモリのサイズ変更                                                                                                                        | 2019、2016                                  | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| **[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**                                                 |                                             |                       |                       |                       |                       |
| Hyper-v 固有のビデオデバイス                                                                                                                | 2019、2016、2012 R2          | &#10004;              | &#10004;              | &#10004;              |                       |
| **[な](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**                                 |                                             |                       |                       |                       |                       |
| キーと値のペア                                                                                                                               | 2019、2016、2012 R2          | & #10004 です。注 2       | & #10004 です。注 2       | & #10004 です。注 2       |                       |
| マスクなしの割り込み                                                                                                                       | 2019、2016、2012 R2                         | &#10004;              | &#10004;              | &#10004;              |                       |
| ホストからゲストへのファイルのコピー                                                                                                                 | 2019、2016、2012 R2                         | & #10004 です。注 2       | & #10004 です。注 2       | & #10004 です。注 2       |                       |
| lsvmbus コマンド                                                                                                                              | 2019、2016、2012 R2          |                       |                       |                       |                       |
| Hyper V ソケット                                                                                                                              | 2019、2016                                  | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| PCI パススルー/DDA                                                                                                                          | 2019、2016                                  | & #10004 です。注 4       | & #10004 です。注 4       |                       |                       |
| **[第2世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)** |                                             |                       |                       |                       |                       |
| UEFI を使用したブート                                                                                                                              | 2019、2016、2012 R2                         | & #10004 です。注 3       | & #10004 です。注 3       | & #10004 です。注 3       |                       |
| セキュア ブート                                                                                                                                  | 2019、2016                                  | &#10004;              |                       |                       |                       |


## <a name="notes"></a>説明

1. Vhd 上のファイル システムを作成する 2 TB を超えることはできません。

2. デーモンを開始する Debian 8.3 では、Debian パッケージを手動でインストールされた"hyperv-"、キーと値のペア、fcopy、および VSS デーモンが含まれています。 取得する必要 hyperv デーモン パッケージ Debian 7.x および 8.0 8.2 [Debian backports](https://wiki.debian.org/Backports)します。

3. Windows Server 2012 R2 第2世代仮想マシンでは、セキュアブートオプションが無効になっていない限り、既定でセキュアブートが有効になっており、一部の Linux 仮想マシンは起動しません。 **Hyper-V マネージャー**で仮想マシンの設定の **[ファームウェア]** セクションか PowerShell を使用してセキュア ブートを無効にすることができます。

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off
   ```
4. 最新のアップストリームカーネル機能は、カーネルに含まれる[Debian バックポート](https://wiki.debian.org/Backports)を使用した場合にのみ使用できます。

5. Debian 6.x はサポート対象外であり、古いカーネルを使用していますが、debian 2.x の Debian backports に含まれるカーネルは、Hyper-v の機能を強化しています。

参照

* [サポートされている CentOS と Hyper-v 上の仮想マシンの Red Hat Enterprise Linux](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている Oracle Linux の仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている Ubuntu 仮想マシン](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v でサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v で Linux を実行するためのベストプラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)
