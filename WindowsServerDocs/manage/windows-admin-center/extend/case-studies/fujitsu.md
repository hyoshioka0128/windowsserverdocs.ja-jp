---
title: 管理センターの Windows SDK のケース スタディ - 富士通
description: 管理センターの Windows SDK のケース スタディ - 富士通
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2052376"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>富士通 ServerView の正常性と RAID の拡張

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>状態のエンドツー エンドの把握、ハードウェア、オペレーティング システムから Windows 管理センター

トップ日本語の情報と通信テクノロジー企業[PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/)と[PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/)サーバー製品の製造元、富士通します。 [富士通 ServerView 管理スイート](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/)は、ライフ サイクル管理のハードウェア管理 CIM と PowerShell インターフェイスを提供するサーバー側エージェントを含む、サーバーの包括的なツールセットを提供します。

富士通は、サーバー側エージェントと通信する CIM と PowerShell のインターフェイスを提供して、Windows の管理センターを容易に統合するには、営業案件を学習します。 利用可能な UI コンポーネントを使用して Windows 管理センター内の情報を可視化を簡単にエージェントに慣れていた CIM 呼び出しを実装および富士通の開発チームができました。

![富士通拡張子の正常性のツリー ビュー](../../media/extend-case-study-fujitsu/health-tree.png)

チームが管理センター Windows SDK のようになりました、追加のハードウェア情報を公開する UI を追加するだけでいくつかの HTML コード行ことがよくをすばやく、ハードウェア コンポーネントの概要ビューを表示するように、1 つのツールから展開することができましたドライバーのモニターをシステムのイベント ログの詳細ビューの正常性のプロセッサ、メモリ、ファン、電源、温度、電圧、ビューと RAID 管理用の別のツールもで区切ります。 グリッドと詳細ウィンドウのコントロールに SDK ツリーなどの利用可能な UI コントロールを使用して、ユーザー インターフェイスを簡単に作成すると、Windows 管理センターの残りの部分によく似てと相互作用デザインをチームが有効になります。

![富士通拡張子 - RAID ツリー ビュー](../../media/extend-case-study-fujitsu/raid-tree.png)

![富士通拡張子 - RAID ボリュームを表示します。](../../media/extend-case-study-fujitsu/raid-volumes.png)

富士通と Windows 管理センターのチームのパートナーシップ明確に内に表示する値との統合の Windows 管理センターでは、お客様のエンドツー エンド洞察はサーバーの役割およびサービス、オペレーティング システム、ハードウェアの管理を有効にします。.