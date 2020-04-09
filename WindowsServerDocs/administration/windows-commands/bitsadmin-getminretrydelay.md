---
title: bitsadmin getminretrydelay
description: '**Bitsadmin getminretrydelay**の Windows コマンドに関するトピックでは、ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 54f0abab-c129-40ed-a603-50f464d26011
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d79ffdf1f45b0198b4af535ed83154c3c2ec24f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850625"
---
# <a name="bitsadmin-getminretrydelay"></a>bitsadmin getminretrydelay

ファイルの転送を試行する前に、サービスが一時的なエラーを検出した後に待機する時間 (秒単位) を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getminretrydelay <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの最小再試行間隔を取得します。

```
C:\>bitsadmin /getminretrydelay myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)