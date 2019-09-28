---
title: bitsadmin getstate
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 55be37a6b1b44b81ed9002e5e3b9eb1fd46bd0dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381234"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate



指定されたジョブの状態を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

考えられる状態は次のとおりです。

|-----|-----| |QUEUED |ジョブは実行を待機しています |。|接続 |BITS はサーバーに接続しています |。|転送中 |BITS はデータを転送しています |。|中断 |ジョブが一時停止されています |。|ERROR |回復不可能なエラーが発生しました。転送は再試行されません |。|TRANSIENT_ERROR |回復可能なエラーが発生しました。最小再試行間隔が経過すると、転送が再試行されます |。|認知済み |ジョブは完了しました |。|CANCELED |ジョブは取り消されました |。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態を取得します。
```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)