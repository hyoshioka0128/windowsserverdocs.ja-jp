---
title: iSCSI ターゲット サーバーのスケーラビリティの制限
TOCTitle: iSCSI Target Server Scalability Limits
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 9514392da133911c900f68fc8f1be260b6c91138
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873033"
---
# <a name="iscsi-target-server-scalability-limits"></a>iSCSI ターゲット サーバーのスケーラビリティの制限

適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server でサポートされていると、テスト対象の Microsoft iSCSI ターゲット サーバーの制限を提供します。 次の表に、テスト対象のサポートの制限と、必要に応じて、制限が適用されるかどうか。

## <a name="general-limits"></a>一般的な制限事項

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>項目</p></th>
<th><p>サポートの制限</p></th>
<th><p>適用されますか。</p></th>
<th><p>Comment</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>iSCSI ターゲット サーバーごとに iSCSI ターゲット インスタンス</p></td>
<td><p>256</p></td>
<td><p>いいえ</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>iSCSI の論理ユニット (Lu) または iSCSI ターゲット サーバーごとの仮想ディスク</p></td>
<td><p>512</p></td>
<td><p>X</p></td>
<td><p>含まれる構成をテストするには。平均の 64 を超えるターゲットを持つターゲット インスタンスと 1 つのターゲットの 1 つの lu 256 のターゲット インスタンスあたり 8 Lu。</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI Lu または各 iSCSI 仮想ディスクのターゲット インスタンス</p></td>
<td><p>256 (Windows Server 2012 で 128)</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>ISCSI ターゲット インスタンスに同時に接続できるセッション</p></td>
<td><p>544 (Windows Server 2012 では 512)</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>LU ごとのスナップショット</p></td>
<td><p>512</p></td>
<td><p>〇</p></td>
<td><p>ISCSI の独立したアプリケーションのボリュームごとの 512 個のスナップショットの制限があります。</p></td>
</tr>
<tr class="even">
<td><p>ローカルにマウントされた仮想ディスクまたは記憶域アプライアンスごとのスナップショット</p></td>
<td><p>32</p></td>
<td><p>〇</p></td>
<td><p>ローカルにマウントされた仮想ディスクは提供していませんが、iSCSI 固有の機能、非推奨 - 詳細についてを参照してください<a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>します。</p></td>
</tr>
</tbody>
</table>

## <a name="fault-tolerance-limits"></a>フォールト トレランスを制限します。

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>項目</p></th>
<th><p>サポートの制限</p></th>
<th><p>適用されますか。</p></th>
<th><p>Comment</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>フェールオーバー クラスター ノード</p></td>
<td><p>8 (Windows Server 2012 では 5)</p></td>
<td><p>いいえ</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>複数のアクティブなクラスター ノード</p></td>
<td><p>サポートされている</p></td>
<td> 
<p>なし</p></td>
<td><p>フェールオーバー クラスター内のアクティブな各ノードでは、実行可能な所有者ノードとして機能する他のノードでさまざまな iSCSI ターゲット サーバーのクラスター化されたインスタンスを所有しています。</p></td>
</tr>
<tr class="odd">
<td><p>エラー回復レベル (ERL)</p></td>
<td><p>0</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>セッションごとの接続</p></td>
<td><p>1</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ISCSI ターゲット インスタンスに同時に接続できるセッション</p></td>
<td><p>544 (Windows Server 2012 では 512)</p></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>マルチパスの入力/出力 (MPIO)</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>MPIO パス</p></td>
<td><p>4</p></td>
<td><p>いいえ</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>スタンドアロンの iSCSI ターゲット サーバーをクラスター化された iSCSI ターゲット サーバーまたはその逆に変換します。</p></td>
<td><p>サポートされていません</p></td>
<td><p>X</p></td>
<td><p>ISCSI ターゲットのインスタンスと仮想ディスクの変換中に、スナップショットのメタデータを含む構成データは失われます。</p></td>
</tr>
</tbody>
</table>

## <a name="network-limits"></a>ネットワークの制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>項目</p></th>
<th><p>サポートの制限</p></th>
<th><p>適用されますか。</p></th>
<th><p>Comment</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>アクティブなネットワーク アダプターの最大数</p></td>
<td><p>8</p></td>
<td><p>X</p></td>
<td><p>アプライアンスでネットワーク アダプターの合計数ではなく、iSCSI トラフィックに専用のネットワーク アダプターに適用されます。</p></td>
</tr>
<tr class="even">
<td><p>サポートされているポータル (IP アドレス)</p></td>
<td><p>64</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ネットワークのポート速度</p></td>
<td><p>1 gbps、10 Gbps、40Gbps、56 Gbps (Windows Server 2012 R2 以降のみ)</p></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>IPv4</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPv6</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>TCP オフロード</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td><p>大量の送信 (セグメント化)、チェックサム、割り込み節度、および RSS のオフロードを利用します。</p></td>
</tr>
<tr class="odd">
<td><p>iSCSI オフロード</p></td>
<td><p>サポートされていません</p></td>
<td>              
<p>なし</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Jumbo Frame</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>IPSec</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CRC オフロード</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
</tbody>
</table>

## <a name="iscsi-virtual-disk-limits"></a>iSCSI 仮想ディスクの制限

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>項目</p></th>
<th><p>サポートの制限</p></th>
<th><p>適用されますか。</p></th>
<th><p>Comment</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>仮想ディスクをベーシック ディスクからダイナミック ディスクに変換する、iSCSI イニシエーターから </p></td>
<td><p>〇</p></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>仮想ハード ディスク フォーマット</p></td>
<td><p>.vhdx (Windows Server 2012 R2 以降のみ)</p>
<p>.vhd</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VHD 形式の最小サイズ</p></td>
<td><p>.vhdx:3 MB</p>
<p>.vhd:8 MB</p></td>
<td><p>〇</p></td>
<td><p>すべてのサポートされている VHD の種類に適用: 親、差分、および修正します。</p></td>
</tr>
<tr class="even">
<td><p>親 VHD の最大サイズ</p></td>
<td><p>.vhdx:64 TB です。</p>
<p>.vhd:2 TB</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>固定の VHD の最大サイズ</p></td>
<td><p>.vhdx:64 TB です。</p>
<p>.vhd:16 TB</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>差分 VHD の最大サイズ</p></td>
<td><p>.vhdx:64 TB です。</p>
<p>.vhd:2 TB</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>固定形式の VHD</p></td>
<td><p>サポートされている</p></td>
<td><p>X</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>差分の形式の VHD</p></td>
<td><p>サポートされている</p></td>
<td><p>X</p></td>
<td><p>差分 VHD ベースの iSCSI 仮想ディスクのスナップショットを作成することはできません。</p></td>
</tr>
<tr class="odd">
<td><p>差分 Vhd を親 VHD あたりの数</p></td>
<td><p>256</p></td>
<td><p>いいえ ([はい] に Windows Server 2012)</p></td>
<td><p>深度 (孫 .vhdx ファイル) 2 つのレベルは、.vhdx ファイルの最大値.vhd ファイルの最大の深さ (子の .vhd ファイル) の 1 つのレベルとなります。</p></td>
</tr>
<tr class="even">
<td><p>動的形式の VHD</p></td>
<td><p>.vhdx:〇</p>
<p>.vhd:はい (Windows Server 2012 ではいいえ)</p></td>
<td><p>〇</p></td>
<td><p>マップ解除はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td><p>exFAT/FAT32 または FAT (VHD のボリュームをホストしている)</p></td>
<td><p>サポートされていません</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>CSV v2</p></td>
<td><p>サポートされていません</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ReFS</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>NTFS</p></td>
<td><p>サポートされている</p></td>
<td><p>なし</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Microsoft 以外の CFS</p></td>
<td><p>サポートされていません</p></td>
<td><p>〇</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>仮想プロビジョニング</p></td>
<td><p>X</p></td>
<td><p>なし</p></td>
<td><p>動的 Vhd はサポートされますが、マッピング解除はサポートされていません。</p></td>
</tr>
<tr class="odd">
<td><p>論理ユニットの圧縮</p></td>
<td><p>[はい] (Windows Server 2012 R2 以降のみ)</p></td>
<td><p>なし</p></td>
<td><p>使用<a href="https://docs.microsoft.com/powershell/module/iscsitarget/resize-iscsivirtualdisk">サイズ変更 iSCSIVirtualDisk</a> LUN を縮小します。</p></td>
</tr>
<tr class="even">
<td><p>論理ユニットの複製</p></td>
<td><p>サポートされていません</p></td>
<td><p>なし</p></td>
<td><p>差分 Vhd を使用して、ディスク データを迅速に複製できます。</p></td>
</tr>
</tbody>
</table>

## <a name="snapshot-limits"></a>スナップショットの制限

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>項目</p></th>
<th><p>サポートの制限</p></th>
<th><p>Comment</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>スナップショットを作成します。</p></td>
<td><p>サポートされている</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>スナップショットの復元</p></td>
<td><p>サポートされている</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>書き込み可能なスナップショット</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>スナップショット – 完全に変換</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>スナップショット – オンラインのロールバック</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>– スナップショットを書き込み可能な変換します。</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>スナップショット - リダイレクト</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>スナップショットのピン留め</p></td>
<td><p>サポートされていません</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>ローカル マウント</p></td>
<td><p>サポートされている</p></td>
<td><p>ローカルにマウントされた iSCSI 仮想ディスクは非推奨の詳細については、「 <a href="https://technet.microsoft.com/library/dn303411.aspx">Features Removed or Deprecated in Windows Server 2012 R2</a>します。 ダイナミック ディスクのスナップショットは、ローカルにマウントすることはできません。</p></td>
</tr>
</tbody>
</table>

## <a name="iscsi-target-server-manageability-and-backup"></a>iSCSI ターゲット サーバーの管理性とバックアップ

アプリケーション サーバーから iSCSI 仮想ディスクにボリューム データのシャドウ コピー (VSS 開いているファイル スナップショット) を作成するか、仮想ディスク サービス (VDS) ハードウェアが必要ですが、古い (Diskraid コマンド) などで構成されたアプリの iSCSI 仮想ディスクを管理したい場合プロバイダーは、スナップショットを取得または、VDS 管理アプリを使用するサーバーに iSCSI ターゲット記憶域プロバイダーをインストールします。

ISCSI ターゲット記憶域プロバイダーは、Windows Server 2016、Windows Server 2012 R2、および Windows Server 2012; を使用して、役割サービスダウンロードしてインストールすることができますも[下位レベルのアプリケーション サーバーの iSCSI ターゲット記憶域プロバイダー (VDS/VSS)](http://www.microsoft.com/download/details.aspx?id=34759) iSCSI ターゲット サーバーが Windows Server 2012 で実行されている限り次のオペレーティング システムで。

  - Windows Storage Server 2008 R2

  - Windows Server 2008 R2

  - Windows HPC Server 2008 R2

  - Windows HPC Server 2008

ISCSI ターゲット サーバーは、Windows Server 2012 R2 を実行しているサーバーでホストされて以降、リモート サーバーから VDS、VSS、またはを使用する場合は、リモート サーバーにも同じバージョンの Windows Server を実行し、iSCSI ターゲット記憶域プロバイダーの役割がサービスに注意してください。e がインストールされています。 また、Windows のすべてのバージョンに iSCSI ターゲット記憶域プロバイダーの役割サービスの 1 つだけのバージョンをインストールする必要がありますに注意してください。

ISCSI ターゲット記憶域プロバイダーの詳細については、次を参照してください。 [iSCSI ターゲット記憶域 (VDS/VSS) プロバイダー](http://blogs.technet.com/b/filecab/archive/2012/10/08/iscsi-target-storage-vds-vss-provider.aspx)します。

## <a name="tested-compatibility-with-iscsi-initiators"></a>ISCSI イニシエーターとの互換性をテスト済み

ISCSI ターゲット サーバー ソフトウェアは、次の iSCSI イニシエーターをテストしました。

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>イニシエーター</p></td>
<td><p>Windows Server 2012 R2</p></td>
<td><p>Windows Server 2012</p></td>
<td><p>コメント</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 2012 R2</p></td>
<td><p>検証済み</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003</p></td>
<td><p>検証済み</p></td>
<td><p>検証済み</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare vSphere 5</p></td>
<td></td>
<td><p>検証済み</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>VMWare ESXi 5.0</p></td>
<td><p>検証済み</p></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>VMWare ESX 4.1</p></td>
<td><p>検証済み</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>CentOS 6.x</p></td>
<td><p>検証済み</p></td>
<td></td>
<td><p>セッションをログアウトし、サイズを変更した仮想ディスクの検出に戻ってログインする必要があります。</p></td>
</tr>
<tr class="even">
<td><p>Red Hat Enterprise Linux 6</p></td>
<td><p>検証済み</p></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>RedHat Enterprise Linux 5 and 5</p></td>
<td><p>検証済み</p></td>
<td><p>検証済み</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>SUSE Linux Enterprise Server 10</p></td>
<td></td>
<td><p>検証済み</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p>Oracle Solaris 11.x</p></td>
<td><p>検証済み</p></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

次の iSCSI イニシエーターが iSCSI ターゲット サーバーによってホストされている仮想ディスクからディスクなしのブートを実行するテストもしました。

  - Windows Server 2012 R2

  - Windows Server 2012

  - IPXE PCIe NIC

  - IPXE で CD または USB ディスク

## <a name="see-also"></a>関連項目

iSCSI ターゲット サーバーと関連テクノロジに関するその他のリソースを次に示します。

  - [iSCSI ターゲット ブロック記憶域の概要](iscsi-target-server.md)

  - [iSCSI Target ブートの概要](iscsi-boot-overview.md)

  - [Windows Server でのストレージ](..\storage.md)

