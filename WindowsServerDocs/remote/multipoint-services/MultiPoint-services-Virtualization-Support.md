---
title: MultiPoint Services の仮想化のサポート
description: Hyper-v で MultiPoint Services を使用する方法について説明します。
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 3f0864b8-a087-4890-94ef-05efbd3c4241
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: d23034b6a70d36df259fc26829b36ebebeade5ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857625"
---
# <a name="multipoint-services-virtualization-support"></a>MultiPoint Services の仮想化のサポート
MultiPoint Services は、次の2つの方法で Hyper-v の役割をサポートします。  
  
-   MultiPoint サービスは、Hyper-v を実行しているサーバー上のゲストオペレーティングシステムとして展開できます。  
  
-   MultiPoint Services は、仮想化サーバーとして使用できます。   
  
仮想マシンで MultiPoint Services を実行すると、Hyper-v ツールを使用してオペレーティングシステムを管理できます。 これらのツールには、チェックポイント機能とロールバック機能が含まれており、仮想マシンのエクスポートとインポートを行うことができます。 大規模なインストールでは、1台の物理サーバー上で複数の MultiPoint Services 仮想コンピューターを実行してサーバーを統合できます。 次のようなシナリオが想定されます。  
  
-   1つのクラスルームまたはラボに20台を超えるシートがあります。 MultiPoint Services を実行する複数の物理コンピューターを展開するのではなく、複数の仮想マシンを1台の物理コンピューターに展開することができます。  
  
    > [!NOTE]  
    > 1つの MultiPoint マネージャーコンソールを使用して、物理または仮想の複数の MultiPoint server を管理できます。  
  
-   MultiPoint server は、同じ物理コンピューター上の別のサーバーインフラストラクチャを持つ仮想マシン上で実行されています。 この場合、このサーバーインフラストラクチャによって、ネットワークのドメイン、セキュリティ、およびデータが一元化されます。 MultiPoint server は、デスクトップをリモートデスクトップサービスし、一元化します。  
  
> [!NOTE]  
> 仮想マシンで MultiPoint Services を実行している場合は、USB over Ethernet および RDP クライアントステーションがサポートされています。 ダイレクトビデオと USB ゼロクライアント接続ステーションはサポートされていません。  
  
Hyper-v の役割の詳細については、「 [hyper-v](../../virtualization/hyper-v/hyper-v-on-windows-server.md)」を参照してください。  