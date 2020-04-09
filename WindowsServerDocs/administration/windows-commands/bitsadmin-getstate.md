---
title: bitsadmin getstate
description: '**Bitsadmin getstate**の Windows コマンドに関するトピックでは、指定されたジョブの状態を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1252d6cf-14ca-44df-beb2-930ff011f297
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 43cd8c8e614cce65f55b16fc5395b1d37de0cf95
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850465"
---
# <a name="bitsadmin-getstate"></a>bitsadmin getstate

指定されたジョブの状態を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getstate <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="output"></a>出力

出力値は次のとおりです。

| 状態 | 説明 |
| --------------- | ----------- |
| キューに登録済み | ジョブは実行を待機しています。 |
| 接続中 | BITS はサーバーに接続しています。 |
| 異動 | BITS はデータを転送しています。 |
| 支払 | BITS によってジョブ内のすべてのファイルが正常に転送されました。 |
| Suspended | ジョブが一時停止されています。 |
| エラー | 回復不可能なエラーが発生しました。転送は再試行されません。 |
| Transient_Error | 回復可能なエラーが発生しました。最小再試行間隔が経過すると、転送が再試行されます。 |
| 確認 | ジョブが完了しました。 |
| Canceled | ジョブは取り消されました。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの状態を取得します。

```
C:\>bitsadmin /getstate myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
