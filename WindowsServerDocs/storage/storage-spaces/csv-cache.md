---
title: 記憶域スペース ダイレクトのメモリ内読み取りキャッシュ
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122055"
---
# 読み取りキャッシュを CSV のメモリ内での記憶域スペース ダイレクトの使用
> 適用対象: Windows Server 2016、Windows Server 2019

このトピックでは、システム メモリを使用して[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)のパフォーマンスを向上させる方法について説明します。

記憶域スペース ダイレクトは、クラスター共有ボリューム (CSV) メモリ内読み取りキャッシュとの互換性です。 読み取りをキャッシュするシステム メモリを使用すると、HYPER-V は、VHD または VHDX ファイルにアクセスするバッファーの I/O を使用するなどのアプリケーションのパフォーマンスを向上させることができます。 (IOs のバッファーは、Windows キャッシュ マネージャーではキャッシュされずする操作です)。

メモリー内キャッシュは、ローカル サーバーであるため、ハイパーコンバージド記憶域スペース ダイレクト展開ではデータのローカル性が向上: 最近の読み取りはキャッシュでは、仮想マシンが実行されている同じホスト上のメモリ、どのくらいの頻度を減らすこと読み取り経由ネットワーク。 これは、結果より短い待機時間と記憶域のパフォーマンスが向上します。

## 計画に関する考慮事項

メモリ内読み取りキャッシュが仮想デスクトップ インフラストラクチャ (VDI) など、読み取り、負荷の高いワークロード最も効果的です。 逆に、ワークロードが非常に書き込みを多用する場合は、キャッシュ値以上のオーバーヘッドが生じる可能性があります、無効にする必要があります。

CSV のメモリ内読み取りキャッシュの合計の物理メモリの最大 80% を使用できます。

  > [!TIP]
  > ハイパーコンバージド展開では、位置を計算し、記憶域を同じサーバー上で実行する仮想マシンのメモリ不足のためのままにするように注意してください。 コンバージド スケール アウト ファイル サーバー (SoFS) 展開では、メモリの少ない競合これは該当しません。

  > [!NOTE]
  > DISKSPD と[VM 航空機の中](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet)結果が生じるさらに、CSV のメモリ内のような特定 microbenchmarking ツールは読み取りキャッシュをよりもなしで有効にします。 既定では、VM 航空機の中は、1 つの 10 GiB 仮想マシン – 約 1 TiB あたり VHDX ~ 100 の Vm の合計*均一にランダムな*読み取りを実行し、それらに書き込みを作成します。 実際のワークロードとは異なり、読み取りしないフォローしている、予測可能なまたは繰り返しパターンのためメモリー内キャッシュが有効でないし、同様のオーバーヘッドが発生します。

## 構成、メモリ内読み取りキャッシュ

CSV メモリ内読み取りキャッシュは同じ機能を持つ Windows Server 2016 および Windows Server 2019 の両方で利用できます。 Windows Server 2016 ではそれは既定でオフです。 Windows Server 2019 では、それは既定でオン割り当てられている 1 gb します。

| OS バージョン          | 既定の CSV キャッシュ サイズ |
|---------------------|------------------------|
| Windows Server 2016 | 0 (無効)           |
| Windows Server 2019 | 1 giB                   |

PowerShell を使用して、メモリの量が割り当てられたについては、次のコマンドを実行します。

```PowerShell
(Get-Cluster).BlockCacheSize
```

返される値は、サーバーあたり mebibytes (MiB) でです。 たとえば、 `1024` 1 gibibyte (GiB) を表します。

メモリの量の割り当てを変更するには、PowerShell を使用して、この値を変更します。 たとえば、サーバーあたり 2 GiB を割り当てるには、次のように実行します。

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

変更は直ちに有効、一時停止し、再開、CSV ボリュームまたはサーバー間を移動します。 たとえば、各 CSV を別のサーバー ノードに移動し、再度この PowerShell フラグメントを使用します。

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## 関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
