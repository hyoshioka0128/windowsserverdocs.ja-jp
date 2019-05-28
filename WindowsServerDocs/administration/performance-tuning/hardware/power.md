---
title: サーバー ハードウェアの電源に関する考慮事項
description: サーバー ハードウェアの電源に関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5fe91888188796c96d5da80e8f9bd3ed627b9d43
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564740"
---
# <a name="server-hardware-power-considerations"></a>サーバー ハードウェアの電源に関する考慮事項

Enterprise およびデータ センター環境でエネルギー効率の向上の重要性を認識する重要です。 高パフォーマンスと低エネルギーの使用状況は多くの場合、競合する目標は、サーバー コンポーネントを慎重に選択するには、適切なバランスを実現できます。 次のセクションでは、電源の特性と機能のサーバーのハードウェア コンポーネントのためのガイドラインを一覧表示します。

## <a name="processor-recommendations"></a>プロセッサに関する推奨事項

頻度、電圧、キャッシュ サイズ、およびプロセスのテクノロジの動作では、プロセッサの電力消費量に影響します。 その他のモデルの基準としたエネルギー消費量の基本の明示 (TDP) 評価ポイント熱設計になっているプロセッサ。

一般に、最下位のパフォーマンスの目標を満たす TDP プロセッサを選択します。 また、新しい世代のプロセッサは一般的に、エネルギー効率が高い、Windows の電源管理アルゴリズムの複数の電源状態を失う可能性がありますが、パフォーマンスのすべてのレベルより優れた電源管理を有効にします。 または、ハードウェア メーカーと共同でマイクロソフトが開発した新しい「協調」の電源管理の手法の一部を使用することががあります。

協調電源管理の手法の詳細についてで共同作業のプロセッサ パフォーマンスの制御をという名前のセクションを参照してください、 [Advanced Configuration and Power Interface Specification](http://www.uefi.org/sites/default/files/resources/ACPI_5_1release.pdf)します。


## <a name="memory-recommendations"></a>メモリの推奨事項
メモリ合計システム電源の増加の割合を占めています。 多くの要因では、メモリのテクノロジ、エラー訂正コード (ECC)、バスの頻度、容量、密度、ランクの数などのメモリ DIMM の電力消費量に影響します。 そのため、大量のメモリを購入する前に、予想される電源評価を比較することをお勧めします。

低電力のメモリは、使用できるようになりましたが、パフォーマンスとコストのトレードオフを考慮する必要があります。 場合は、サーバーはページングは、ページング ディスクのエネルギー コストも考慮する必要があります。


## <a name="disks-recommendations"></a>ディスクの推奨事項
高い RPM では、増加のエネルギー消費量を意味します。 SSD ドライブには、回転ドライブより効率的な多くの電力です。 また、2.5 インチ ドライブでは、通常の 3.5 インチ ドライブよりも電力が必要です。

## <a name="network-and-storage-adapter-recommendations"></a>ネットワークと記憶域アダプターに関する推奨事項
一部のアダプターは、アイドル状態のときのエネルギー消費量を減らします。 これは、10 Gb ネットワーク アダプターと高帯域幅 (4 ~ 8 Gb) のストレージのリンクの重要な考慮事項です。 このようなデバイスでは、大量のエネルギーを使用できます。


## <a name="power-supply-recommendations"></a>電源装置の推奨事項
電源効率の向上は、パフォーマンスに影響を与えずにエネルギー消費量を削減する優れた方法です。 効率の高い電源装置には、サーバーごとの 1 年あたり多く kilowatt-hours を保存できます。


## <a name="fan-recommendations"></a>ファンの推奨事項
ファン、電源などは、領域をシステムのパフォーマンスに影響を与えずにエネルギー消費量を減らすことができます。 可変速度のファンでは、システムの負荷が排除することの不要なエネルギー消費量として RPM を減らすことができます。


## <a name="usb-devices-recommendations"></a>USB デバイスの推奨事項
既定では USB デバイスの選択的な Windows Server 2016 有効を中断します。 ただし、デバイス ドライバーは、かなりのマージンでシステムのエネルギー効率が中断されることができます。 潜在的な問題を避けるためには、USB デバイスを切断や、BIOS で無効にする USB デバイスを必要としないサーバーを選択します。


## <a name="remotely-managed-power-strip-recommendations"></a>リモートで管理されている電源ストリップの推奨事項
電源タップは、サーバーのハードウェアの不可欠な部分ではありませんが、データ センターで大きな差を行えるように。 測定値は、プラグが差し込まれているが、オフ、表面上利用したボリュームのサーバーが最大 30 ワットの電力を要求することも説明します。

電力を浪費を回避するには、プログラムで特定のサーバーからの電源を切断するサーバーの各ラックのリモートに管理される電源ストリップをデプロイできます。

## <a name="processor-terminology"></a>プロセッサの用語集
このトピック全体で使用されるプロセッサの用語では、次の図で使用可能なコンポーネントの階層が反映されます。 次のコンポーネントの最小粒度に、大きい方から使用される用語に示します。

-   プロセッサ ソケット
-   NUMA ノード (NUMA node)
-   Core
-   論理プロセッサ

![プロセッサの用語集](../media/perftune-guide-figure-1.png)

## <a name="see-also"></a>関連項目
- [サーバー ハードウェアのパフォーマンスに関する考慮事項](index.md)
- [電源とパフォーマンスのチューニング](power/power-performance-tuning.md)
- [プロセッサの電源管理チューニング](power/processor-power-management-tuning.md)
- [推奨されるバランスのプラン パラメーター](power/recommended-balanced-plan-parameters.md)
