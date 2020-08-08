---
title: DNS ポリシー シナリオ ガイド
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 50fdb08a-bbd8-4107-954a-6699672110ff
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ed28fe6dd472b505d2a39ac55c74c399ef63e068
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966659"
---
# <a name="dns-policy-scenario-guide"></a>DNS ポリシー シナリオ ガイド

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このガイドは、DNS、ネットワーク、およびシステム管理者が使用することを目的としています。

DNS ポリシーは、Windows Server 2016 の DNS の新機能です &reg; 。 このガイドを使用すると、dns ポリシーを使用して、ポリシーで定義したさまざまなパラメーターに基づいて、DNS サーバーが名前解決のクエリをどのように処理するかを制御できます。

このガイドでは、dns ポリシーの概要について説明します。また、プライマリおよびセカンダリ DNS サーバーの地理的な場所ベースのトラフィック管理、アプリケーションの高可用性、スプリットブレイン DNS など、目標を達成するために DNS サーバーの動作を構成する方法についても説明しています。

このガイドは次のセクションで構成されます。

- [DNS ポリシーの概要](DNS-Policies-Overview.md)
- [プライマリ サーバーでの地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する](primary-geo-location.md)
- [プライマリ-セカンダリの展開での地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する](primary-secondary-geo-location.md)
- [1 日の時間に基づくインテリジェントなDNS 応答に DNS ポリシーを使用する](dns-tod-intelligent.md)
- [Azure Cloud App Server を使用した時間帯に基づく DNS 応答](dns-tod-azure-cloud-app-server.md)
- [スプリットブレイン DNS 展開に DNS ポリシーを使用する](split-brain-DNS-deployment.md)
- [Active Directory でのスプリットブレイン DNS に DNS ポリシーを使用する](dns-sb-with-ad.md)
- [Dns クエリにフィルターを適用するために DNS ポリシーを使用する](apply-filters-on-dns-queries.md)
- [アプリケーションの負荷分散に DNS ポリシーを使用する](app-lb.md)
- [地理的な場所を認識するアプリケーションの負荷分散に DNS ポリシーを使用する](app-lb-geo.md)

