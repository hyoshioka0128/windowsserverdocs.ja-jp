---
title: DNS ポリシー シナリオ ガイド
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b3a1400a68e22fc4988c87c9222b66f718cf5fd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865643"
---
# <a name="dns-policy-scenario-guide"></a>DNS ポリシー シナリオ ガイド

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このガイドは、DNS、ネットワーク、およびシステム管理者の使用のものです。  
  
DNS のポリシーは、Windows server DNS の新しい機能&reg;2016。 このガイドを使用すると、DNS のポリシーを使用して、DNS サーバーがポリシーで定義する、さまざまなパラメーターに基づく名前解決クエリを処理する方法を制御するのに方法について説明します。   
  
このガイドには、プライマリの地理的場所ベースのトラフィック管理の目標を達成する DNS サーバーの動作を構成する方法について手順を提供する特定の DNS ポリシー シナリオと同様に DNS ポリシーの概要情報が含まれていて、セカンダリ DNS サーバー、アプリケーションの高可用性、スプリット ブレイン DNS、および詳細。  
  
このガイドは次のセクションで構成されます。  
  
- [DNS のポリシーの概要](DNS-Policies-Overview.md)  
- [Geo ロケーションの DNS ポリシーを使用するプライマリ サーバーのトラフィック管理のベース](primary-geo-location.md)  
- [地理的場所ベースのプライマリ セカンダリ展開でのトラフィック管理用に DNS ポリシーを使用します。](primary-secondary-geo-location.md)  
- [1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用します。](dns-tod-intelligent.md)
- [Azure の 1 日の時間に基づく DNS 応答のクラウド アプリケーション サーバー](dns-tod-azure-cloud-app-server.md)
- [スプリット ブレイン DNS 展開の DNS ポリシーを使用します。](split-brain-DNS-deployment.md)
- [Active Directory でスプリット ブレイン DNS の DNS ポリシーを使用します。](dns-sb-with-ad.md)
- [DNS クエリのフィルターを適用するために DNS ポリシーを使用します。](apply-filters-on-dns-queries.md)
- [アプリケーションの負荷分散に DNS ポリシーを使用します。](app-lb.md)
- [アプリケーションの負荷分散位置認識での DNS ポリシーを使用します。](app-lb-geo.md)

