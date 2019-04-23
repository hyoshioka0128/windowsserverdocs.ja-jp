---
title: その他の局を MultiPoint サーバーにアタッチします。
description: ステーションを MultiPoint Services の展開に追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d78ebf4e-0968-4014-9a42-9f75cc50cb52
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 57fc8ed6774c3266298ecd98e8f609ec01f63ef6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889263"
---
# <a name="attach-additional-stations-to-multipoint-services"></a>その他の局を MultiPoint Services に接続します。
、MultiPoint サービス環境内では、ユーザーは、ステーションを MultiPoint Services に接続し、自分の作業に使用します。 ステーションとは、Multipoint Services を実行しているコンピューターに接続するためのユーザーのエンドポイントです。  
  
MultiPoint services では、ステーションの 3 つの種類をサポートします。  
  
-   直接ビデオ接続ステーション  
  
-   USB ゼロ クライアント接続ステーション (および Ethernet 0 クライアント接続ステーションで USB)  
  
-   RDP over LAN 接続されたステーション  
  
分類は、ステーションのハードウェアおよび使用する接続の種類に基づいています。 混在させるし、ステーションの接続の種類に一致できます。 唯一の要件は、(これは、インストールした) プライマリ ステーションは、直接ビデオ接続ステーションである必要があります。 ステーションのセットアップの詳細については、次を参照してください。 [MultiPoint ステーション](MultiPoint-services-Stations.md)します。  
  
各タイプのステーションを設定する方法を説明する手順については、次を参照してください。  
  
-   [直接ビデオ接続ステーションのセットアップします。](Set-up-a-direct-video-connected-station-in-MultiPoint-services.md)  
  
-   [可能な USB ゼロ クライアント接続ステーションを設定します。](Set-up-a-USB-zero-client-connected-station-in-MultiPoint-services.md)  
  
-   [RDP over LAN 接続ステーションのセットアップします。](Set-up-an-RDP-over-LAN-connected-station-in-MultiPoint-services.md)  
  
ステーションの種類の詳細な比較についてを参照してください。[ステーション型の比較](multipoint-services-stations.md#BKMK_StationTypeComparison)します。  
  
> [!NOTE]  
> -   ステーションをアタッチするための手順では、中間のハブまたはダウン ストリーム ハブを設定する方法は説明しません。 これらのハブをインストールする場所については、次を参照してください。 [MultiPoint ステーション](MultiPoint-services-Stations.md)します。  
> -   場合によっては、仮想マシンで実行される、仮想デスクトップ ステーションを作成する必要もあります。 たとえば、Windows Server にインストールできないアプリケーションや、同じホスト コンピューターで複数のインスタンスが実行されないアプリケーションを使用します。 詳細については、次を参照してください。[作成 Windows 10 Enterprise の仮想デスクトップ ステーションを](Create-Windows-10-Enterprise-virtual-desktops-for-stations.md)します。  
  
> [!TIP]  
> MultiPoint Server で順番に識別するために、その物理的な場所の順序、ステーションを作成すると便利です。 後で、ステーションの名前を変更する場合、MultiPoint マネージャーを実行できます。 詳細については、MultiPoint Server のヘルプとサポートですべてステーションを再マップを参照してください。