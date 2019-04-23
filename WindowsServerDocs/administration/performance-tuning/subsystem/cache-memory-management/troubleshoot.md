---
title: キャッシュとメモリ マネージャーのパフォーマンスの問題をトラブルシューティングします。
description: キャッシュと Windows Server 16 の Memory Manager のパフォーマンスの問題をトラブルシューティングします。
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 66c7e2a6b264a837c65df927b271fadd2672fa24
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835793"
---
# <a name="troubleshoot-cache-and-memory-manager-performance-issues"></a>キャッシュとメモリ マネージャーのパフォーマンスの問題をトラブルシューティングします。

Windows Server 2012 では、前に、2 つのプライマリの潜在的な問題は、特定のワークロードで使用可能なメモリが残りわずかになるまで拡張するシステム ファイル キャッシュを発生します。 ときにこのような状況には、システムが動作の遅いでの結果が、サーバーがこれらの問題のいずれかの接続がかどうかを判断できます。


## <a name="counters-to-monitor"></a>監視するためのカウンター

-   メモリ\\長期的な平均スタンバイ キャッシュの有効期間 (秒) &lt; 1800 秒

-   メモリ\\Mbytes が不足

-   メモリ\\システム キャッシュの常駐バイト数

場合メモリ\\Available Mbytes は低いメモリと同時に\\System Cache Resident Bytes、物理メモリのかなりの部分を消費している、使用することができます[RAMMAP](https://technet.microsoft.com/sysinternals/ff700229.aspx)どのようなキャッシュが使用されていることを確認するには。

## <a name="system-file-cache-contains-ntfs-metafile-data-structures"></a>システム ファイル キャッシュには、NTFS メタファイル データ構造が含まれています。


この問題に次の図に示すように、非常に高いアクティブ メタファイル内のページ数 RAMMAP、出力が表示されます。 この問題がありますが確認されています高いサーバーでは数百万件のファイルがアクセスされているため、キャッシュから解放されない NTFS メタファイルのデータをキャッシュに結果として得られる。

![rammap ビュー](../../media/perftune-guide-rammap.png)

この問題を軽減するために使用*DynCache*ツール。 Windows Server 2012 以降でアーキテクチャが再設計され、この問題が存在しない必要があります。

## <a name="system-file-cache-contains-memory-mapped-files"></a>システム ファイル キャッシュには、メモリ マップ ファイルが含まれています。


この問題は、非常に高いアクティブなマップ済みファイル内のページ数 RAMMAP 出力が表示されます。 通常は示しますサーバー上のいくつかのアプリケーションが多数を使用して大規模なファイルを開いています[CreateFile](https://msdn.microsoft.com/library/windows/desktop/aa363858.aspx)ファイルを使用した API\_フラグ\_ランダム\_アクセス フラグを設定します。

この問題は、サポート技術情報の記事で詳しく説明[2549369](https://support.microsoft.com/default.aspx?scid=kb;en-US;2549369)します。 ファイル\_フラグ\_ランダム\_アクセス フラグ (メモリ マネージャーは、メモリ不足の状態を通知しません) までは、ファイルのマップ ビューをできるだけ長くメモリに保持するキャッシュ マネージャーのヒントとなります。 同時に、このフラグはキャッシュ マネージャーはファイル データのプリフェッチを無効にするように指示します。

このような状況がセットのトリミング機能強化の操作で Windows Server 2012 以降で、ある程度軽減されたが、それ自体問題がないファイルを使用して、アプリケーション ベンダーによって主に対処する必要が\_フラグ\_ランダム\_アクセスします。 ファイルにアクセスするときに、低いメモリの優先順位を使用するアプリのベンダーの代替ソリューションがあります。 これを使用して実現することができます、 [SetThreadInformation](https://msdn.microsoft.com/library/windows/desktop/hh448390.aspx) API。 メモリ不足の優先順位でアクセスされるページは、ワーキング セットをより積極的にから削除されます。

(キャッシュ マネージャーも、この FILE_FLAG_RANDOM_ACCESS フラグなしで開かれるその他のファイルと同じように扱われますので、トリミング意思決定を行うときに、FILE_FLAG_RANDOM_ACCESS を無視することによってこれを以降 Windows Server 2016 ではさらに軽減キャッシュ マネージャーフラグをファイル データのプリフェッチを無効にする)。 多数のファイルのこのフラグで開かれ、本当にランダムにアクセスした場合でもシステム キャッシュの肥大化が発生することができます。 FILE_FLAG_RANDOM_ACCESS をアプリケーションで使用しないことを強くお勧めします。
