---
title: HTTP 1.1/2 のパフォーマンスチューニング
description: HTTP 1.1/2 のパフォーマンスチューニングに関する推奨事項
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: ivanpash; gmonte
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: a0a4464d7a13911ec9cc7d104b6fe9292a64586e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471247"
---
# <a name="performance-tuning-http-112"></a>HTTP 1.1/2 のパフォーマンスチューニング

HTTP/2 は、クライアント側のパフォーマンスを向上させることを目的としています (ブラウザーでのページ読み込み時間など)。 サーバーでは、CPU コストがわずかに増加している可能性があります。 サーバーは、すべての要求に対して1つの TCP 接続を必要としなくなったのに対して、その状態の一部が HTTP レイヤーに保持されるようになりました。 さらに、HTTP/2 には、追加の CPU 負荷を表すヘッダー圧縮があります。

場合によっては、http/1.1 フォールバックが必要になります (HTTP/2 接続をリセットし、代わりに HTTP/1.1 を使用する新しい接続を確立します)。 特に、TLS の再ネゴシエーションと HTTP 認証 (基本およびダイジェストを除く) には、HTTP/1.1 フォールバックが必要です。 これによってオーバーヘッドが増加しますが、これらの操作は既に遅延を意味するため、特にパフォーマンスを重視することはありません。

## <a name="additional-references"></a>その他のリファレンス
- [Web サーバーのパフォーマンスチューニング](index.md)
- [IIS 10.0 のパフォーマンス チューニング](tuning-iis-10.md)