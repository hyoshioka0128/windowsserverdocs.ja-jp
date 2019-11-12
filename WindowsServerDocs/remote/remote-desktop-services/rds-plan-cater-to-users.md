---
title: リモート デスクトップ サービスのさまざまな種類のユーザーの要求を満たす
description: RDS のユーザーのさまざまな種類について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da522a18-c33f-468e-b9d6-3ad7d3cfba26
author: spatnaik
ms.author: spatnaik
ms.date: 11/06/2019
manager: scottman
ms.openlocfilehash: dc83d76dbfaded9dadae7c16ae9e1c8df7958a7d
ms.sourcegitcommit: d25e47a54a120b9bc26ff43597518fca58c1cc5b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73753820"
---
# <a name="remote-desktop-services---cater-to-different-kinds-of-users"></a>リモート デスクトップ サービスのさまざまな種類のユーザーの要求を満たす

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

リモート デスクトップ サービスは、さまざまな種類のワークロードをサポートします。 ユーザーの種類ごとの予想されるニーズに応じて、展開を拡張できます。

## <a name="types-of-users"></a>ユーザーの種類

### <a name="knowledge-user"></a>ナレッジ ユーザー

ナレッジ ユーザーは、Microsoft Word、Excel、Outlook、Microsoft Edge ブラウザーなどの軽量な生産性アプリケーションを使用します。

ナレッジ ユーザーの場合、仮想 CPU (vCPU) ごとにユーザー 4 人を超えないようにします。

### <a name="professional-user"></a>プロフェッショナル ユーザー

プロフェッショナル ユーザーは、インターネット ブラウザーや生産性アプリケーションに加えて、ソフトウェアの開発やマルチメディア コンテンツの作成など、より負荷の高いワークロードをサポートします。

プロフェッショナル ユーザーの場合、vCPU あたりユーザー 2 人を超えないようにします。

### <a name="power-user"></a>パワー ユーザー

パワー ユーザーは、コンピューター支援設計 (CAD) や Adobe Photoshop などのエンジニアリングとグラフィックスのアプリケーションを使用します。 ビデオ レンダリング、3D デザイン、シミュレーションのためにグラフィック集中型のプログラムを定期的に使用するユーザーには、多くの場合 GPU が適しています。

パワー ユーザーの場合、vCPU あたりユーザー 1 人を超えないようにします。

グラフィックス アクセラレーションの詳細については、「[どちらのグラフィックス仮想化テクノロジが適切か](rds-graphics-virtualization.md)を参照してください。

Azure には、他のグラフィックス アクセラレーション展開オプションと、使用可能な複数の GPU VM サイズがあります。 これらについては、「[GPU 最適化済み仮想マシンのサイズ](https://docs.microsoft.com/azure/virtual-machines/windows/sizes-gpu)」を参照してください。

## <a name="test-workload"></a>ワークロードのテスト

ストレス テストと実際の使用状況のシミュレーションの両方で、デプロイのロード テストを行うことをお勧めします。 シミュレーション ツールを使用して、デプロイのロード テストを行うことができます。 システムがユーザーのニーズを満たすのに十分な応答性と回復性を備えていることを確認し、予想外の事態を避けるために、ロード サイズを変更してください。
