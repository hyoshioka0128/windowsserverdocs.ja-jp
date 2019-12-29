---
title: Windows 管理センター SDK ケーススタディ-富士通
description: Windows 管理センター SDK ケーススタディ-富士通
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9acfa873e4ce7d3e91a23abff726836f0e11ce59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357221"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>富士通の ServerView のヘルスと RAID 拡張

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>オペレーティングシステムからハードウェアまで、Windows 管理センターにエンドツーエンドの可視性をもたらす

富士通は、 [PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/)および[PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/) server 製品の主要な日本情報とコミュニケーションテクノロジを提供している企業です。 [富士通 ServerView 管理スイート](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/)は、ハードウェア管理用の CIM と PowerShell インターフェイスを提供するサーバー側エージェントなど、サーバーのライフサイクル管理のための包括的なツールセットを提供します。

富士通は、サーバー側のエージェントと通信できる CIM と PowerShell インターフェイスを提供することで、Windows 管理センターと簡単に統合できるようになりました。 富士通の開発チームは、使い慣れた CIM 呼び出しをエージェントに簡単に実装し、使用可能な UI コンポーネントを使用して Windows 管理センター内で情報を視覚化することができました。

![富士通拡張-正常性ツリービュー](../../media/extend-case-study-fujitsu/health-tree.png)

チームが Windows 管理センター SDK について理解したら、追加のハードウェア情報を公開するための UI を追加するだけでは、多くの場合、単に数行の HTML コードが表示され、1つのツールから簡単に拡張してハードウェアコンポーネントの概要ビューを表示できました。システムイベントログのヘルス、詳細な表示、ドライバーモニター、プロセッサ、メモリ、ファン、電源、気温、電圧の個別のビュー、および RAID 管理用の追加ツール。 ツリー、グリッド、詳細ペインなどの SDK で使用できる UI コントロールを使用すると、チームは UI をすばやく構築でき、さらに Windows 管理センターの他の部分と非常によく似たビジュアルと対話のデザインも実現できます。

![富士通拡張-RAID ツリービュー](../../media/extend-case-study-fujitsu/raid-tree.png)

![富士通拡張-RAID ボリュームビュー](../../media/extend-case-study-fujitsu/raid-volumes.png)

富士通と Windows 管理センターチームのパートナーシップは、Windows 管理センター内の統合の価値を明確に示しています。これにより、お客様は、サーバーの役割とサービス、オペレーティングシステム、およびハードウェア管理について、エンドツーエンドの洞察を得ることができるようになります.