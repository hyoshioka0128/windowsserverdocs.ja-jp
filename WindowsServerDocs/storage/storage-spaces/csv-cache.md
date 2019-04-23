---
title: 記憶域スペース ダイレクト-メモリ内キャッシュを読み取る
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7ed5894a569d4c42a3a4b0e018de5171f2c84a62
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850553"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>CSV のインメモリで記憶域スペース ダイレクトを使用してキャッシュを読み取る
> 適用先:Windows Server 2016、Windows Server 2019

このトピックでは、システム メモリを使用してのパフォーマンスを向上する方法を説明します。[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)します。

記憶域スペース ダイレクトは、クラスター共有ボリューム (CSV) のインメモリ キャッシュを読み取るとの互換性です。 システム メモリ キャッシュの読み取りに使用すると、VHD または VHDX ファイルにアクセスするバッファなし I/O を使用する HYPER-V などのアプリケーションのパフォーマンスを向上できます。 (バッファなし IOs、Windows のキャッシュ マネージャーによってキャッシュされないすべての操作です)。

ハイパーコンバージド記憶域スペース ダイレクト展開のデータの局所性が向上するメモリ内キャッシュがローカル サーバーであるため、:、最近の読み取りはキャッシュで、仮想マシンが実行されている同じホスト上のメモリをどのくらいの頻度を減らす読み取り移動、ネットワーク経由でします。 これにより、低待機時間と記憶域のパフォーマンスが向上します。

## <a name="planning-considerations"></a>計画時の注意事項

メモリの読み取りキャッシュは読み取りが集中するワークロードを仮想デスクトップ インフラストラクチャ (VDI) などの最も効果的です。 逆に、作業負荷が非常に書き込み中心の場合は、キャッシュ値よりも多くのオーバーヘッドを生じる可能性があり、無効にする必要があります。

インメモリ CSV 読み取りキャッシュの合計物理メモリの最大 80% を使用することができます。

  > [!TIP]
  > ハイパー コンバージド展開では、コンピューティング、および記憶域が同じサーバー上で実行する仮想マシンに十分なメモリのままにするように注意してください。 収束のスケール アウト ファイル サーバー (SoFS) 展開は、メモリ、競合が減りで、この適用されません。

  > [!NOTE]
  > DISKSPD などの特定の microbenchmarking ツールと[VM Fleet](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet)悪い結果が生じる、csv 形式でメモリ内の読み取りキャッシュをよりもなしで有効にします。 既定で Fleet を VM 10 GiB あたり約 1 TiB の仮想マシン – VHDX 100 の vm を合計し、実行する 1 つ作成します*一様乱数*それらに対して読み取りし、書き込み。 実際のワークロードとは異なり、読み取りはメモリ内キャッシュが有効ではなく、オーバーヘッドが発生したため、予測可能なや反復的なパターンを実行しないでください。

## <a name="configuring-the-in-memory-read-cache"></a>キャッシュの読み取りでメモリを構成します。

CSV、インメモリの読み取りキャッシュが同じ機能の Windows Server 2016 および Windows Server 2019 の両方で利用できます。 Windows Server 2016 では、これは既定で無効です。 Windows Server 2019 は既定で 1 gb が割り当てられます。

| OS バージョン          | CSV キャッシュの既定のサイズ |
|---------------------|------------------------|
| Windows Server 2016 | 0 (無効)           |
| Windows Server 2019 | 1 giB                   |

PowerShell を使用して、割り当てるメモリ量を表示するには、次のコマンドを実行します。

```PowerShell
(Get-Cluster).BlockCacheSize
```

返される値が、サーバーあたり mebibytes (MiB)。 たとえば、 `1024` 1 ギビバイト (GiB) を表します。

割り当てられているメモリの量を変更するには、PowerShell を使用してこの値を変更します。 たとえば、サーバーあたり 2 GiB を割り当てるには、次のように実行します。

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

変更を有効にするには、すぐに、一時停止または、CSV ボリュームを再開し、サーバー間で移行します。 たとえば、各 CSV を別のサーバー ノードに移動し、再びこの PowerShell のフラグメントを使用します。

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
