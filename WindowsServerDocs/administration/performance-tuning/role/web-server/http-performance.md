---
title: HTTP 1.1/2 のパフォーマンス チューニング
description: パフォーマンスに関する推奨事項の HTTP 1.1/2
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: IvanPash; GMonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bf85efa88e377966135c23a548119f19c39cceba
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866373"
---
# <a name="performance-tuning-http-112"></a>パフォーマンス チューニングの HTTP 1.1/2

Http/2 は、(たとえば、ページの読み込み時間、ブラウザーで) クライアント側でのパフォーマンスが向上します。 サーバーで、CPU コストで若干の増加を表すこと可能性があります。 不要になったサーバーが要求ごとに 1 つの TCP 接続を必要とはいくつかの状態のようになりましたに保持される HTTP レイヤー。 さらに、http/2 は、ヘッダーの圧縮は、追加の CPU 負荷を表します。

状況によっては、http/1.1 (http/2 接続をリセットして、http/1.1 を使用する新しい接続を確立する代わりに) フォールバックが必要です。 具体的には、TLS の再ネゴシエーションと HTTP 認証 (Basic とダイジェスト認証) 以外には、http/1.1 にフォールバックが必要です。 このオーバーヘッドもこれらの操作は既にいくつかの遅延を意味し、ようにするは特にパフォーマンスが区別されません。

## <a name="see-also"></a>関連項目
- [Web Server のパフォーマンス チューニング](index.md) 
- [IIS 10.0 パフォーマンス チューニング](tuning-iis-10.md)