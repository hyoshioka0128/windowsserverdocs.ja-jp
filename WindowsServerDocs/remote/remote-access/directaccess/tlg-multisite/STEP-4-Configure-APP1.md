---
title: 手順 4 APP1 を構成します。
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccfac583f64d40012881a2d3f6a0897beb16c02a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867223"
---
# <a name="step-4-configure-app1"></a>手順 4 APP1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

静的 IPv6 アドレスを構成し、2 Corpnet サブネットに APP1 を有効にするゲートウェイの設定にアクセスします。  
  
- 既定のゲートウェイと DNS サーバーを構成します。 マルチサイト構成では、デフォルト ゲートウェイとして ROUTER1 コンピューターを使用します。 APP1 で、既定のゲートウェイを構成します。  
  
## <a name="to-configure-the-default-gateway-and-dns-server"></a>既定のゲートウェイと DNS サーバーを構成するには  
  
1.  サーバー マネージャー コンソールで、次のようにクリックします。**ローカル サーバー**、し、**プロパティ**エリア、次へ を**ワイヤード (イーサネット) 接続**、リンクをクリックします。  
  
2.  **ネットワーク接続**ウィンドウで、右クリックして**ワイヤード (イーサネット) 接続**、順にクリックします**プロパティ**します。  
  
3.  **ワイヤード (イーサネット) 接続プロパティ**ダイアログ ボックスで、をクリックして**インターネット プロトコル バージョン 4 (Tcp/ipv4)**、順にクリックします**プロパティ**します。  
  
4.  **デフォルト ゲートウェイ**、型**10.0.0.254**、および**代替 DNS サーバー**、型**10.2.0.1**、 をクリックし、 **ok**.  
  
5.  **ワイヤード (イーサネット) 接続プロパティ**ダイアログ ボックスで、をクリックして**インターネット プロトコル バージョン 6 (Tcp/ipv6)**、順にクリックします**プロパティ**します。  
  
6.  **デフォルト ゲートウェイ**、型**2001:db8:1::fe**します。 **代替 DNS サーバー**、型**2001:db8:2::1**、 をクリックし、 **OK**。  
  
7.  **ワイヤード (イーサネット) 接続プロパティ**ダイアログ ボックスで、をクリックして**閉じます**、閉じて、**ネットワーク接続**ウィンドウ。  
  


