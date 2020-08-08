---
title: 記憶域スペース ダイレクトのパフォーマンス チューニング
description: このトピックで説明するように、記憶域スペース ダイレクトは、使用するハードウェアのキャッシュ構成に基づいて自動的にパフォーマンスを調整します。
ms.topic: article
ms.assetid: 15a519fa-37cc-4d84-a9fe-097d33bb71ea
author: phstee
ms.author: vshankar; danlo; clausjor; stevenek
ms.date: 4/14/2017
ms.openlocfilehash: 18dca2080a311a337e0d41055e95e7a7f0f42a80
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991986"
---
# <a name="performance-tuning-for-storage-spaces-direct"></a>記憶域スペース ダイレクトのパフォーマンス チューニング

記憶域スペース ダイレクトは Windows Server ベースのソフトウェア定義記憶域ソリューションであり、自動的にパフォーマンスを調整するので、列数、使用するハードウェアのキャッシュ構成、および共有 SAS 記憶域ソリューションで手動で設定する必要があるその他の要因を手動で指定する必要がなくなります。 背景情報については、[Windows Server 2016 の記憶域スペース ダイレクト](../../../../storage/storage-spaces/storage-spaces-direct-overview.md)に関する記事を参照してください。

記憶域スペース ダイレクトのソフトウェア記憶域バスのキャッシュは、システムに存在する記憶域の種類に基づいて自動的に構成されます。 次の 3 種類が認識されます。**HDD**、**SSD**、**NVMe**。 キャッシュは、必要に応じて、読み取りや書き込みキャッシュ用に最速の記憶域を要求し、データの永続的な記憶域用にはより低速の記憶域を使用します。

次の表は、既定値をまとめたものです。

| 記憶域の種類 | キャッシュの構成 |
| --- | --- |
| 任意の 1 種類 | 存在する記憶域の種類が 1 つのみの場合、ソフトウェア記憶域バスのキャッシュは構成されません。 |
| SSD+HDD または NVMe+HDD | 最速の記憶域はキャッシュ レイヤーとして構成され、読み取りと書き込みの両方をキャッシュします。 |
| SSD+SSD または NVMe+NVMe | このような高速 + 高速オプションは、たとえば、キャッシュのためには 1 日当たり 10 ドライブ書き込みの (DWPD) NAND フラッシュ SSD、容量のためには 1.5 DWPD NAND フラッシュ SSD など、耐久性の高い記憶域と低い記憶域の組み合わせを対象としています。 キャッシュ デバイスの識別に使用する一連のモデル文字列を記憶域スペース ダイレクトに付与することで、これを実現します。 詳細については、[Enable-StorageSpacesDirect](https://technet.microsoft.com/library/mt589697.aspx) コマンドレット リファレンス (`CacheDeviceModel`) を参照してください。 <br><br>高速 + 高速システムでは、書き込みのみがキャッシュされます。 読み取りはキャッシュされません。 |

SSD または NVMe デバイスを介したキャッシュの既定は書き込みのキャッシュのみであることに注意してください。 その目的は、容量デバイスは高速なので、読み取りコンテンツをキャッシュ デバイスに移動するときに制限値を適用することです。 これには該当しない場合がありますが、読み取りキャッシュを有効にすると、パフォーマンスが向上しなくてもキャッシュ デバイスの耐久性が不必要に消費される可能性があるので、注意が必要です。 次のような例があります。

* **NVme + SSD** 読み取りキャッシュを有効にすると、読み取り IO は、集計された SSD と比較して、PCIe 接続や NVMe デバイスの高い IOPS パフォーマンスを利用できます。 <br>これは、NVMe デバイスと SSD に接続する HBA との相対的な帯域幅機能があるため、帯域幅指向のシナリオに "_該当する可能性があります_"。 パフォーマンスの向上を実現できる前に、IOPS の CPU コストによってシステムが制限される場合がある IOPS 指向のシナリオでは、"_該当しない可能性があります_"。
* **NVMe+NVMe** 同様に、キャッシュ NVMe の読み取り機能が合計容量の NVMe よりも高い場合、読み取りキャッシュを有効にする価値がある可能性があります。 <br>このような構成に適している読み取りキャッシュのケースはまれであると考えられます。

キャッシュ構成を表示および変更するには、[Get-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt634616.aspx) および [Set-ClusterStorageSpacesDirect](https://technet.microsoft.com/library/mt763265.aspx) コマンドレットを使用します。 `CacheModeHDD` および `CacheModeSSD` プロパティは、指定された種類の容量メディア上でキャッシュがどのように機能するかを定義します。

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペース ダイレクトについて](../../../../storage/storage-spaces/understand-the-cache.md)
- [記憶域スペース ダイレクトの計画](../../../../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)
- [ファイル サーバーのパフォーマンス チューニング](../../role/file-server/index.md)
- [ソフトウェア定義記憶域の設計に関する考慮事項ガイド](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/mt243829(v=ws.11)) (Windows Server 2012 R2 および共有 SAS 記憶域用)