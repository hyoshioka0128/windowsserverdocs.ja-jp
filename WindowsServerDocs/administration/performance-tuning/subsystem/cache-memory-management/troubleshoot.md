---
title: キャッシュとメモリマネージャーのパフォーマンスの問題のトラブルシューティング
description: Windows Server 16 でのキャッシュとメモリマネージャーのパフォーマンスに関する問題のトラブルシューティング
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: pavel; atales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0b01808564cfaf1eaedf30a66c774e2228205847
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851655"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>キャッシュとメモリマネージャーのパフォーマンスの問題のトラブルシューティング

Windows Server 2012 より前では、特定のワークロードで使用可能なメモリがほとんど使い果たされないように、システムファイルキャッシュが大きくなるという2つの主な問題が発生しました。 この状況によってシステムの処理が遅くなる場合は、サーバーがこれらの問題のいずれかに直面しているかどうかを判断できます。


## <a name="counters-to-monitor"></a>監視するカウンター

-   メモリ\\長期間のスタンバイキャッシュの有効期間 &lt; 1800 秒

-   メモリ\\使用可能なメガバイト数が不足しています

-   メモリ\\システムキャッシュ常駐バイト数

メモリ\\使用可能なメガバイト数が少なく、同時にメモリ\\システムキャッシュ常駐バイトが物理メモリの重要な部分を占めている場合は、 [Rammap](https://technet.microsoft.com/sysinternals/ff700229.aspx)を使用して、キャッシュがどのように使用されているかを調べることができます。

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>システムファイルキャッシュに NTFS メタファイルデータ構造が含まれている


この問題は、次の図に示すように、RAMMAP の出力に含まれるアクティブなメタファイルの数が非常に多い場合に示されます。 この問題は、大量のファイルがアクセスされているビジー状態のサーバーで発生している可能性があります。これにより、NTFS メタファイルデータがキャッシュから解放されません。

![rammap ビュー](../../media/perftune-guide-rammap.png)

*DynCache*ツールによって軽減される問題。 Windows Server 2012 以降では、アーキテクチャが再設計され、この問題は存在しなくなりました。

## <a name="system-file-cache-contains-memory-mapped-files"></a>システムファイルキャッシュにメモリマップファイルが含まれています


この問題は、RAMMAP の出力で、非常に多くのアクティブなマップ済みファイルページによって示されています。 これは通常、サーバー上の一部のアプリケーションが、ファイル\_フラグ\_ランダム\_アクセスフラグが設定された[CreateFile](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx) API を使用して多数の大きなファイルを開こうとしていることを示します。

この問題の詳細については、サポート技術情報の記事[2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369)で説明されています。 ファイル\_フラグ\_ランダム\_アクセスフラグは、キャッシュマネージャーがファイルのマップされたビューを可能な限り長くメモリに保持するためのヒントです (メモリマネージャーがメモリ不足の状態を通知しないようにするため)。 同時に、このフラグは、ファイルデータのプリフェッチを無効にするようにキャッシュマネージャーに指示します。

この状況は、Windows Server 2012 以降で設定のトリミングの機能強化によって、ある程度軽減されていますが、この問題自体は、ファイル\_フラグ\_ランダム\_アクセスを使用せずに、アプリケーションベンダーによって主に対処する必要があります。 アプリケーションベンダー向けの代替ソリューションとして、ファイルへのアクセス時に低メモリ優先度を使用することもできます。 これは、 [Setthreadinformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) API を使用して実現できます。 低いメモリ優先度でアクセスされるページは、作業セットから積極的に削除されます。

キャッシュマネージャーは、Windows Server 2016 以降では、トリミングに関する決定を行うときに FILE_FLAG_RANDOM_ACCESS を無視することで、これをさらに軽減します。そのため、FILE_FLAG_RANDOM_ACCESS フラグを指定せずに開いた他のファイルと同様に処理されます (キャッシュマネージャーでは、ファイルデータのプリフェッチを無効にするために、このフラグは引き続き このフラグを使用して多数のファイルを開いて、真のランダムな方法でアクセスした場合は、システムキャッシュが肥大化する可能性があります。 FILE_FLAG_RANDOM_ACCESS アプリケーションでは使用しないことを強くお勧めします。
