---
title: キャッシュおよびメモリ マネージャー サブシステムのパフォーマンス チューニング
description: キャッシュおよびメモリ マネージャー サブシステムのパフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bbbd8ad17bfb735b148b7f9a53628ab4445f07c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891433"
---
# <a name="performance-tuning-cache-and-memory-manager"></a>キャッシュおよびメモリ マネージャーのパフォーマンス チューニング

Windows の既定では、ディスクから読み取られるファイル データとディスクに書き込まれるファイル データはキャッシュされます。 つまり、読み取り操作では、物理ディスクからではなく、システム ファイル キャッシュと呼ばれるシステム メモリ内の領域からファイル データが読み取られます。 同様に、書き込み操作では、ディスクではなくシステム ファイル キャッシュにファイル データが書き込まれます。この種類のキャッシュはライトバック キャッシュと呼ばれます。 キャッシュはファイル オブジェクトごとに管理されます。 キャッシュは、Windows の実行中に継続的に動作するキャッシュ マネージャーの指示に従って実行されます。

システム ファイル キャッシュ内のファイル データは、オペレーティング システムによって決定された間隔でディスクに書き込まれます。 フラッシュされたページは、システム キャッシュ ワーキング セット (FILE\_FLAG\_RANDOM\_ACCESS が設定され、ファイル ハンドルが閉じられていない場合) または使用可能なメモリの一部となる待機リストに残ります。

ファイルへのデータの書き込みを遅延し、キャッシュがフラッシュされるまでキャッシュに保持するポリシーは遅延書き込みと呼ばれ、指定された時間間隔でキャッシュ マネージャーからトリガーされます。 ファイル データのブロックがフラッシュされる時間は、部分的には、キャッシュに格納されていた時間と、データが読み取り操作で最後にアクセスされてからの時間に基づいて決まります。 これにより、頻繁に読み取られるファイル データが、システム ファイル キャッシュ内で可能な限り長くアクセス可能な状態が維持されます。

このファイル データ キャッシュ プロセスを次の図に示します。

![ファイル データのキャッシュ](../../media/perftune-guide-file-data-caching.png)

上の図の実線の矢印で示されているように、ファイルの読み取り操作中にキャッシュ マネージャーによって最初に要求されたときに、256 KB のデータ領域がシステム アドレス空間内の 256 KB のキャッシュ スロットに読み取られます。 次に、ユーザーモード プロセスによって、このスロット内のデータがそのアドレス空間にコピーされます。 プロセスでデータ アクセスが完了すると、プロセスのアドレス空間とシステム キャッシュ間の点線の矢印で示されているように、変更されたデータはシステム キャッシュの同じスロットに書き戻されます。 キャッシュ マネージャーは、一定期間、データが不要になると判断すると、システム キャッシュとディスク間の点線の矢印で示されているように、変更されたデータはディスク上のファイルに書き戻されます。

**このセクションの内容:**

-   [キャッシュおよびメモリ マネージャーの潜在的なパフォーマンスの問題](troubleshoot.md)

-   [Windows Server 2016 でのキャッシュおよびメモリ マネージャーの機能強化](improvements-in-2016.md)
