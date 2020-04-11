---
title: bitsadmin info
description: '**Bitsadmin info**の Windows コマンドに関するトピックでは、指定したジョブに関する概要情報が表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5c306677-0d64-41c0-8276-5bba7750cecb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 20b8358caba3e0c07b0c985cb24e8f7bde43b06c
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123113"
---
# <a name="bitsadmin-info"></a>bitsadmin info

指定されたジョブに関する概要情報を表示します。

## <a name="syntax"></a>構文

```
bitsadmin /info <job> [/verbose]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| /verbose | 省略可。 各ジョブの詳細情報を提供します。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブに関する情報を取得します。

```
C:\>bitsadmin /info myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin info](bitsadmin-info.md)