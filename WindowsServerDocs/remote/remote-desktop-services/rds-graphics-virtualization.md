---
title: RDS でグラフィックス仮想化テクノロジが適切でしょうか。
description: 最適なグラフィックス、RDS デプロイ用の仮想化オプションを選択するのに役立つ計画情報。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/16/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d6ff5b22-7695-4fee-b1bd-6c9dce5bd0e8
author: lizap
manager: scottman
ms.openlocfilehash: 7cf7fdf3510fcaaa955bd0031fb3564fe4372472
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875803"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>グラフィックスの仮想化テクノロジは、適切なでしょうか。

リモート デスクトップ サービスでのグラフィックス レンダリングを有効にする際に、さまざまなオプションがあります。 仮想化環境を計画する際に、次の考慮事項は、どのグラフィックスのレンダリングのテクノロジを選択をドライブします。

![グラフィックスのレンダリングに関する考慮事項 - 比較ユーザー スケールと GPU の要件、環境に最適な GPU テクノロジを判断するには](media/rds-gpu.png)

Windows Server 2016 では、GPU ハードウェアを活用できる HYPER-V で使用可能な 2 つのグラフィックス仮想化テクノロジがあります。

- [独立したデバイスの割り当て (DDA)](#discrete-device-assignment) – 1 つまたは複数の Gpu を使用して、最高のパフォーマンスは、VM 内でネイティブの GPU ドライバーのサポートを提供する VM に専用の場合。 密度が低いサーバーで使用可能な物理 Gpu の数によって制限されますです。 
- [リモート FX vGPU](#remotefx-vgpu) - ナレッジ ワーカーおよび高バースト GPU シナリオが複数の Vm が para 仮想化を通じて 1 つまたは複数の Gpu を活用します。 このソリューションでは、サーバーごとの高いユーザー密度を提供します。

次の図では、Windows Server 2016 では、グラフィックス仮想化のオプションを示します。

![RDS での Windows Server 2016 でのグラフィックス仮想化のオプションは使用可能な 3 つのテクノロジとスケールとパフォーマンスの違いを示しています。](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>個別のデバイスの割り当て
独立したデバイスの割り当て (DDA) は、VM があるネイティブのドライバーを使用して GPU へのフル アクセスを最高のパフォーマンスを提供するハードウェアのパススルー ソリューションです。 VM ユーザーとデバイスのネイティブ ドライバーも自分のデバイスのすべての機能にアクセスできます。 つまり、同じデバイスをベア メタルで実行されている VM のミラーでデバイスを実行する機能。

DDA に関する詳細については、チェック アウト[の個別のデバイスの割り当ての展開を計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)します。

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU は、ナレッジ ワーカーのシナリオ (上記の最初の図を参照してください) を有効にする、さまざまなゲスト オペレーティング システムに分割される GPU の処理能力を許可するグラフィックスの仮想化テクノロジです。 Windows Server 2016 の進歩は、GPU バーストのシナリオでのアプリケーションとデータ視覚化のデザイナーなどのさらなる機能強化を使用できます。 その他の機能強化は次のとおりです。

-   第 2 世代ゲスト Vm、Windows Server 2016 ゲスト Vm、および Windows クライアント、HYPER-V ホストをサポートします。
   >[!NOTE] 
   > Windows Server 2016 ゲスト VM にリモート デスクトップ セッション ホストがサポートされていませんWindows Server 2016 ゲスト VM あたり 1 つだけセッションをホストできます。

-   強化されたアプリケーションの互換性と安定性。
-   VM 接続拡張セッション モード、RemoteFX vGPU を有効になっている VM に接続する VM で USB とクリップボードのリダイレクトを許可します。

詳細については、チェック アウト[設定 for Remote Desktop Services の RemoteFX vGPU の構成のセットアップと](rds-remotefx-vgpu.md)します。

## <a name="which-should-you-use"></a>これを使用する必要がありますか。

重要な考慮事項をどの仮想化テクノロジがハードウェアの仕様または環境内でアプリケーションの要件に依存可能性があります。 DDA および RemoteFX vGPU の機能に関する簡単なテーブルを次に示します。

| 機能               | RemoteFX vGPU                                                                       | 個別のデバイスの割り当て                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| GPU とデバイスの割り当て | Para 仮想化 (多数の Vm を 1 つまたは複数の Gpu)                                     | 1 つの VM に 1 つ以上の GPU                                                  |
| Scale                 | スケールのベスト/1 GPU を多数の Vm                                                      | スケールが低い/1 の VM に 1 つ以上の Gpu                                     |
| アプリケーションの互換性     | DX 11.1、OpenGL 4.4、OpenCL 1.1                                                     | (DX 12、OpenGL、CUDA) ベンダーから提供されるすべての GPU 機能          |
| AVC444                | (Windows 10 および Windows Server 2016)、既定で有効になっています。                             | グループ ポリシー (Windows 10 および Windows Server 2016) を利用    |
| GPU VRAM              | 最大 1 GB の専用 VRAM                                                           | GPU でサポートされている VRAM まで                                        |
| フレーム レート            | 最大 30 fps                                                                         | 最大 60 fps                                                            |
| ゲストでの GPU ドライバー   | RemoteFX 3D アダプター ディスプレイ ドライバー (マイクロソフト)                                      | GPU ベンダー ドライバー (Nvidia、AMD、Intel)                                 |
| ゲスト OS のサポート      |  Windows Server 2012 R2 Windows Server 2016 の Windows 7 SP1 を Windows 8.1 の Windows 10 |  Windows Server 2012 R2 Windows Server 2016 の Windows 10 の Linux         |
| ハイパーバイザー            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| ホスト OS の可用性  |  Windows Server 2012 R2  Windows Server 2016 Windows 10                             | Windows Server 2016                                                    |
| GPU ハードウェア          | エンタープライズの Gpu (Nvidia Quadro/グリッドまたは AMD FirePro)                         | エンタープライズの Gpu (Nvidia Quadro/グリッドまたは AMD FirePro)            |
| サーバー ハードウェア       | 特別な要件はありません。                                                             | 最新のサーバー OS (通常は準拠しているハードウェアの SR-IOV) に IOMMU を公開します。 |

一般的な経験則では、仮想マシンは GPU への直接アクセスであるために、最適なアプリケーションの互換性に関する DDA を使用します。 GPU の厳格な要件として、アプリケーションまたはワークロードがないユーザーの広いベース サーバーにする場合は、RemoteFX vGPU が自分に最適です。