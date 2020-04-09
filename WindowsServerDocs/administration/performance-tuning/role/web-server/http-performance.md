---
title: HTTP 1.1/2 のパフォーマンスチューニング
description: HTTP 1.1/2 のパフォーマンスチューニングに関する推奨事項
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: ivanpash; gmonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5e62f7428f015193896aba5c7d9c146bd11e7225
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851685"
---
# <a name="performance-tuning-http-112"></a>HTTP 1.1/2 のパフォーマンスチューニング

HTTP/2 は、クライアント側のパフォーマンスを向上させることを目的としています (ブラウザーでのページ読み込み時間など)。 サーバーでは、CPU コストがわずかに増加している可能性があります。 サーバーは、すべての要求に対して1つの TCP 接続を必要としなくなったのに対して、その状態の一部が HTTP レイヤーに保持されるようになりました。 さらに、HTTP/2 には、追加の CPU 負荷を表すヘッダー圧縮があります。

場合によっては、http/1.1 フォールバックが必要になります (HTTP/2 接続をリセットし、代わりに HTTP/1.1 を使用する新しい接続を確立します)。 特に、TLS の再ネゴシエーションと HTTP 認証 (基本およびダイジェストを除く) には、HTTP/1.1 フォールバックが必要です。 これによってオーバーヘッドが増加しますが、これらの操作は既に遅延を意味するため、特にパフォーマンスを重視することはありません。

## <a name="see-also"></a>参照
- [Web サーバーのパフォーマンスチューニング](index.md) 
- [IIS 10.0 のパフォーマンス チューニング](tuning-iis-10.md)