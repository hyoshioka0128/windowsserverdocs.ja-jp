---
title: 追加のステーションを MultiPoint server に接続する
description: MultiPoint Services のデプロイにステーションを追加する
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: d78ebf4e-0968-4014-9a42-9f75cc50cb52
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: f82cfb982d36e9d66ff5f951f65030f2f1d77539
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858735"
---
# <a name="attach-additional-stations-to-multipoint-services"></a>MultiPoint Services に追加のステーションをアタッチする
MultiPoint Services 環境では、ユーザーはステーションを使用して MultiPoint Services に接続し、作業を行います。 ステーションは、Multipoint Services を実行しているコンピューターに接続するためのユーザーエンドポイントです。  
  
MultiPoint services では、次の3種類のステーションがサポートされています。  
  
-   直接ビデオ接続ステーション  
  
-   USB ゼロクライアント接続ステーション (および USB over Ethernet 0 クライアント接続ステーション)  
  
-   RDP over LAN 接続されたステーション  
  
分類は、ステーションのハードウェアと、それが使用する接続の種類に基づいています。 ステーションの接続の種類を組み合わせることができます。 唯一の要件は、(前にインストールした) プライマリステーションが直接ビデオ接続ステーションであることです。 ステーションの設定の詳細については、「 [MultiPoint ステーション](MultiPoint-services-Stations.md)」を参照してください。  
  
各種類のステーションを設定する方法の詳細については、次を参照してください。  
  
-   [直接ビデオ接続ステーションをセットアップする](Set-up-a-direct-video-connected-station-in-MultiPoint-services.md)  
  
-   [USB ゼロ クライアント接続ステーションをセットアップする](Set-up-a-USB-zero-client-connected-station-in-MultiPoint-services.md)  
  
-   [RDP over LAN 接続ステーションをセットアップする](Set-up-an-RDP-over-LAN-connected-station-in-MultiPoint-services.md)  
  
ステーションの種類の詳細な比較については、「[ステーションの種類の比較](multipoint-services-stations.md#BKMK_StationTypeComparison)」を参照してください。  
  
> [!NOTE]  
> -   ステーションをアタッチする手順では、中間ハブや下流ハブを設定する方法については説明しません。 これらのハブをインストールする場所の詳細については、 [MultiPoint ステーション](MultiPoint-services-Stations.md)に関する説明を参照してください。  
> -   場合によっては、仮想マシンで実行されるステーション仮想デスクトップの作成が必要になることがあります。 たとえば、Windows Server にインストールできないアプリケーションや、同じホストコンピューターで複数のインスタンスを実行しないアプリケーションを使用しているとします。 詳細については、「[ステーション用の Windows 10 Enterprise 仮想デスクトップを作成する](Create-Windows-10-Enterprise-virtual-desktops-for-stations.md)」を参照してください。  
  
> [!TIP]  
> ステーションを物理的な場所の順序で作成し、MultiPoint Server で順番に識別されるようにすると便利です。 後でステーションの名前を変更する場合は、MultiPoint マネージャーで行うことができます。 詳細については、MultiPoint Server のヘルプとサポートですべてのステーションを再マップする方法に関する説明を参照してください。