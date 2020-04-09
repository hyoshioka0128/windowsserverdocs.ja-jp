---
title: bitsadmin gettype
description: '**Bitsadmin gettype**の Windows コマンドに関するトピックでは、指定されたジョブのジョブの種類を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bec16f04-3e95-4587-889e-3de6ad03c9c8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 66a1fc5b0478e1eec26557dc9a7f76d50abcb8b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850445"
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
| 送信 | ジョブの表示名または GUID。 |

## <a name="output"></a>出力

出力値は次のとおりです。

| 種類 | 説明 |
| --------------- | ----------- |
| ダウンロード | このジョブはダウンロードです。 |
| アップロード | ジョブはアップロードです。 |
| アップロード-応答 | ジョブは、アップロード応答です。 |
| 不明 | ジョブの種類が不明です。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブのジョブの種類を取得します。

```
C:\>bitsadmin /gettype myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)