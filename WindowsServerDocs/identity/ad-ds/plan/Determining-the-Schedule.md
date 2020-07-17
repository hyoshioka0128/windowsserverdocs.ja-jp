---
ms.assetid: 28ecaf5c-9131-406c-b211-a230162e462e
title: スケジュールを決定する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d5c1c7c77304317bab2e80223dd745c88bc79efd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822545"
---
# <a name="determining-the-schedule"></a>スケジュールを決定する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

サイトリンクのスケジュールを設定することによって、サイトリンクの可用性を制御できます。 2つのサイト間のレプリケーションが複数のサイトリンクを通過する場合、関連するすべてのリンクのレプリケーションスケジュールの共通部分によって、2つのサイト間の接続スケジュールが決まります。  
  
サイトリンクスケジュールの設定を計画するには、互いに直接レプリケートされるドメインコントローラーを含むサイトリンク間で、2つの重複したスケジュールを作成します。 ピーク時間中にレプリケーショントラフィックをブロックする場合を除き、これらのリンクに対して既定 (100-%) のスケジュールを使用します。 レプリケーションをブロックすると、他のトラフィックに優先順位が与えられますが、レプリケーションの潜在期間も長くなります。  
  
ドメインコントローラーは、世界協定時刻 (UTC) で時刻を格納します。 サイトリンクオブジェクトのスケジュールの時刻設定は、スケジュールが設定されているサイトとコンピューターのローカル時刻に準拠しています。 ドメインコントローラーが、別のサイトおよびタイムゾーンにあるコンピューターに接続すると、そのコンピューターのサイトのローカル時刻に従って、ドメインコントローラーのスケジュールに時刻の設定が表示されます。  
  


