---
title: MultiPoint Services の仮想化のサポート
description: MultiPoint Services、HYPER-V を使用する方法について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 06d518dcea154ac2bab49a7d0e83a90f96be6e44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872523"
---
# <a name="multipoint-services-virtualization-support"></a>MultiPoint Services の仮想化のサポート
MultiPoint Services では、2 つの方法で、Hyper-v の役割をサポートします。  
  
-   MultiPoint Services は、HYPER-V を実行しているサーバー上のゲスト オペレーティング システムとして展開できます。  
  
-   MultiPoint Services は、仮想化サーバーとして使用できます。   
  
MultiPoint Services を仮想マシンで実行されているオペレーティング システムを管理する HYPER-V ツールの使用を提供します。 これらのツールは、チェックポイントとロールバックの機能を含めるし、エクスポートし、仮想マシンをインポートすることができます。 大規模なインストールの場合、1 台の物理サーバーで複数の MultiPoint Services の仮想コンピューターを実行してサーバーを統合できます。 次のようなシナリオが想定されます。  
  
-   1 つのクラスルームまたはラボは、20 を超えるシートを持っています。 MultiPoint Services を実行している複数の物理コンピューターを展開するのではなく、1 台の物理コンピューター上の複数の仮想マシンをデプロイできます。  
  
    > [!NOTE]  
    > 物理または仮想、単一の MultiPoint マネージャー コンソールを使用するかどうかは、複数の MultiPoint サーバーを管理できます。  
  
-   MultiPoint server は、同じ物理コンピューター上の別のサーバー インフラストラクチャと仮想マシンで実行しています。 その場合はこのサーバー インフラストラクチャは、ドメイン、セキュリティ、およびネットワークのデータを一元化します。 MultiPoint サーバーでは、リモート デスクトップ サービスを提供し、デスクトップの一元化します。  
  
> [!NOTE]  
> 仮想マシンで MultiPoint Services を実行するときに、USB over Ethernet と RDP クライアント ステーションがサポートされます。 直接のビデオと USB ゼロ クライアント接続ステーションがサポートされていません。  
  
HYPER-V ロールの詳細については、次を参照してください。 [Hyper-v](../../virtualization/hyper-v/hyper-v-on-windows-server.md)します。  