---
title: HYPER-V でサポートされている FreeBSD 仮想マシン
description: Linux integration services オブジェクトと各バージョンに含まれる機能を一覧表示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 930e758f-bd50-46b4-a3a4-9857110f17b4
author: shirgall
ms.author: kathydav
ms.date: 08/30/2017
ms.openlocfilehash: a398334700f7c292732207919b73a33145a6aae9
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222693"
---
# <a name="supported-freebsd-virtual-machines-on-hyper-v"></a>HYPER-V でサポートされている FreeBSD 仮想マシン

>適用先:Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

次の機能の配布マップでは、各バージョンの機能を示します。 既知の問題と各配布の回避策は、表の下に一覧表示されます。

## <a name="table-legend"></a>表の凡例

* **組み込みの**-BIS (FreeBSD Integration Service) はこの FreeBSD リリースの一部として含まれています。

* &#10004 です。の機能使用

* (*空白*) の機能は使用できません

|**機能**|**Windows Server オペレーティング システムのバージョン**|**11.1/11.2**|**11.0**|**10.3**|**10.2**|**10.0 - 10.1**|**9.1 - 9.3, 8.4**|
|-|-|-|-|-|-|-|-|
|**可用性**||組み込まれています。|組み込まれています。|組み込まれています。|組み込まれています。|組み込まれています。|[ポート](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/) |
|**[コア](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#core)**|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004; |
|Windows Server 2016 の正確な時刻|2016|&#10004;||||||
|**[ネットワー キング](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#networking)**||||||||
|Jumbo Frame|2016、2012 R2、2012、2008 R2|&#10004 です。注 3|&#10004 です。注 3|&#10004 です。注 3|&#10004 です。注 3|&#10004 です。注 3|&#10004 です。注 3|
|VLAN タグ付け、トランキング|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ライブ マイグレーション|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|静的 IP インジェクション|2016、2012 R2、2012|&#10004 です。注 4|&#10004 です。注 4|&#10004 です。注 4|&#10004 です。注 4|&#10004 です。注 4|&#10004;|
|vRSS|2016、2012 R2|&#10004;|&#10004;|||||
|TCP セグメント化およびチェックサム オフロード|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|大規模なオフロード (LRO) が表示されます。|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;||||
|SR-IOV|2016|||||||
|**[ストレージ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#storage)**||注 1|注 1|注 1|注 1|注 1, 2|注 1, 2|
|VHDX のサイズ変更|2016、2012 R2|&#10004 です。注 7|&#10004 です。注 7|||||
|仮想ファイバー チャネル|2016、2012 R2|||||||
|ライブの仮想マシンのバックアップ|2016、2012 R2|&#10004;||||||
|TRIM のサポート|2016、2012 R2|&#10004;||||||
|SCSI WWN|2016、2012 R2|||||||
|**[メモリ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#memory)**||||||||
|PAE カーネル サポート|2016、2012 R2、2012、2008 R2|||||||
|MMIO の間隔の構成|2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|動的メモリでホット アド|2016、2012 R2、2012|||||||
|動的メモリ - バルーニング|2016、2012 R2、2012|||||||
|ランタイムのメモリのサイズ変更|2016|||||||
|**[ビデオ](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#video)**||||||||
|HYPER-V で特定のビデオ デバイス|2016、2012 R2、2012、2008 R2|||||||
|**[その他](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#miscellaneous)**||||||||
|キー/値ペア|2016、2012 R2、2012、2008 R2|&#10004;|&#10004;|&#10004;|&#10004;注 6|&#10004 です。注 5、6|&#10004;注 6|
|マスク不可能割り込み|2016、2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|ホスト ゲストからファイル コピー|2016、2012 R2|||||||
|lsvmbus コマンド|2016、2012 R2、2012、2008 R2|||||||
|Hyper V ソケット|2016|||||||
|PCI パススルー/DDA|2016|&#10004;||||||
|**[第 2 世代仮想マシン](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#generation-2-virtual-machines)**||||||||
|UEFI を使用してブートします。|2016、2012 R2|&#10004;||||||
|セキュア ブート|2016|||||||

## <a name="BKMK_notes"></a>ノート

1. ことを推奨[ラベル ディスク デバイス]( https://www.freebsd.org/doc/handbook/geom-glabel.html)スタートアップ中にルート マウント エラーを回避します。

2. FreeBSD に BIS ドライバーが読み込まれるときに、バーチャル DVD ドライブを認識されない 8.x および 9.x レガシ ATA ドライバーは、次のコマンドを有効にしない限りです。
    ```sh
    # echo ‘hw.ata.disk_enable=1’ >> /boot/loader.conf
    # shutdown -r now
    ```

3. 9126 は、サポートされる最大の MTU サイズです。

4. フェールオーバーのシナリオでは、レプリカ サーバーで静的な IPv6 アドレスを設定できません。 代わりに IPv4 アドレスを使用します。

5. KVP は FreeBSD 10.0 上のポートが提供されます。 参照してください、 [FreeBSD 10.0 ポート](https://svnweb.freebsd.org/ports/branches/2015Q1/emulators/hyperv-is/)詳細スロバキアにします。

6. KVP は、Windows Server 2008 R2 で機能しない可能性があります。

7. FreeBSD 11.0 で正しく VHDX のオンライン サイズ変更作業を行うには、特別な手動の手順がホスト VHDX ディスクのサイズを変更した後、11.0 以降で修正されてジオメトリのバグを回避する - ディスクの書き込みを開き、次のよう"gpart recover"を実行するために必要です。
    ```sh
    # dd if=/dev/da1 of=/dev/da1 count=0
    # gpart recover da1
    ```
**その他のメモ**:10 の安定性と安定版の 11 の機能の一覧は、FreeBSD 11.1 のリリースでは同じです。 加算、FreeBSD 10.2 および以前のバージョン (10.1、10.0、9.x、8.x) が終了します。 参照してください[ここ](https://security.freebsd.org/)のサポートされるリリースと最新のセキュリティ アドバイザリの最新の一覧。

**その他のメモ**:10 の安定性と安定版の 11 の機能の一覧は、FreeBSD 11.1 のリリースでは同じです。 加算、FreeBSD 10.2 および以前のバージョン (10.1、10.0、9.x、8.x) が終了します。 参照してください[ここ](https://security.freebsd.org/)のサポートされるリリースと最新のセキュリティ アドバイザリの最新の一覧。

## <a name="see-also"></a>関連項目

* [HYPER-V で Linux および FreeBSD の仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)
* [HYPER-V で FreeBSD を実行するためのベスト プラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
