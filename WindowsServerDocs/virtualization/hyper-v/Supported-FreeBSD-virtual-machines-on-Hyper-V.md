---
title: HYPER-V でサポートされている FreeBSD 仮想マシン
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 08/30/2017
ms.openlocfilehash: ea63a64ee0e1ce36ceb7783bbbc764c6ca5ca9d6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855955"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている FreeBSD 仮想マシン

>適用対象: Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows Server 2012、Hyper-v Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、windows 8、Windows 7.1、Windows 7。

次の機能の配布マップでは、各バージョンの機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

## <a name="table-legend"></a>表の凡例

* **組み込み**の BIS (Freebsd Integration Service) は、この freebsd リリースの一部として含まれています。

* & #10004 です。の機能使用

* (*空白*) の機能は使用できません

|**機能**|**Windows Server オペレーティングシステムのバージョン**|**11.1/11.2**|**11.0**|**10.3**|**10.2**|**10.0 ~ 10.1**|**9.1-9.3、8.4**|
|-|-|-|-|-|-|-|-|
|**可用性**||組み込まれています。|組み込まれています。|組み込まれています。|組み込まれています。|組み込まれています。|[Ports](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 の正確な時刻|2019、2016|&#10004;||||||
|**[機能](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo Frame|2019、2016、2012 R2、2012、2008 R2|& #10004 です。注 3|& #10004 です。注 3|& #10004 です。注 3|& #10004 です。注 3|& #10004 です。注 3|& #10004 です。注 3|
|VLAN のタグ付けとトランキング|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2019、2016、2012 R2、2012|& #10004 です。注 4|& #10004 です。注 4|& #10004 です。注 4|& #10004 です。注 4|& #10004 です。注 4|&#10004;|
|vRSS|2019、2016、2012 R2|&#10004;|&#10004;|||||
|TCP セグメント化とチェックサムのオフロード|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|大規模なオフロード (LRO) が表示されます。|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2019、2016|||||||
|**[・](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||メモ1|メモ1|メモ1|メモ1|メモ1、2|メモ1、2|
|VHDX のサイズ変更|2019、2016、2012 R2|& #10004 です。注 7|& #10004 です。注 7|||||
|仮想ファイバー チャネル|2019、2016、2012 R2|||||||
|仮想マシンのライブバックアップ|2019、2016、2012 R2|&#10004;||||||
|トリムのサポート|2019、2016、2012 R2|&#10004;||||||
|SCSI WWN|2019、2016、2012 R2|||||||
|**[量](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE カーネルサポート|2019、2016、2012 R2、2012、2008 R2|||||||
|MMIO ギャップの構成|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2019、2016、2012 R2、2012|||||||
|動的メモリ - バルーニング|2019、2016、2012 R2、2012|||||||
|ランタイムのメモリのサイズ変更|2019、2016|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|HYPER-V で特定のビデオ デバイス|2019、2016、2012 R2、2012、2008 R2|||||||
|**[な](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|キー/値ペア|2019、2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;注 6|& #10004 です。注 5、6|&#10004;注 6|
|マスクなしの割り込み|2019、2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ホストからゲストへのファイルのコピー|2019、2016、2012 R2|||||||
|lsvmbus コマンド|2019、2016、2012 R2、2012、2008 R2|||||||
|Hyper V ソケット|2019、2016|||||||
|PCI パススルー/DDA|2019、2016|&#10004;||||||
|**[第2世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI を使用したブート|2019、2016、2012 R2|&#10004;||||||
|セキュア ブート|2019、2016|||||||

## <a name="notes"></a><a name="BKMK_notes"></a>注記

1. 起動時にルートマウントエラーが発生しないように、[ディスクデバイスにラベルを付ける]( https://www.freebsd.org/doc/handbook/geom-glabel.html)ことをお勧めします。

2. 次のコマンドを使用してレガシ ATA ドライバーを有効にしない限り、BIS ドライバーが FreeBSD 2.x と1.x に読み込まれるときに、バーチャル DVD ドライブが認識されないことがあります。
    ```sh
    # echo ‘hw.ata.disk_enable=1' >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126は、サポートされている最大の MTU サイズです。

4. フェールオーバーのシナリオでは、レプリカ サーバーで静的な IPv6 アドレスを設定できません。 代わりに IPv4 アドレスを使用します。

5. KVP は、FreeBSD 10.0 のポートによって提供されます。 詳細については、FreeBSD.org の[FreeBSD 10.0 ポート](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/)を参照してください。

6. KVP は、Windows Server 2008 R2 で機能しない可能性があります。

7. VHDX のオンラインサイズ変更が FreeBSD 11.0 で適切に行われるようにするには、11.0 + で修正されたジオメトリバグを回避するための特別な手動手順が必要です。これは、ホストが VHDX ディスクのサイズを変更した後、書き込み用にディスクを開き、次のように "gpart 回復" を実行します。
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
   **追加の注意事項**:10 安定および11安定した機能マトリックスは、FreeBSD 11.1 リリースと同じです。 さらに、FreeBSD 10.2 とそれ以前のバージョン (10.1、10.0、1.x、2.x) は、有効期間が終了します。 サポートされているリリースと最新のセキュリティアドバイザリの最新の一覧については、[こちら](https://security.freebsd.org/)を参照してください。

**追加の注意事項**:10 安定および11安定した機能マトリックスは、FreeBSD 11.1 リリースと同じです。 さらに、FreeBSD 10.2 とそれ以前のバージョン (10.1、10.0、1.x、2.x) は、有効期間が終了します。 サポートされているリリースと最新のセキュリティアドバイザリの最新の一覧については、[こちら](https://security.freebsd.org/)を参照してください。

## <a name="see-also"></a>参照

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [Hyper-v で FreeBSD を実行するためのベストプラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
