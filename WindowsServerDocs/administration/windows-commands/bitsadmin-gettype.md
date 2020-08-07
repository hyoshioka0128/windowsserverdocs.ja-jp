---
title: bitsadmin gettype
description: Bitsadmin gettype コマンドの参照記事。指定されたジョブのジョブの種類を取得します。
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f0fe66256e59526b874aaf2ec8ae0193846a1da
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893825"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

指定されたジョブの種類を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

#### <a name="output"></a>出力

返される出力値は次のようになります。

| Type | 説明 |
| --------------- | ----------- |
| ダウンロード | このジョブはダウンロードです。 |
| アップロード | ジョブはアップロードです。 |
| アップロード-応答 | ジョブは、アップロード応答です。 |
| Unknown | ジョブの種類が不明です。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのジョブの種類を取得するには、次のようにします。

```
bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
