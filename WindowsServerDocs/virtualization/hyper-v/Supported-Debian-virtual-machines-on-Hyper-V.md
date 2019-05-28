---
title: Debian の仮想マシンを HYPER-V でサポートされています。
description: Linux integration services オブジェクトと各バージョンに含まれる機能を一覧表示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cc62c10-02a3-4633-960c-23bf91a45bd5
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 129783dc980be6e471ecadb2cdbffee900e3396e
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222835"
---
# <a name="supported-debian-virtual-machines-on-hyper-v"></a>Debian の仮想マシンを HYPER-V でサポートされています。

>適用先:Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

次の機能の配布マップでは、各バージョンに存在する機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

## <a name="table-legend"></a>表の凡例

* **組み込まれている** に LIS がこの Linux ディストリビューションの一部として含まれています。 インストールしないように、この配布では、Microsoft 提供の LIS のダウンロード パッケージは機能しません。 組み込みの LIS のカーネル モジュールのバージョン番号 (に示すように **lsmod**, 、たとえば) マイクロソフト提供の LIS のダウンロード パッケージにバージョン番号とは異なります。 不一致では、組み込みの LIS の項目が古いことは示されません。

* &#10004 です。の機能使用

* (*空白*) の機能は使用できません

|**機能**|**Windows Server オペレーティング システムのバージョン**|**9.0 9.6 (ストレッチ)**|**8.0 8.11 (jessie)**|**7.0 7.11 (wheezy)**|
|-|-|-|-|-|
|**可用性**||組み込まれています。|組み込まれています。|(メモ 6) に組み込まれています。|
|**[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 の正確な時刻|2019, 2016|&#10004;8 に注意してください。||
|**[ネットワー キング](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**|
|Jumbo Frame|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|
|VLAN タグ付け、トランキング|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2019、2016、2012 R2、2012|||
|vRSS|2019、2016、2012 R2|&#10004;8 に注意してください。|||
|TCP セグメント化およびチェックサム オフロード|2019、2016、2012 R2、2012、2008 R2|&#10004;8 に注意してください。|||
|SR-IOV|2019, 2016|&#10004;8 に注意してください。||
|**[ストレージ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**|
|VHDX のサイズ変更|2019、2016、2012 R2|&#10004 です。注 1|&#10004 です。注 1|&#10004 です。注 1|
|仮想ファイバー チャネル|2019、2016、2012 R2|||
|ライブの仮想マシンのバックアップ|2019、2016、2012 R2|&#10004 です。注 4、5|&#10004 です。注 4、5|&#10004 です。注 4|
|TRIM のサポート|2019、2016、2012 R2|&#10004;8 に注意してください。|||
|SCSI WWN|2019、2016、2012 R2|&#10004;8 に注意してください。||
|**[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**|
|PAE カーネル サポート|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|
|MMIO の間隔の構成|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2019、2016、2012 R2、2012|&#10004;8 に注意してください。|||
|動的メモリ - バルーニング|2019、2016、2012 R2、2012|&#10004;8 に注意してください。|||
|ランタイムのメモリのサイズ変更|2019, 2016|&#10004;8 に注意してください。|||
|**[ビデオ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**|
|ハイパー V 固有ビデオ デバイス|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;||
|**[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**|
|キーと値のペア|2019、2016、2012 R2、2012、2008 R2|&#10004 です。注 4|&#10004 です。注 4||
|マスク不可能割り込み|2019、2016、2012 R2|&#10004;|&#10004;|
|ホスト ゲストからファイル コピー|2019、2016、2012 R2|&#10004 です。注 4|&#10004 です。注 4||
|lsvmbus コマンド|2019、2016、2012 R2、2012、2008 R2|||
|Hyper V ソケット|2019, 2016|&#10004;8 に注意してください。|||
|PCI パススルー/DDA|2019, 2016|&#10004;8 に注意してください。|||
|**[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**|
|UEFI を使用してブートします。|2019、2016、2012 R2|&#10004 です。注 7|&#10004 です。注 7||
|セキュア ブート|2019, 2016|||

## <a name="BKMK_notes"></a>ノート

1. Vhd 上のファイル システムを作成する 2 TB を超えることはできません。

2. Windows Server 2008 R2 の SCSI ディスク エントリを 8 つに作成/デベロッパー/sd * します。

3. Windows Server 2012 R2 と 8 コア以上の VM には、1 つの vCPU にルーティングされるすべての割り込みがあります。

4. デーモンを開始する Debian 8.3 では、Debian パッケージを手動でインストールされた"hyperv-"、キーと値のペア、fcopy、および VSS デーモンが含まれています。 取得する必要 hyperv デーモン パッケージ Debian 7.x および 8.0 8.2 [Debian backports](https://wiki.debian.org/Backports)します。

5. ライブの仮想マシンのバックアップは、ext2 ファイル システムでは動作しません。 Debian インストーラーによって作成される既定のレイアウトに ext2 ファイルシステムが含まれています、このファイル システムの種類を作成しないレイアウトをカスタマイズする必要があります。

6. カーネルに含まれる Debian 7.x は、サポート対象外には、古いカーネルを使用して、 [Debian backports](https://wiki.debian.org/Backports) Debian 7.x が HYPER-V の機能を向上させるためです。

7. Windows Server 2012 R2 世代 2 の仮想マシンがセキュア ブートが既定で有効になっているにあり、セキュア ブート オプションが無効にしない限り、一部の Linux 仮想マシンは起動しません。 セキュア ブートを無効にすることができます、 **ファームウェア** でバーチャル マシンの設定のセクション **HYPER-V マネージャーで** または Powershell を使用して無効にすることができます。

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```
8. アップ ストリームのカーネルの最新の機能は、含まれるカーネルを使用してのみ利用可能な[Debian backports](https://wiki.debian.org/Backports)します。

関連項目

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Oracle Linux 仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v のサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Ubuntu 仮想マシンの HYPER-V でサポートされています。](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v のサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux および FreeBSD の仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)
