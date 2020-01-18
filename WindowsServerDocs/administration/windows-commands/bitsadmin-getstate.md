---
title: bitsadmin getstate
description: Bitsadmin getstate の Windows コマンドに関するトピック
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
ms.openlocfilehash: 2cff790c8787b1514e8523a4583184d6f6a59efc
ms.sourcegitcommit: 51e0b575ef43cd16b2dab2db31c1d416e66eebe8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/17/2020
ms.locfileid: "76259107"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate


指定されたジョブの状態を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /GetState <Job>
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
|    Job    | ジョブの表示名または GUID |

## <a name="remarks"></a>注釈

可能性のある状態は次のとおりです。

|      State (状態)      | 説明 |
| --------------- | ----------- |
| QUEUED          | ジョブは実行を待機しています。 |
| 接続中      | BITS はサーバーに接続しています。 |
| 異動    | BITS はデータを転送しています。 |
| 支払     | BITS によってジョブ内のすべてのファイルが正常に転送されました。 |
| SUSPENDED       | ジョブが一時停止されています。 |
| エラー           | 回復不可能なエラーが発生しました。転送は再試行されません。 |
| TRANSIENT_ERROR | 回復可能なエラーが発生しました。最小再試行間隔が経過すると、転送が再試行されます。 |
| 確認済み    | ジョブが完了しました。 |
| [CANCELED] (キャンセル済み)        | ジョブは取り消されました。 |

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態を取得します。

```
C:\>bitsadmin /GetState myDownloadJob
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
