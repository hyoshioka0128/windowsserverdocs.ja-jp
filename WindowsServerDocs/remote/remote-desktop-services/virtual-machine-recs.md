---
title: 仮想マシンのサイズ設定
description: 各ワークロードの種類の推奨サイズ。
ms.author: helohr
ms.date: 12/02/2019
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 6ddc3b14fbf068405e0145f7342ea27a8f51a5af
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970099"
---
# <a name="virtual-machine-sizing-guidelines"></a>仮想マシンのサイズ設定のガイドライン

リモート デスクトップ サービスまたは Windows 仮想デスクトップのどちらで仮想マシンを実行している場合でも、ワークロードの種類ごとに異なるセッション ホスト仮想マシン (VM) 構成が必要です。 最適なエクスペリエンスを実現するには、ユーザーのニーズに応じてデプロイをスケールします。

## <a name="multi-session-recommendations"></a>複数セッションに関する推奨事項

仮想中央処理ユニット (vCPU) あたりの推奨される最大ユーザー数と、各ワークロードの最小 VM 構成を次の表に示します。 これらの推奨事項は、[リモート デスクトップのワークロード](remote-desktop-workloads.md)に基づいています。

| ワークロードの種類 | vCPU あたりの最大ユーザー数 | vCPU/RAM/OS ストレージの最小値 | Azure インスタンスの例 | プロファイル コンテナー ストレージの最小値 |
| --- | --- | --- | --- | --- |
| 淡色 | 6 | 2 vCPUs、8 GB RAM、16 GB ストレージ | D2s_v3、F2s_v2 | 30 GB |
| 中間 | 4 | 4 vCPUs、16 GB RAM、32 GB ストレージ | D4s_v3、F4s_v2 | 30 GB |
| ヘビー | 2 で保護されたプロセスとして起動されました | 4 vCPUs、16 GB RAM、32 GB ストレージ | D4s_v3、F4s_v2 | 30 GB |
| Power | 1 | 6 vCPUs、56 GB RAM、340 GB ストレージ | D4s_v3、F4s_v2、NV6 | 30 GB |

## <a name="single-session-recommendations"></a>シングルセッションの推奨事項

シングルセッション シナリオの VM のサイズ設定の推奨事項については、VM あたり少なくとも 2 つの物理 CPU コア (通常、ハイパースレッディング搭載の 4 つの vCPU) をお勧めします。 シングルセッション シナリオの VM のサイズ設定について具体的な推奨事項が必要な場合は、実際のワークロードに固有のソフトウェア ベンダーに問い合わせてください。 シングルセッション VM の VM のサイズ設定は、多くの場合、物理デバイスのガイドラインに合わせて調整されます。

## <a name="general-virtual-machine-recommendations"></a>一般的な仮想マシンの推奨事項

オペレーティング システムを実行するための VM の要件については、[Windows 10 コンピューターの仕様とシステム要件](https://www.microsoft.com/windows/windows-10-specifications)に関する記事を参照してください。

サービス レベル アグリーメント (SLA) が必要な運用環境のワークロードには、OS ディスクで Premium SSD ストレージを使用することをお勧めします。 詳細については、「[Virtual Machines の SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_8/)」を参照してください。

ビデオ レンダリング、3D デザイン、シミュレーションのためにグラフィック集中型のプログラムを定期的に使用するユーザーには、多くの場合、グラフィックス プロセッシング ユニット (GPU) が適しています。 グラフィックス アクセラレーションの詳細については、[グラフィックス レンダリング テクノロジの選択](rds-graphics-virtualization.md)に関する記事を参照してください。 Azure には、いくつかのグラフィックス アクセラレーション展開オプションと、使用可能な複数の GPU VM サイズがあります。 詳細については、「[GPU 最適化済み仮想マシンのサイズ](/azure/virtual-machines/windows/sizes-gpu)」を参照してください。

[負荷の急増に対応できる B シリーズ VM](/azure/virtual-machines/windows/b-series-burstable) は、最大 CPU パフォーマンスを常に必要としないユーザーに適しています。 VM の種類とサイズの詳細については、「[Azure の Windows 仮想マシンのサイズ](/azure/virtual-machines/windows/sizes)」、価格情報については、[Microsoft の Virtual Machines シリーズのページ](https://azure.microsoft.com/pricing/details/virtual-machines/series/)を参照してください。

## <a name="test-your-workload"></a>ワークロードをテストする

最後に、ストレス テストと実際の使用状況シミュレーションの両方でデプロイをテストするために、シミュレーション ツールを使用することをお勧めします。 システムがユーザーのニーズを満たすのに十分な応答性と回復性を備えていることを確認し、予想外の事態を避けるために、ロード サイズを変更してください。
