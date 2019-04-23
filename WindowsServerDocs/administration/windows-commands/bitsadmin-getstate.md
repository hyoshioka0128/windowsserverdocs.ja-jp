---
title: bitsadmin getstate
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7ed7529fda264efaceb6b4b36e36e728c211f3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889623"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate



指定したジョブの状態を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

可能な状態は次のとおりです。

|-----|-----| |キューに置かれた |ジョブが実行を待機している |。|接続する |BITS は、サーバーへの接続します |。|転送する |BITS がデータを転送する |。|中断 |ジョブが一時停止しています |。|エラー |回復可能なエラーが発生しました。転送は再試行されません |。|TRANSIENT_ERROR |回復可能なエラーが発生しました。最小再試行間隔が経過すると、転送の再試行します |。|受信確認 |ジョブが完了した |。|取り消されました |ジョブが取り消されました |。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの状態を取得する*myDownloadJob*します。
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)