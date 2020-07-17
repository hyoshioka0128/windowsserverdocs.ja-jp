---
title: メモリ内読み取りキャッシュの記憶域スペースダイレクト
ms.prod: windows-server
ms.author: eldenc
manager: siroy
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 02/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: fff78ddc831ae9f6cba103d7630da3afec2c87d7
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474239"
---
# <a name="using-storage-spaces-direct-with-the-csv-in-memory-read-cache"></a>CSV インメモリ読み取りキャッシュでの記憶域スペースダイレクトの使用
> 適用先:Windows Server 2019、Windows Server 2016

このトピックでは、システムメモリを使用して[記憶域スペースダイレクト](storage-spaces-direct-overview.md)のパフォーマンスを向上させる方法について説明します。

記憶域スペースダイレクトは、メモリ内の読み取りキャッシュクラスターの共有ボリューム (CSV) と互換性があります。 システムメモリを使用して読み取りをキャッシュすると、Hyper-v などのアプリケーションのパフォーマンスを向上させることができます。 Hyper-v では、バッファーを使用しない i/o を使用して VHD または VHDX ファイルにアクセスします。 (バッファリングされていない IOs とは、Windows キャッシュマネージャーによってキャッシュされない操作のことです)。

メモリ内キャッシュはサーバーローカルであるため、ハイパー集約記憶域スペースダイレクト配置のデータの局所性が向上します。最近の読み取りは、仮想マシンが実行されているのと同じホスト上のメモリにキャッシュされるので、ネットワーク経由での読み取り回数を減らすことができます。 これにより、待機時間が短くなり、ストレージのパフォーマンスが向上します。

## <a name="planning-considerations"></a>計画に関する考慮事項

インメモリ読み取りキャッシュは、仮想デスクトップインフラストラクチャ (VDI) などの読み取り負荷の高いワークロードで最も効果的です。 逆に、ワークロードの書き込みが非常に多い場合は、キャッシュのオーバーヘッドが値より多くなり、無効にする必要があります。

CSV インメモリ読み取りキャッシュでは、合計物理メモリの最大80% を使用できます。

  > [!TIP]
  > コンピューティングとストレージが同じサーバー上で実行されるハイパー収束デプロイの場合は、仮想マシン用に十分なメモリを確保するように注意してください。 収束スケールアウトファイルサーバー (SoFS) のデプロイでは、メモリの競合が少ないため、この設定は適用されません。

  > [!NOTE]
  > DISKSPD や[VM](https://github.com/Microsoft/diskspd/tree/master/Frameworks/VMFleet)などの一部のマイクロベンチマークツールでは、CSV インメモリ読み取りキャッシュが有効になっていない場合に比べて、より悪い結果が生じる可能性があります。 既定では、VM は仮想マシンごとに 1 10 の GiB VHDX を作成し、100 Vm では約 1 TiB の合計を作成した後、*一様にランダム*な読み取りと書き込みを実行します。 実際のワークロードとは異なり、読み取りは予測可能パターンまたは反復パターンに従わないので、メモリ内キャッシュは有効ではなく、オーバーヘッドが発生します。

## <a name="configuring-the-in-memory-read-cache"></a>インメモリ読み取りキャッシュの構成

CSV インメモリ読み取りキャッシュは、Windows Server 2016 と Windows Server 2019 の両方で同じ機能を使用して利用できます。 Windows Server 2016 では、既定で無効になっています。 Windows Server 2019 では、既定で 1 GB が割り当てられています。

| OS バージョン          | 既定の CSV キャッシュサイズ |
|---------------------|------------------------|
| Windows Server 2016 | 0 (無効)           |
| Windows Server 2019 | 1 GiB                   |

PowerShell を使用して割り当てられているメモリの量を確認するには、次のように実行します。

```PowerShell
(Get-Cluster).BlockCacheSize
```

返される値は、サーバーごとに mebibytes (MiB) です。 たとえば、は `1024` 1 ギビバイト (GiB) を表します。

割り当てられるメモリの量を変更するには、PowerShell を使用してこの値を変更します。 たとえば、サーバーごとに2つの GiB を割り当てるには、次のように実行します。

```PowerShell
(Get-Cluster).BlockCacheSize = 2048
```

変更がすぐに有効になるようにするには、一時停止し、CSV ボリュームを再開するか、サーバー間で移動します。 たとえば、次の PowerShell フラグメントを使用して、各 CSV を別のサーバーノードに移動してから再び復元します。

```PowerShell
Get-ClusterSharedVolume | ForEach {
    $Owner = $_.OwnerNode
    $_ | Move-ClusterSharedVolume
    $_ | Move-ClusterSharedVolume -Node $Owner
}
```

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
