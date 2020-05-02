---
title: bitsadmin gettype
description: 指定されたジョブのジョブの種類を取得する bitsadmin gettype コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 151f9b8e81229a666111ebcd20f060d84160445a
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717476"
---
# <a name="bitsadmin-gettype"></a>bitsadmin gettype

指定されたジョブの種類を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /gettype <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
