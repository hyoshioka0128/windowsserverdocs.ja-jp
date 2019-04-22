---
title: Windows Admin Center SDK のケース スタディ - Fujitsu
description: Windows Admin Center SDK のケース スタディ - Fujitsu
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 6d916920b187dd3c637644a0f40ae9f9cca72b66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814993"
---
# <a name="fujitsu-serverview-health-and-raid-extensions"></a>Fujitsu ServerView の正常性と RAID の拡張機能

## <a name="bringing-end-to-end-visibility-from-operating-system-to-hardware-into-windows-admin-center"></a>ハードウェア、オペレーティング システムから Windows Admin Center にエンド ツー エンドの可視性を取り込む

Fujitsu は先頭日本情報との通信テクノロジ企業との製造元[PRIMERGY](http://www.fujitsu.com/fts/products/computing/servers/primergy/)と[PRIMEQUEST](http://www.fujitsu.com/fts/products/computing/servers/mission-critical/)サーバー製品です。 [Fujitsu ServerView 管理スイート](http://www.fujitsu.com/fts/products/computing/servers/primergy/management/)サーバー ハードウェア管理のために CIM および PowerShell インターフェイスを提供するサーバー側のエージェントを含むライフ サイクル管理の包括的なツールセットを提供します。

Fujitsu は、サーバー側のエージェントと通信する CIM および PowerShell のインターフェイスが提供されるように、Windows Admin Center と簡単に統合する機会を説明しました。 Fujitsu の開発チームは、簡単に、エージェントに慣れていた CIM 呼び出しを実装し、使用可能な UI コンポーネントを使用して、Windows Admin Center 内の情報を視覚化することでした。

![Fujitsu 拡張機能 - 正常性のツリー ビュー](../../media/extend-case-study-fujitsu/health-tree.png)

チームが、Windows Admin Center SDK を使い慣れてなって以来、多くの場合、単に、いくつかの HTML コードの行には追加のハードウェア情報を公開する UI を追加してすぐに、ハードウェア コンポーネントの概要ビューを表示するときに 1 つのツールから展開することができました正常性、システム イベント ログには、ドライバーのモニターの詳細なビューでは、プロセッサ、メモリ、ファン、電源、温度、電圧のビューと RAID 管理のための別のツールでもを分離します。 グリッドと詳細ウィンドウのコントロールをツリーなどの SDK で使用できる UI コントロールを使用して、迅速な UI を作成して、Windows Admin Center の残りの部分によく似ています、ビジュアルと対話設計を実現するチームが有効になります。

![Fujitsu 拡張機能 - RAID ツリー ビュー](../../media/extend-case-study-fujitsu/raid-tree.png)

![Fujitsu 拡張機能 - RAID ボリュームを表示します。](../../media/extend-case-study-fujitsu/raid-volumes.png)

Fujitsu と、Windows Admin Center チームの間のパートナーシップ明確に値が表示されます統合の内、Windows Admin Center では、お客様はサーバーの役割とサービスをオペレーティング システムおよびハードウェアの管理に洞察のエンド ツー エンドの有効化.