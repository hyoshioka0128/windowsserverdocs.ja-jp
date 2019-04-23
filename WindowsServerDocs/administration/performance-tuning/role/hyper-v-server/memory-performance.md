---
title: Hyper V のメモリのパフォーマンス
description: パフォーマンス チューニング、HYPER-V でメモリに関する考慮事項
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 63a1b654b8ac52725cc5dd87c8b245f9dfaf40f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848073"
---
# <a name="hyper-v-memory-performance"></a>Hyper V のメモリのパフォーマンス


ハイパーバイザーでは、非仮想化システムとしてだけでゲスト物理メモリを仮想マシンを互いに分離して、各ゲスト オペレーティング システムの連続した、0 から始まるメモリ領域を提供する仮想化します。

## <a name="correct-memory-sizing-for-child-partitions"></a>子パーティションの適切なメモリのサイズを変更します。

物理コンピューター上のサーバー アプリケーションに対する通常の方法は、仮想マシンのメモリを調整する必要があります。 これが通常に予想される負荷を無理なく処理サイズを変更する必要がある時とピークのため、メモリ不足は、応答時間と CPU または I/O 使用率に大幅に向上させることができます。

Windows 仮想マシンのメモリを動的にサイズを許可する動的メモリを有効にすることができます。 動的メモリは、仮想マシンでのアプリケーション、突然大量のメモリの割り当てを行う際の問題が発生する場合、メモリの負荷に動的メモリが応答ときに、一時的なバックアップを確保する仮想マシンのページファイルのサイズを増やすことができます。

動的メモリの詳細については、次を参照してください。 [Hyper-v 動的メモリの概要]( https://go.microsoft.com/fwlink/?linkid=834434)と[Hyper-v 動的メモリ構成ガイド](https://go.microsoft.com/fwlink/?linkid=834435)します。

子パーティションで Windows を実行するときに、子パーティションはメモリ不足が発生しているより大きな仮想マシンのメモリ サイズとパフォーマンスが向上する可能性があるかどうかを識別するために、子パーティション内の次のパフォーマンス カウンターを使用できます。

| パフォーマンス カウンター                                                         | 推奨されるしきい値                                                                                                                                                           |
|-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| メモリ-スタンバイ キャッシュ予約のバイト数                                        | スタンバイ キャッシュ予約のバイト数と空き、およびゼロ ページ リストのバイトの合計には、2 GB 以上の表示の RAM を備えたシステムで 1 GB、および 300 MB 以上のシステムで 200 MB 以上を指定する必要があります。 |
| メモリ-空き領域 & ゼロ ページ リストのバイト数                                        | スタンバイ キャッシュ予約のバイト数と空き、およびゼロ ページ リストのバイトの合計には、2 GB 以上の表示の RAM を備えたシステムで 1 GB、および 300 MB 以上のシステムで 200 MB 以上を指定する必要があります。 |
| メモリ-1 秒あたりの入力ページ                                                    | 1 時間以上にわたって平均は、10 未満です。                                                                                                                                       | 

## <a name="correct-memory-sizing-for-root-partition"></a>ルート パーティションの適切なメモリのサイズを変更します。

ルート パーティションには、I/O 仮想化、仮想マシンのスナップショット、および子パーティションをサポートするために管理などのサービスを提供するための十分なメモリが必要です。

Windows Server 2016 で HYPER-V では、ルート パーティションの高パフォーマンスと信頼性を確保しながら、子パーティションにどのくらいのメモリが割り当て安全に可能を決定する、ルート パーティションの管理オペレーティング システムのランタイム ヘルスを監視します。

## <a name="see-also"></a>関連項目

-   [HYPER-V 用語](terminology.md)

-   [HYPER-V のアーキテクチャ](architecture.md)

-   [HYPER-V サーバーの構成](configuration.md)

-   [HYPER-V のプロセッサのパフォーマンス](processor-performance.md)

-   [HYPER-V ストレージの I/O パフォーマンス](storage-io-performance.md)

-   [HYPER-V ネットワークの I/O パフォーマンス](network-io-performance.md)

-   [仮想化環境のボトルネックの検出](detecting-virtualized-environment-bottlenecks.md)

-   [Linux 仮想マシン](linux-virtual-machine-considerations.md)
