---
title: キャッシュとメモリ マネージャーの機能強化
description: キャッシュと Windows Server 2016 でのメモリ マネージャーの機能強化
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Pavel; ATales
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: bd15cfc0714d1992e6b15d716b6b96ce259786da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868583"
---
# <a name="cache-and-memory-manager-improvements"></a>キャッシュとメモリ マネージャーの機能強化

このトピックでは、Windows Server 2012 および 2016 でのキャッシュ マネージャーおよびメモリ マネージャーの機能強化について説明します。

## <a name="cache-manager-improvements-in-windows-server-2016"></a>Windows Server 2016 でのキャッシュ マネージャーの機能強化
キャッシュ マネージャーは、true 非同期キャッシュ読み取りのサポートも追加されます。
キャッシュされた非同期の読み取りに大きく依存している場合は、可能性のあるアプリケーションのパフォーマンスを向上これでした。  ボックス内のファイル システムのほとんどは、しばらくの間、非同期キャッシュの読み取りをサポートされていますが、スレッド プールとファイル システムの内部作業キューの処理に関連するさまざまな設計上の選択のためのパフォーマンスの制限が多くの場合があります。  カーネル適切なサポートにより、キャッシュ マネージャーには、すべてのスレッドのプールが表示されなくなりましたしように処理することでより効率的な非同期のファイル システムからの作業キュー管理の複雑さが読み取りをキャッシュします。キャッシュ マネージャーは (システムでサポートされる最大値) の各コントロールのデータ構造の 1 つのセットを並列処理を最大化する VHD 入れ子レベル。


## <a name="cache-manager-improvements-in-windows-server-2012"></a>Windows Server 2012 でのキャッシュ マネージャーの機能強化
キャッシュ マネージャーの機能強化は、連続したワークロードの場合は、新しい API の先読みのロジックに加えて[CcSetReadAheadGranularityEx](https://msdn.microsoft.com/library/windows/hardware/hh406341.aspx)ファイル システム ドライバー、SMB など、その読み取り先行パラメーターを変更できるように追加されました。 複数の小規模の先読みを 1 つの大きな読み取り先行の要求を送信する代わりに要求を送信することによってリモート ファイルのシナリオのスループットを向上できます。 ファイル システムのドライバーなどのカーネル コンポーネントのみでは、ファイルごとにプログラムによってこれらの値を設定できます。

## <a name="memory-manager-improvements-in-windows-server-2012"></a>Windows Server 2012 でのメモリ マネージャーの機能強化
ページの結合を有効にすると、同じコンテンツを持つプライベートなページング可能なページの多いサーバーのメモリ使用量を減らすことができます。 たとえば、同じメモリを消費するアプリ、または反復性の高いデータで動作する 1 つのアプリの複数のインスタンスを実行しているサーバーには、ページを組み合わせることをお試しくださいする適切な候補があります。 ページの結合の有効化の短所は、CPU 使用率の向上です。

ここでページを組み合わせることがメリットを提供する可能性の高いサーバーの役割の例を示します。

-   ファイル サーバーが (メモリの大部分はプライベートであり、したがってしない組み合わせ可能ではないファイル ページによって消費される)

-   AWE または大きなページ (メモリの大部分はプライベートであるが、非ページング) を使用して構成されている Microsoft SQL サーバー

ページを組み合わせることが既定で無効になっているを使用して有効にすることができますが、[有効にする MMAgent](https://technet.microsoft.com/library/jj658954.aspx) Windows PowerShell コマンドレット。 ページを組み合わせることは、Windows Server 2012 で追加されました。
